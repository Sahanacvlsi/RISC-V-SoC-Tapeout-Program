# WEEK - 2 Task – BabySoC Fundamentals & Functional Modelling
---
# Objective
This week I am learning about the to build a solid understanding of SoC fundamentals and practice functional modelling of
the BabySoC using simulation tools (Icarus Verilog & GTKWave) through this workshop.
# CONTENT
1. What is a System-on-Chip (SoC)?
2. Components of a typical SoC (CPU, memory, peripherals, interconnect).
3. Why BabySoC is a simpliﬁed model for learning SoC concepts.
4. The role of functional modelling before RTL and physical design stages.

# SoC-Basics

**Repository:**

This repository documents introductory concepts of System-on-Chip (SoC) design, simplified through BabySoC examples. It answers four core questions useful for beginners in RTL and VLSI learning.

---

## 1. What is a System-on-Chip (SoC)?

A **System-on-Chip (SoC)** is an integrated circuit (IC) that combines all essential components of a complete electronic system onto a single chip. Instead of having separate chips for CPU, memory, I/O controllers, and communication interfaces, an SoC integrates them into one compact device. This leads to reduced power consumption, improved performance, and smaller physical footprint.

<img width="400" height="234" alt="image" src="https://github.com/user-attachments/assets/c72ca286-5db1-4053-9d3c-c6fe8d5df5ec" />

---

## 2. Components of a Typical SoC

A typical SoC contains the following key components:

* **CPU (Central Processing Unit):** Executes instructions and manages data operations.
* **Memory:** Includes volatile (SRAM, DRAM) and non-volatile (ROM, Flash) storage.
* **Peripherals:** Interfaces such as timers, UART, SPI, I2C, GPIO, ADC/DAC for interaction with external devices.
* **Interconnect (Bus / Network-on-Chip):** Connects CPU, memory, and peripherals. Examples: AMBA, AXI, AHB.
* **Accelerators (optional):** Specialized hardware for AI, graphics, or DSP tasks.
* **Power Management Unit:** Manages energy efficiency.
  <img width="1085" height="566" alt="image" src="https://github.com/user-attachments/assets/4f600e1d-3d5b-4477-bdd2-6f5d7f44f6df" />


---

## 3. Why BabySoC is a Simplified Model for Learning SoC Concepts

**BabySoC** is a minimal SoC model used in academic and training contexts to help learners understand core principles without the complexity of industrial SoCs. It usually includes:

* A small CPU core (e.g., RISC-V or custom simple CPU)
* Basic memory (ROM + SRAM)
* A few peripherals (UART, GPIO)
* A lightweight interconnect

By stripping down the design, BabySoC makes it easier to:

* Learn SoC integration at the RTL level.
* Understand verification and simulation flows.
* Connect theory to practice before moving to large-scale industrial SoCs.
<img width="571" height="339" alt="image" src="https://github.com/user-attachments/assets/95849c83-68d8-4788-8d81-4c4f5a122ca6" />

---

## 4. Role of Functional Modelling Before RTL and Physical Design Stages

Functional modelling is performed **before RTL design and physical implementation** to validate the system architecture and design choices at a higher abstraction. Its role includes:

* **Concept validation:** Ensures the intended system behavior is correct before committing to RTL.
* **Exploration:** Allows designers to test CPU, memory, and peripheral interactions using high-level models.
* **Debugging early:** Catching functional errors early reduces design cost and risk.
* **Specification clarity:** Provides a reference for RTL engineers and verification teams.

<img width="800" height="395" alt="image" src="https://github.com/user-attachments/assets/e76c8044-2340-4ed7-88ce-8aafb1e9f6ec" />

This stage is often implemented using languages like SystemC, C/C++, or Python-based models.

---

