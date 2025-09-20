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
<img width="946" height="681" alt="Screenshot from 2025-09-20 11-57-53" src="https://github.com/user-attachments/assets/3d06b02a-cf5d-4467-874c-ded7d1d1bb6e" />

### Iverilog 
```
sudo apt-get update
sudo apt-get update
sudo apt-get install iverilog
```
<img width="903" height="400" alt="Screenshot from 2025-09-20 09-58-36" src="https://github.com/user-attachments/assets/5a4d61e6-cd27-4207-8a8a-27ab6360e7fc" />


### GTKWAVE
```
$ sudo apt update
$ sudo apt install 
```
<img width="737" height="135" alt="Screenshot from 2025-09-20 10-00-16" src="https://github.com/user-attachments/assets/9a6378ca-35ba-4f1a-9924-fe099a96b3e8" />

<img width="996" height="422" alt="Screenshot from 2025-09-20 09-49-36" src="https://github.com/user-attachments/assets/88c2969c-e350-4d66-96e3-a683c476b935" />

