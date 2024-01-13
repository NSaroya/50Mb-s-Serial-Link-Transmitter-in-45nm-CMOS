# Objective
The objective of this project was to design the digital components of a sensor chip. The chip is comprised of sensing and analog components, as well as digital components. However, the main focus of this project lies on the digital components, which encompass the encoder, parallel-in serial-out shift register, digital MUX, and the transmitter module. Figure 1 shows a high-level block diagram of the system. 

Each sensor outputs some analog voltage, which is converted to a digital signal by the analog-to-digital converter (ADC). The encoder then reduces the amount of data required to represent the signal. This parallel data is converted to a serial data stream by the shift register. The serial data is sent to the transmitter where it is modulated and sent wirelessly to the base station.

<div align="center">
  
  ![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/67b1b2cf-86fb-4171-80a4-96b324b6b00a)

</div>

<p align="center">
  <strong>Figure 1:</strong> System Top-Level Block Diagram.
</p>

