# SKY130 RTL Design — Day 4: Gate-Level Simulation, Verilog Assignment Styles & Mismatches 🔍⚙️

Welcome to **Day 4** of my RTL Design & Synthesis journey with the **SKY130 PDK**!

Today, I focused on 3 crucial topics that bridge **functional correctness** and **physical realization** of digital logic:

-  **Gate-Level Simulation (GLS)**
-  **Synthesis-Simulation Mismatch**
-  **Blocking vs Non-Blocking Assignments in Verilog**

Each concept is backed by labs and practical hands-on experiments to understand how subtle coding choices impact synthesis and post-synthesis behavior.

---

## 📚 Topics Covered

### 1️⃣ Gate-Level Simulation (GLS)

**What is it?**
GLS is the simulation of a synthesized netlist (gate-level Verilog) to ensure the design behaves **exactly** as intended.

**Why perform GLS?**
- ✅ Validate post-synthesis functionality
- ⏱️ Check timing behavior using annotated delays (via SDF)
- 🔌 Verify test structures like scan chains
- 🔍 Catch synthesis-related bugs early

**When?**
After RTL synthesis and before moving to physical design (floorplanning, place & route).

---

### 2️⃣ Synthesis-Simulation Mismatch

A mismatch occurs when **pre-synthesis RTL simulation** results differ from **post-synthesis (GLS)**.

**Causes:**
- ❌ Non-synthesizable constructs (`initial`, delays `#`, `for`, `while`)
- 😵‍💫 Ambiguous or incomplete sensitivity lists
- 🤖 Different interpretation by synthesis vs simulation tools

💡 **Tip:** Always write synthesizable RTL and avoid simulation-only constructs.

---

### 3️⃣ Blocking vs. Non-Blocking Assignments

Verilog has two types of procedural assignments:

#### ➡️ Blocking (`=`)

- Executes **immediately** in the order written
- Use in **combinational logic**
```verilog
always @(*) y = a & b;
```
## Labs & Experiments

All design files are stored in verilog_labs/ folder.

### 💡 Lab 1: Ternary Operator MUX
```
module ternary_operator_mux (input i0, input i1, input sel, output y);
  assign y = sel ? i1 : i0;
endmodule
```
🔬 Function: If sel = 1, output is i1; else i0.
### 🛠️ Lab 2: Yosys Synthesis of MUX

Used the standard Yosys flow:
```
read_verilog ternary_operator_mux.v
synth -top ternary_operator_mux
abc -liberty sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog mux_synth.v
```
### 🧮 Lab 3: Gate-Level Simulation of Synthesized MUX

Simulated the netlist along with primitives:
```
iverilog sky130_fd_sc_hd.v mux_synth.v testbench.v -o mux_gls.out
./mux_gls.out
gtkwave mux.vcd
```
🧠 Observation: GLS matched RTL — confirms correct synthesis.
### ❌ Lab 4: Bad MUX Design (RTL Pitfalls)
```
module bad_mux (input i0, input i1, input sel, output reg y);
  always @ (sel) begin
    if (sel)
      y <= i1;
    else 
      y <= i0;
  end
endmodule
```
🚨 Issues:
  - Incomplete sensitivity list (missing i0, i1)
  - Used non-blocking (<=) in combinational logic

✅ Corrected:
```
always @(*) begin
  if (sel)
    y = i1;
  else
    y = i0;
end
```
### 🧪 Lab 5: GLS of Bad MUX

Simulated the synthesized bad_mux.
⚠️ Result: Mismatches and unexpected glitches.

💡 Lesson: Code style matters in hardware!
### ⚠️ Lab 6: Blocking Assignment Caveat
```
module blocking_caveat (input a, input b, input c, output reg d);
  reg x;
  always @(*) begin
    d = x & c;   // ❌ using old value of x
    x = a | b;
  end
endmodule
```
🔁 Problem: d is computed before x is updated.

✅ Fix:
```
always @(*) begin
  x = a | b;
  d = x & c;
end
```
### 🏗️ Lab 7: Synthesis of Blocking Caveat (Corrected)

Used Yosys to synthesize the corrected logic.
🧠 Confirmed: Logical correctness + optimal gate mapping.
