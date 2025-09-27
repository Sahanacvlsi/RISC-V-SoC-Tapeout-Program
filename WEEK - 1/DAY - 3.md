# SKY130 PDK & RTL Design — Day 3: Combinational and Sequential Optimization ⚡️

Welcome to **Day 3** of my RTL Design and Synthesis journey using the SKY130 PDK!  
Today was focused on **design optimization techniques** for both combinational and sequential logic. I explored how synthesis tools like Yosys can enhance circuit efficiency using methods like constant propagation, state optimization, cloning, and retiming.

---

## 🧠 Topics Covered

### 1️⃣ Constant Propagation
An optimization where constant values are propagated throughout the design. This simplifies logic, reduces gate count, and improves speed.

**Example Behavior:**
If `a = 0`, and we have `assign y = a ? b : 0;`, then `y = 0` regardless of `b`.  
→ This lets the tool optimize the logic away.

### 2️⃣ State Optimization
Used in FSMs (Finite State Machines). Involves:
- **State Reduction**: Merging equivalent states.
- **Encoding Optimization**: Choosing efficient binary values.
- **Power Optimization**: Gating logic when idle.

### 3️⃣ Cloning
Cloning duplicates certain logic elements to:
- Reduce load
- Improve timing
- Balance paths
Common in datapaths or fan-out-heavy designs.

### 4️⃣ Retiming
A sequential optimization where registers are moved across logic boundaries to improve:
- Critical path timing
- Clock period
- Power efficiency  
Retiming keeps **functionality same** while improving performance.

---

## 🧪 Lab Work: Optimization in Action

### 💡 Lab 1 — Constant Propagation Basic

**File**: `opt_check.v`
```verilog
module opt_check (input a , input b , output y);
	assign y = a ? b : 0;
endmodule

