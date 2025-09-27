## 📂 Week 1 - RTL Design and Synthesis
# SKY130 PDK & RTL Design — Day 1 Learnings 🚀

Welcome to my Day 1 journey into digital IC design using the SKY130 PDK! Today, I focused on understanding the basics of simulation, Verilog coding, and the first steps of synthesis using open-source tools. This repo captures my notes, example codes, and workflows.

---

## What I Learned Today 🔍

### Simulator, Design, and Testbench Basics  
- **Simulator:** A software tool that verifies the correctness of your digital design by applying test inputs and checking outputs. It’s like a virtual lab where you catch bugs before hardware fabrication.  
- **Design:** Your actual Verilog code that describes the intended hardware behavior.  
- **Testbench:** A specialized Verilog environment that generates stimuli (inputs) to your design and monitors outputs during simulation to confirm the design works as expected.

### Getting Started with `iverilog` for Simulation  
- Learned the simulation flow using **iverilog**, an open-source Verilog compiler and simulator.  
- Compiled both the design and testbench files to generate a `.vcd` (Value Change Dump) file.  
- Opened the `.vcd` file in **GTKWave** to visually inspect signal transitions over time — super helpful for debugging!

### Lab: Simulating a 2-to-1 Multiplexer 🧩  
- Practiced by simulating a simple **2-to-1 multiplexer**.  
- The mux chooses between two inputs (`i0` and `i1`) based on a select signal (`sel`), passing the chosen input to the output (`y`).  
- Ran the simulation, viewed waveforms, and confirmed the mux behaves correctly.

### Verilog Code Snippet: 2-to-1 Multiplexer

```verilog
module good_mux (input i0, input i1, input sel, output reg y);
    always @ (*)
    begin
        if(sel)
            y <= i1;
        else 
            y <= i0;
    end
endmodule
