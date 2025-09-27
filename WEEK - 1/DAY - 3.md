# SKY130 PDK & RTL Design — Day 3: Combinational and Sequential Optimization 

Welcome to **Day 3** of my RTL Design and Synthesis journey using the SKY130 PDK!  
Today was focused on **design optimization techniques** for both combinational and sequential logic. I explored how synthesis tools like Yosys can enhance circuit efficiency using methods like constant propagation, state optimization, cloning, and retiming.

---

## Topics Covered

### 1️ Constant Propagation
An optimization where constant values are propagated throughout the design. This simplifies logic, reduces gate count, and improves speed.

**Example Behavior:**
If `a = 0`, and we have `assign y = a ? b : 0;`, then `y = 0` regardless of `b`.  
→ This lets the tool optimize the logic away.

### 2️ State Optimization
Used in FSMs (Finite State Machines). Involves:
- **State Reduction**: Merging equivalent states.
- **Encoding Optimization**: Choosing efficient binary values.
- **Power Optimization**: Gating logic when idle.

### 3️ Cloning
Cloning duplicates certain logic elements to:
- Reduce load
- Improve timing
- Balance paths
Common in datapaths or fan-out-heavy designs.

### 4️ Retiming
A sequential optimization where registers are moved across logic boundaries to improve:
- Critical path timing
- Clock period
- Power efficiency  
Retiming keeps **functionality same** while improving performance.

---

## Lab Work: Optimization in Action

###  Lab 1 — Constant Propagation Basic

**File**: `opt_check.v`
```verilog
module opt_check (input a , input b , output y);
	assign y = a ? b : 0;
endmodule
```
🔍 What it does:
If a = 0, y = 0 always. Tool should optimize logic accordingly.

###  Lab 2 — Constant as Output

File: opt_check2.v
```
Module opt_check2 (input a , input b , output y);
	assign y = a ? 1 : b;
endmodule
```
 What it does:

    y = 1 when a = 1

    y = b when a = 0

Acts like a mux but includes a constant input.
###  Lab 3 — Same as Lab 2 (Reviewed for Optimization Patterns)

Functionality Recap:
Another mux-like pattern:

assign y = a ? 1 : b;

Observed how synthesis tools handle repeated constant patterns.
### Lab 4 — Nested Ternary Expression

File: opt_check4.v
```
module opt_check4 (input a , input b , input c , output y);
	assign y = a ? (b ? (a & c) : c) : (!c);
endmodule
```
Simplified Logic:
After analyzing the logic, it reduces to:

assign y = a ? c : !c;

Shows how powerful logic reduction can simplify nested conditions.
###  Lab 5 — Flip-Flop with Constant 1

File: dff_const1.v
```
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end
endmodule
```
 What it does:

    Asynchronous reset sets q = 0

    Otherwise, always loads 1

Insight: This register always ends up as 1, so tool may optimize away FF logic depending on usage.
### Lab 6 — Flip-Flop with Fixed Output

File: dff_const2.v
```
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	q <= 1'b1;
end
endmodule
```
 What it does:

    Regardless of input/reset/clock, q is always 1.

##  Tool behavior: Should recognize this as a constant output → can remove FF in synthesis.
** Synthesis Flow Used**

For each design, I followed this synthesis flow in Yosys:

**yosys**
```
# Read the liberty file
read_liberty -lib /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib

# Read design
read_verilog opt_check.v  # or the respective file

# Synthesize
synth -top <module_name>

# Optimization step
opt_clean -purge

# Technology mapping
abc -liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib

# View schematic
show
```
### Summary

**Focus:**
Optimizing Verilog designs using synthesis techniques that reduce gate count, improve timing, or simplify logic.

Techniques Covered:

✅ Constant Propagation

✅ FSM State Optimization

✅ Logic Cloning

✅ Retiming Flip-Flops

**Labs Completed:**
✔️ 6 labs showing optimization effects with Verilog code examples
