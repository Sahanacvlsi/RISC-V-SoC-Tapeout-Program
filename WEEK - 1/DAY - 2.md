# SKY130 PDK & RTL Design — Day 2 Learnings

This repo contains my notes, code, and insights from Day 2 of my RISC-V-SoC-Tapeout-Program design program using the SKY130 PDK and RTL design tools.

---

## What I Worked On Today

### SKY130 Timing Libraries  
- Explored the SKY130 PDK and understood the naming scheme for timing libraries (process corners, voltage, temperature).  
- Learned how to open and read `.lib` files to check timing info.

### Hierarchical vs Flattened Synthesis  
- Tried out both hierarchical and flattened synthesis flows using Yosys.  
- Noticed pros and cons of each: hierarchy is easier for debugging, flattening enables better optimization but is slower.

### Flip-Flop Coding Styles  
- Coded various D flip-flops in Verilog: asynchronous reset, asynchronous set, and synchronous reset styles.  
- Tested these with simple testbenches and simulated using Icarus Verilog and GTKWave.

### Simulation & Synthesis Flow  
- Practiced compiling and running simulations (`iverilog`, `gtkwave`).  
- Ran synthesis with Yosys using the SKY130 liberty file for tech mapping and saw the gate-level netlist.

---

## Code & Files

- `dff_asyncres.v` — async reset D flip-flop  
- `dff_async_set.v` — async set D flip-flop  
- `dff_syncres.v` — sync reset D flip-flop  
- Testbenches and liberty files included for simulation and synthesis.

---

## Commands I Used

```bash
# Open timing library
gedit sky130_fd_sc_hd__tt_025C_1v80.lib

# Simulation
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd

# Yosys synthesis
yosys
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty sky130_fd_sc_hd__tt_025C_1v80.lib
show

