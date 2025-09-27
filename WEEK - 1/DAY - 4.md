# SKY130 RTL Design — Day 4: Gate-Level Simulation, Verilog Assignment Styles & Mismatches 🔍⚙️

Welcome to **Day 4** of my RTL Design & Synthesis journey with the **SKY130 PDK**!

Today, I focused on 3 crucial topics that bridge **functional correctness** and **physical realization** of digital logic:

- 🧩 **Gate-Level Simulation (GLS)**
- ⚠️ **Synthesis-Simulation Mismatch**
- 🔁 **Blocking vs Non-Blocking Assignments in Verilog**

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

