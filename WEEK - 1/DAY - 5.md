# Verilog Control Structures and Optimization Labs 📘

Hi! This repository contains the Verilog labs and explanations I made to better understand if-else statements, latch inference, loops, generate blocks, and the design of a ripple carry adder. I’ve included detailed code examples and synthesis notes from my learning process.

# RTL Workshop Optimization

**Repository:** 

This repo contains Day 5 material for an RTL workshop: optimization in synthesis — if-else, for loops, generate blocks, and latch inference labs. Everything is provided as ready-to-copy files (Verilog sources, README notes, and a Makefile). Drop these files into your Git repo and push.


## How to use

1. Copy the `labs/` files into your repo folder.
2. Simulate with Icarus Verilog / GTKWave (or use your preferred simulator / synthesis tool):

```sh
# simulate (iverilog + vvp)
iverilog -o simv labs/fa.v labs/lab12_rca.v && vvp simv
# or run all testbenches you create
```

3. For synthesis, run your FPGA tool (Vivado/Quartus/others). Use the `docs/day5-notes.md` for synthesis tips.

---
# LAB 
## Files (code used for lab)

### labs/lab01_incomp_if.v

```verilog
module incomp_if (input i0, input i1, input i2, output reg y);
always @(*) begin
    if (i0)
        y <= i1;
end
endmodule
```

### labs/lab02_incomp_synth.txt

```
# expected: latch inferred for 'y' because when i0==0, y not assigned
# open synthesis report to inspect inferred latches
```

### labs/lab03_incomp_if2.v

```verilog
module incomp_if2 (input i0, input i1, input i2, input i3, output reg y);
always @(*) begin
    if (i0)
        y <= i1;
    else if (i2)
        y <= i3;
end
endmodule
```

### labs/lab04_incomp2synth.txt

```
# expected: latch inferred for 'y' (no assignment when i0==0 and i2==0)
```

### labs/lab05_comp_case.v

```verilog
module comp_case (input i0, input i1, input i2, input [1:0] sel, output reg y);
always @(*) begin
    case(sel)
        2'b00 : y = i0;
        2'b01 : y = i1;
        default : y = i2;
    endcase
end
endmodule
```

### labs/lab06_compcase_synth.txt

```
# expected: no latch for 'y' (all cases assign y)
```

### labs/lab07_bad_case.v

```verilog
module bad_case (
    input i0, input i1, input i2, input i3,
    input [1:0] sel,
    output reg y
);
always @(*) begin
    case(sel)
        2'b00: y = i0;
        2'b01: y = i1;
        2'b10: y = i2;
        2'b1?: y = i3; // caution: wildcard patterns may overlap and cause unexpected behavior
    endcase
end
endmodule
```

### labs/lab08_partial_case_assign.v

```verilog
module partial_case_assign (
    input i0, input i1, input i2,
    input [1:0] sel,
    output reg y, output reg x
);
always @(*) begin
    case(sel)
        2'b00: begin
            y = i0;
            x = i2;
        end
        2'b01: y = i1;
        default: begin
            x = i1;
            y = i2;
        end
    endcase
end
endmodule
```

### labs/lab09_mux_generate.v

```verilog
module mux_generate (
    input i0, input i1, input i2, input i3,
    input [1:0] sel,
    output reg y
);
wire [3:0] i_int;
assign i_int = {i3, i2, i1, i0};
integer k;
always @(*) begin
    for (k = 0; k < 4; k = k + 1) begin
        if (k == sel)
            y = i_int[k];
    end
end
endmodule
```

### labs/lab10_demux_case.v

```verilog
module demux_case (
    output o0, output o1, output o2, output o3,
    output o4, output o5, output o6, output o7,
    input [2:0] sel,
    input i
);
reg [7:0] y_int;
assign {o7, o6, o5, o4, o3, o2, o1, o0} = y_int;
always @(*) begin
    y_int = 8'b0;
    case(sel)
        3'b000 : y_int[0] = i;
        3'b001 : y_int[1] = i;
        3'b010 : y_int[2] = i;
        3'b011 : y_int[3] = i;
        3'b100 : y_int[4] = i;
        3'b101 : y_int[5] = i;
        3'b110 : y_int[6] = i;
        3'b111 : y_int[7] = i;
    endcase
end
endmodule
```

### labs/lab11_demux_generate.v

```verilog
module demux_generate (
    output o0, output o1, output o2, output o3,
    output o4, output o5, output o6, output o7,
    input [2:0] sel,
    input i
);
reg [7:0] y_int;
assign {o7, o6, o5, o4, o3, o2, o1, o0} = y_int;
integer k;
always @(*) begin
    y_int = 8'b0;
    for (k = 0; k < 8; k = k + 1) begin
        if (k == sel)
            y_int[k] = i;
    end
end
endmodule
```

### labs/fa.v

```verilog
module fa (input a, input b, input c, output co, output sum);
    assign {co, sum} = a + b + c;
endmodule
```

### labs/lab12_rca.v

```verilog
module rca (
    input [7:0] num1,
    input [7:0] num2,
    output [8:0] sum
);
wire [7:0] int_sum;
wire [7:0] int_co;

genvar i;
generate
    for (i = 1; i < 8; i = i + 1) begin : gen_fa
        fa u_fa_1 (.a(num1[i]), .b(num2[i]), .c(int_co[i-1]), .co(int_co[i]), .sum(int_sum[i]));
    end
endgenerate

fa u_fa_0 (.a(num1[0]), .b(num2[0]), .c(1'b0), .co(int_co[0]), .sum(int_sum[0]));

assign sum[7:0] = int_sum;
assign sum[8] = int_co[7];
endmodule
```

---



---

## Makefile 

```makefile
SIM=iverilog
SIM_FLAGS=-g2012

all: sim

sim:	$(SIM) $(SIM_FLAGS) -o simv labs/fa.v labs/lab12_rca.v && vvp simv

clean:	rm -f simv *.vcd
```
##  SUMMARY 

This file summarizes the key points from Day 5 (copy the content from your workshop notes if you want):

* Always assign every output in every branch of combinational `always @(*)` blocks to avoid latches.
* Use `default` in `case` statements for safety.
* For-loops synthesizable only with a fixed iteration count known at compile time.
* `genvar` + `generate` create replicated hardware at elaboration time.
* Check synthesis reports for inferred latches and combinational loops.
