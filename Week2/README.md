# BabySoC Project

This project aims at an open-source System on Chip (SoC) based on RVMYTH, a RISC-V-based processor core. It integrates a Phase-Locked Loop (PLL) for clock generation and control, alongside a 10-bit Digital-to-Analog Converter (DAC) for interfacing with external analog systems. By converting digital signals into analog, this DAC allows BabySoC to communicate with devices that accept analog inputs.

---

## What is an SoC?

A System on a Chip (SoC) is an integrated circuit that consolidates all or most key components of a computer or electronic system into a single microchip. This includes a central processing unit (CPU), memory modules, input/output interfaces, and often other specialized components like graphics processing units (GPUs), digital signal processors, and communication modules such as Wi-Fi or cellular modems.

---

## Components of a Typical SoC

A typical SoC integrates several crucial components on a single microchip, enabling a complete functional system. The primary components include:

### Central Processing Unit (CPU)  
The CPU is the core of the SoC, responsible for executing instructions and managing operations. Modern SoCs may have multiple CPU cores, often based on architectures like ARM, allowing for multitasking and enhanced performance.

### Memory  
SoCs integrate various types of memory for storage and fast data access:  
- **RAM (Random Access Memory):** Volatile memory used for temporary data storage during operation, including SRAM and DRAM.  
- **ROM (Read-Only Memory):** Non-volatile memory for firmware and persistent system instructions.  
Additional memory types include flash memory and caches for performance optimization.

### Peripherals  
Peripherals provide interfaces and additional functions:  
- **Input/Output Interfaces (I/O):** Connect external devices via USB, HDMI, UART, SPI, and other protocols.  
- **Connectivity Modules:** Integrated Wi-Fi, Bluetooth, Ethernet, and cellular modules for communication.  
- **Digital Signal Processors (DSP):** Specialized processors for real-time signal processing in audio, video, and data communication.  
- **Graphics Processing Unit (GPU):** Handles rendering of images, video, and graphical user interfaces.  
- **Power Management Unit (PMU):** Manages power consumption for energy efficiency and battery life.  
- **Security Modules:** Handle encryption, secure boot, and protection measures.

### Interconnect  
The interconnect is the internal communication network (bus or crossbar) linking all components inside the SoC, allowing data transfer between CPU, memory, peripherals, and other cores efficiently and with low latency.

---

## Why BabySoC is a Simplified Model for Learning SoC Concepts

- **Simplification of Complex Systems:** Distills essential elements of a full SoC into a smaller-scale model, making it easier to grasp the interaction of SoC parts.  
- **Focus on Core Components:** Includes a simple CPU, basic memory, minimal peripherals, and straightforward interconnect to focus on critical modules.  
- **Hands-on Learning:** Provides practical examples, simulations, or projects enabling active learning through experimentation.  
- **Stepwise Complexity:** Starts with a basic SoC layout and incrementally introduces additional features for progressive learning.

---

## Role of Functional Modeling Before RTL and Physical Design

Functional modeling is critical before RTL and physical design stages for verifying design correctness at high abstraction levels.

1. **Early Verification of Design Intent:** Simulates and validates SoC behavior and algorithms early on without hardware implementation details.  
2. **Identifying Design Issues Early:** Detects logical errors and inefficiencies before time-consuming RTL coding and physical design.  
3. **Faster Simulation and Iteration:** Enables rapid exploration and tuning due to faster high-level simulations.  
4. **Facilitates Communication:** Abstract models help designers and engineers understand and discuss design goals.  
5. **Foundation for Subsequent Stages:** Validated functional models serve as blueprints for RTL and physical design, ensuring consistency.

---

## VSDBabySoC Design Components

- **rvmyth.v (RISC-V Core):** A simple RISC-V processor that outputs a 10-bit digital signal (OUT) to be converted by the DAC.  
- **avsdpll.v (PLL Module):** A phase-locked loop generating a stable clock (CLK) for the RISC-V core.  
- **avsddac.v (DAC Module):** Converts the 10-bit digital signal from the rvmyth core to an analog output.

---

## TLV to Verilog Conversion

sudo apt update

sudo apt install python3-venv python3-pip

> **Note:** The following commands should be run in **bash** only. If you are using **tcsh**, switch to bash by running:
>
> ```
> bash
> ```
> 
python3 -m venv sp_env

source sp_env/bin/activate

pip install pyyaml click sandpiper-saas

sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/

---

## Pre-Synthesis Simulation

mkdir -p output/pre_synth_sim

iverilog -o output/pre_synth_sim/pre_synth_sim.out
-DPRE_SYNTH_SIM
-I src/include -I src/module
src/module/testbench.v

cd output/pre_synth_sim
./pre_synth_sim.out

gtkwave pre_synth_sim.vcd

>  Signals `D[9:0]` and `OUT[9:0]` can be viewed as analog signals in GTKWave by right-clicking the signals and selecting:  
> `Data Format > Analog > Interpolated`


