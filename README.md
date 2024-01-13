# Objective
The objective of this project was to design the digital components of a sensor chip. The chip is comprised of sensing and analog components, as well as digital components. However, the main focus of this project lies on the digital components, which encompass the encoder, parallel-in serial-out shift register, digital MUX, and the transmitter module. Figure 1 shows a high-level block diagram of the system. 

Each sensor outputs some analog voltage, which is converted to a digital signal by the analog-to-digital converter (ADC). The encoder then reduces the amount of data required to represent the signal. This parallel data is converted to a serial data stream by the shift register. The serial data is sent to the transmitter where it is modulated and sent wirelessly to the base station.

<div align="center">
  
  ![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/67b1b2cf-86fb-4171-80a4-96b324b6b00a)

</div>

<p align="center">
  <strong>Figure 1:</strong> System Top-Level Block Diagram.
</p>

This part of the design flow includes the following steps:
- Create circuit schematics
- Create the symbol view
- Create simulation test-benches for typical model parameters

Using the theoretical width-ratio between PMOS and NMOS transistors (approximately two) as a starting point, resize and re-simulate the transistor sizes so that:
- Approximately equal rise and fall times of the signal pulses at the outputs are achieved, i.e. the cross-over point at around VDD/2.
Gate propagation delay and power dissipation of the gates can be measured.
- The gate performance can be measured as a function of varying the load capacitance.

The Cadence technology will be used for the entirity of this project.

# Design
