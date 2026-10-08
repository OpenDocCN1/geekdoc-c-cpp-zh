# TABLE 8.1 PIC18F4321 Pinout description (Continued)

| Pin Number | Pin Name | Pin Type | Description |
|---|---|---|---|
| 10 | RE2 | Input/Output | Digital I/O; port E bit 2. |
|  | | Input | Chip Select control for Parallel Slave Port (see related RD and WR ). |
|  | AN7 | Input | Analog input 7. |
| 11 | VDD | Power | Positive supply for logic and I/O pins. |
| 12 | VSS | Ground | Ground reference for logic and I/O pins. |
| 13 | OSC1 | Input | Oscillator crystal input or external clock source input. |
|  | CLKI | Input | External clock source input. Always associated with pin function OSC1.(See related OSC1/CLKI, OSC2/CLKO pins.) |
|  | RA7 | Input/Output | Digital I/O; port A bit 7. |
| 14 | OSC2 | Output | Oscillator crystal output. Connects to crystal or resonator in Crystal Oscillator mode. In RC, EC and INTIO modes, OSC2 pin outputs |
|  | CLKO | Output | CLKO which has one-fourth the frequency of OSC1 and denotes the instruction cycle rate |
|  | RA6 | Input/Output | Digital I/O; port A bit 6. |
| 15 | RCO | Input/Output | Digital I/O; port C bit 0. |
|  | T1OSO | Output | Timer1 oscillator analog output. |
|  | T13CKI | Input | Timer1/Timer3 external clock input |
| 16 | RC1 | Input/Output | Digital I/O; port C bit 1. |
|  | T1OSI | Input | Timer1 oscillator analog input. |
|  | CCP2 | Input/Output | Capture 2 input/Compare 2 output/PWM 2 output; default assignment for CCP2 when Configuration bit, CCP2MX, is set. |
| 17 | RC2 | Input/Output | Digital I/O; port C bit 2. |
|  | CCP1 | Input/Output | Capture 1 input/Compare 1 output/PWM 1 output. |
|  | P1A | Output | Enhanced CCP1 output. |
| 18 | RC3 | Input/Output | Digital I/O; port C bit 3. |
|  | SCK | Input/Output | Synchronous serial clock input/output for SPI mode. |
|  | SCL | Input/Output | Synchronous serial clock input/output for I$^{2}$C$^{TM}$ mode |
| 19 | RD0 | Input/Output | Digital I/O; port D bit 0. |
|  | PSP0 | Input/Output | Parallel Slave Port data. |
| 20 | RD1 | Input/Output | Digital I/O; port D bit 1. |
|  | PSP1 | Input/Output | Parallel Slave Port data. |
| 21 | RD2 | Input/Output | Digital I/O; port D bit2. |
|  | PSP2 | Input/Output | Parallel Slave Port data |
| 22 | RD3 | Input/Output | Digital I/O; port D bit 3. |
|  | PSP3 | Input/Output | Parallel Slave Port data. |