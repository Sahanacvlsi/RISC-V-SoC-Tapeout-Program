# RISC-V-SoC-Tapeout-Program
This repository is a week-by-week log of my progress and learnings in the VSD SoC Tapeout Program.  In this program, we explore the complete flow of System-on-Chip (SoC) design — starting from RTL (Register Transfer Level) design and verification to GDSII (final layout) using open-source EDA tools.
This repository is a my week-by-week log of my progress and learnings in the VSD SoC Tapeout Program.  In this program, we explore the complete flow of System-on-Chip (SoC) design — starting from RTL (Register Transfer Level) design and verification to GDSII (final layout) using open-source EDA tools.

## Why this program matters:

- Strengthens India’s semiconductor design ecosystem.
- Empowers students and engineers with open-source silicon design skills.
- Contributes to the global RISC-V and open hardware movement.

 # WEEK - 0
 ## Tools Installation
 Tools installed:
- **OS**: Ubuntu 20.04 or higher  
- **RAM**: 6 GB  
- **Storage**: 50 GB HDD (free space)  
- **CPU**: 4 vCPU
### Iverilog 
```sudo apt-get update
sudo apt-get install iverilog
```
### Yosys 
``` $ sudo apt-get update
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys
$ sudo apt install make (If make is not installed please install it)
$ sudo apt-get install build-essential clang bison flex \
 libreadline-dev gawk tcl-dev libffi-dev git \
 graphviz xdot pkg-config python3 libboost-system-dev \
 libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make config-gcc
$ make
$ s<img width="1920" height="1080" alt="Sign up in app" src="https://github.com/user-attachments/assets/acaa067c-6499-464f-828e-00097ab973b3" />
udo make install'
```
### Iverilog 
```
sudo apt-get update
sudo apt-get install iverilog 
### gtkwave
$ sudo apt-get update
$ sudo apt install gtkwave
```
