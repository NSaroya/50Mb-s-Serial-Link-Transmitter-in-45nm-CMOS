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
## Invertor Design
### Schematics
![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/2bff407d-a949-4a0c-991a-58ea99e45138)

## MUX AND NAND GATE DESIGN
### Schematics
![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/fb24fca9-41f3-4ccb-8207-798b9d6a5165)
4-input NAND gate schematic

![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/30bacd9d-6380-4de4-a4ac-b2d346114e10)
MUX schematic with available inputs D0, D1, D2 and D3

![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/132d0cff-4c06-4338-b0f0-f54ae6cae002)
MUX testbench schematic with set input waveform parameters for testing the MUX block

### Test Bench Simulation

|Input Voltage | Voltage 1 | Voltage 2 | Rise time | Fall time | Pulse width | Period  |
|------------|---------------|-----------|-----------|-----------|-----------|-------------|
| A          | 0             | 1.0       | 1p        | 1p        | 80n       | 160n        |         
| B          | 0             | 1.0       | 1p        | 1p        | 40n       | 80n         |         
| C          | 0             | 1.0       | 1p        | 1p        | 20n       | 40n         |         
| D          | 0             | 1.0       | 1p        | 1p        | 10n       | 20n         |         

4-INPUT NAND GATE SIMULATION VPULSE PARAMETERS.

![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/f07ee3d4-b31f-4f6f-a178-521f4e7076b1)
3-input and 4-input NAND gate simulation results. Transient Simulation time 200ns.

|       | Tpdr (s)       | Tpdf (s)       |
|-------|----------------|----------------|
| NAND3 | 1.802E-11      | 1.197E-11      |
| NAND4 | 2.831E-11      | 1.628E-11      |

PROPOGATION DELAYS OF 4-INPUT NAND GATE 

|Input  | Voltage 1 | Voltage 2 | Delay time | Rise time | Fall time | Pulse width | Period  |
|----|----------------|-----------|-----------|------------|-----------|-----------|-------------|
| S1 | 1.0            | 0         | -5n       | 1p         | 1p        | 40n       | 80n         |         
| S0 | 1.0            | 0         | -5n       | 1p         | 1p        | 20n       | 40n         |         
| A  | 0              | 1.0       | 0n        | 1p         | 1p        | 10n       | 80n         |         
| B  | 1.0            | 0         | 20n       | 1p         | 1p        | 10n       | 80n         |         
| C  | 0              | 1.0       | 40n       | 1p         | 1p        | 10n       | 80n         |         
| D  | 1.0            | 0         | 60n       | 1p         | 1p        | 10n       | 80n         |         

MUX SIMULATION VPULSE PARAMETERS.

![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/68058b12-f922-4a60-b94b-b384fd27ef27)
MUX Timing Simulation to find the propagation delay of the MUX output with respect rising and falling edge of each of the 4 inputs

|     | Tpdr (s)       | Tpdf (s)       |
|-----|----------------|----------------|
| A   | 3.417E-10      | 3.0E-11        |
| B   | 4.266E-10      | 3.89E-11       |
| C   | 4.834E-10      | 4.52E-11       |
| D   | 5.194E-10      | 4.84E-11       |

To size the transistors of a n-input complementary logic NAND for equal pull-up and pull-down resistance assuming µn = 1.25µp. The NMOS transistors must be upsized by a factor of n so that each transistor resistance is R/n and effective pull-down resistance is R. In the pull-up network, the worse possible resistance is when only one PMOS transistor is active, and since µn = 1.25µp, we must up-size the PMOS transistor by a factor of 1.25 such that the effective resistance is 1.25*(R/k), where k = 1.25, hence the pull-up resistance is R. 

## TPSC Flip Flop Design
Each stage of the circuit was optimally sized using logical effort analysis to minimize delay and the propagation delays were characterized via simulations. The nominal rising propagation delay was observed to be 77.8ps, while the falling edge propagation delay was 102.4ps. For process variations, SS process simulates the worst-case and FF process displaying the best-case for propagation delays respectively. SF process is slightly better than SS process, and FS having slightly higher propagation delay than FF process and typical process (TT) being at nominal.

**Flip-Flop Schematic**

![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/c66497c0-cae6-4039-a7ef-b03a0da574fc)

TSPC flip-flop schematic using transistor size determined by logical effort analysis. 

**Plot of Flip-flop functionality**

![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/0037c71b-f414-43b8-b4a2-30c6736c8e0f)

TSPC flip flop functionality – samples the input on a positive clock Edge transition to output Q

**Temperature variation plot**

![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/bd0a62a2-554f-4df2-8eaa-bb898c6c8a69)

Temperature variation sweep – rise time of a TSPC flip flop increases with temperature

**Process variation plot**

![image](https://github.com/NSaroya/50Mbps-Serial-Link-Transmitter-in-45nm-CMOS/assets/156468713/5c52ae0c-cd56-4a4e-8cbc-81f01a8f082e)

Process variation plot at 27C – shortest rise time for FF process, while SS having slowest rise time. FS and SF being slightly faster than SS and TT respectively.

**Temperature propagation delays**

| Q (Output) | Nominal   | Min       | Max       | 0°C       | 27°C      | 70°C      |
|------------|-----------|-----------|-----------|-----------|-----------|-----------|
| Tprop0-1   | 77.8p     | 62.34p    | 77.80p    | 62.34p    | 67.92p    | 77.8p     |
| Tprop1-0   | 102.4p    | 102.4p    | 79.57p    | 79.57p    | 87.99p    | 102.4p    |

**Process corner propagation delays**

|Q (Output)  | Nominal   | Min       | Max       | SS        | SF        | TT        | FS        | FF        |
|------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
| Tprop0-1   | 77.80p    | 57.88p    | 81.81p    | 81.81p    | 65.52p    | 67.92p    | 72.32p    | 57.88p    |
| Tprop1-0   | 102.4p    | 74.23p    | 107.7p    | 107.7p    | 73.48p    | 87.99p    | 85.2p     | 74.23p    |

**Setup and Hold times**

|          | T_setup  | T_hold  |
|----------|----------|---------|
| Values   | -5ps     | -8ps    |

The propagation delays tend to increase as the temperature increases. For process variations, SS process simulates the worst-case and FF process displaying the best-case for propagation delays respectively. SF process is slightly better than SS process, and FS having slightly higher propagation delay than FF process and typical process (TT) being at nominal. 

The setup time is the minimum amount of time that the input data must be stable before the clock edge arrives. The setup time affects the maximum clock frequency as a shorter setup allows the input data to be stable for a shorter period before the clock edge arrives, which means that the circuit can operate at a higher frequency. The maximum clock frequency can be calculated using the equation, maximum clock frequency = 1/ (max data path delay – min clock path delay + Tsetup.

During the falling edge transition, the output node needs to transition from a pre-charged high state to a low state. This discharge operation can take longer than the latching operation during the rising edge. Further, the parasitic capacitance of the output node is higher for the falling edge than the rising edge, which results in a longer propagation delay. 
