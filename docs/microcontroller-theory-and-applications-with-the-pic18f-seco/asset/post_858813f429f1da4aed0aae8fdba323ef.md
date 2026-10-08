
current is called $I_{source}$ or output high current, $I_{OH}$. This is typically represented by a negative sign in front of the current value in the TTL data book, a notation indicating that the chip is losing current. For a low output value of the logic gate, the switches in $\mathbf{Q}_{1}$ and D are open and the switch in $\mathbf{Q}_{2}$ closes. A current flows from the output through $\mathbf{Q}_{2}$ to ground. This current is called $I_{sink}$ or Output Low current, $I_{OL}$. This is represented by a positive sign in front of the current value in the TTL data book, indicating that current is being added to the chip. Either $I_{source}$ or $I_{sink}$ can be used to drive a typical output device such as an LED. $I_{source}$ $(I_{OH})$ is normally much smaller than $I_{sink}$ $(I_{OL})$. $I_{source}$ $(I_{OH})$ is typically $-0.4$ mA (or $-400$ $\mu$A) at a minimum voltage of 2.7 V at the output. $I_{source}$ is normally used to drive devices that require high currents. A current amplifier (buffer) such as a transistor or an inverting buffer chip such as 74LS368 needs to be connected at the output if $I_{source}$ is used to drive a device such as an LED requiring high current (10 mA to 20 mA). $I_{sink}$ is normally 8 mA.

The totem-pole outputs must not be tied together. When two totem-pole outputs are connected together with the output of one gate HIGH and the output of the second gate LOW, the excessive amount of current drawn can produce enough heat to damage the transistors in the circuit.

Tristate is a special totem-pole output that allows connecting the outputs together like the open-collector outputs. When a totem-pole output TTL gate has this property, it is called a tristate (three state) output. A tristate has three output states:

-   1.  A LOW level state when the lower transistor in the totem-pole is ON and the upper transistor is OFF.
-   2.  A HIGH level when the upper transistor in the totem-pole is ON and the lower transistor is OFF.
-   3.  A third state when both output transistors in the totem-pole are OFF. This third state provides an open circuit or high-impedance state which allows a direct wire connection of many outputs to a common line called the bus.

### CMOS Outputs
Like TTL, the CMOS logic offers three types of outputs. These are push-pull (totem-pole in TTL), open drain (open collector in TTL), and tristate outputs. For example, the 74HC00 contains four independent 2-input NAND gates and includes push-pull output. The 74HC03 also contains four independent 2-input NAND gates, but has open drain outputs. The 74HC03 requires a pull-up resistor for each gate. The 74HC125 contains four independent tri-state buffers in a single chip. Note that CMOS technology is normally used in designing microcontrollers.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_60_0.png)

## 3.2.2 Simple I/O Devices

A simple input device such as a DIP switch can be connected to a microcontroller's I/O port as shown in Figure 3.12. The figure shows a switch circuit that can be used as a single bit input into an I/O port. When the DIP switch is open, $V_{\mathrm{IN}}$ is HIGH. When the switch is closed, $V_{\mathrm{IN}}$ is LOW. $V_{\mathrm{IN}}$ can be used as an input bit for performing laboratory experiments. Note that unlike TTL, a $1 \mathrm{k} \Omega$ resistor is connected between the switch and the input of the MOS gate. This provides protection against static discharge.

For performing simple I/O experiments using programmed I/O, light-emitting diodes (LEDs) and seven-segment displays can be used as output devices. An LED is typically driven by low voltage and low current, which makes it a very attractive device for use with microcontrollers.

Table 3.5 provides the current and voltage requirements for red, yellow, and green LEDs. Basically, an LED will be ON, generating light when its cathode is sufficiently negative with respect to its anode. A microcontroller can therefore light an LED either by grounding the cathode (if the anode is tied to $+5 \mathrm{~V}$ ) or by applying $+5 \mathrm{~V}$ to the anode (if the cathode is grounded) through an appropriate resistor value. A typical hardware interface between a microcontroller and an LED is depicted in Figure 3.13.

A typical microcontroller such as the PIC18F outputs adequate current to turn an LED ON or OFF. In Figure 3.13 (a), a '1' from the microcontroller will turn the LED ON while a '0' will turn it OFF. In Figure 3.13 (b) on the other hand, a '0' from the microcontroller will turn the LED ON while a '1' will turn it OFF.

From Table 3.5, a red LED requires $10 \mathrm{~mA}$ current at $1.7 \mathrm{~V}$. In Figure 3.13 (a), a HIGH at the microcontroller output will turn the LED ON. This will allow a path of current to flow from the $+5 \mathrm{~V}$ source through R and the LED to the ground. In Figure 3.13 (b), a LOW at the microcontroller output will turn the LED ON. This will allow a path of current to flow from the $+5 \mathrm{~V}$ source through R and the LED to the ground (microcontroller I/O port). The appropriate value of R needs to be calculated to satisfy the voltage and current requirements of the LED. The value of R can be calculated as follows:

$R=\frac{5-1.7}{10 \mathrm{~mA}}=330 \Omega$

Therefore, the interface design is complete, and a value of $\mathrm{R}=330 \Omega$ is required. A seven-segment display can be used with programmed I/O to display, for example, decimal numbers from 0 to 9. The name seven segment is based on the fact that there are seven LEDs, one in each segment of the display. Figure 3.14 shows a typical seven-segment display. In the figure, each segment contains an LED. All decimal numbers from 0 through 9 can be displayed by turning the appropriate segment ON or OFF. For example, a '0' can be displayed by turning the LED in segment g OFF and turning the other six LEDs in segments a through f ON. There are two types of seven-segment displays: [OCR missing text likely regarding common-cathode] send a HIGH to light a segment and a LOW to turn it off. In a common-anode configuration, on the other hand, the microcontroller sends a LOW to light a segment and a HIGH to turn it off.

Seven-segment displays can be interfaced to typical microcontrollers using programmed I/O. BCD to seven-segment code converter chips such as 7447 or 7448 can be replaced by a lookup table. This table can be stored in a microcontroller's memory. An assembly language program can be written to read the appropriate code for a BCD digit stored in this table. This data can be outputted to display the BCD digit on a seven-segment display connected to an I/O port of the microcontroller. Programs to accomplish this were written in PIC18F assembly and C languages in Chapter 8.

## 3.2.3 Programmed I/O

A microcontroller communicates with an external device via one or more registers called I/O ports using programmed I/O. Each bit in the port can be configured individually as either input or output. Each port can be configured as an input or output port by another register usually called the Data Direction Register (DDR). The port contains the actual input or output data. The data-direction register is an output register and can be used to configure the bits in the port as inputs or outputs.

Each bit in the port can be set up as an input or output, normally by writing a 0 or a 1 in the corresponding bit of the DDR. The PIC18F microcontroller makes an I/O port bit an input by writing a '1' in the corresponding bit in DDR. On the other hand, writing a '0' in a particular bit in DDR will configure the corresponding bit in the port as an output.

For example, if an 8-bit DDR in the PIC18F contains 0xCB (CB Hex), the corresponding port is defined as shown in Figure 3.15. In this example, because 0xCB (1100 1011) is stored in the data-direction register, bits 0, 1, 3, 6, and 7 of the port are set

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_62_0.png)

FIGURE 3.13 Interfacing LED to PIC18F

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_62_1.png)

FIGURE 3.14 A seven-segment display

**FIGURE 3.12** Typical switch for a microcontroller's input.

**TABLE 3.5** Current and Voltage Requirements of LEDs

| LEDs | Red | Yellow | Green |
| :--- | :--- | :--- | :--- |
| Current | $10 \mathrm{~mA}$ | $10 \mathrm{~mA}$ | $20 \mathrm{~mA}$ |
| Voltage | $1.7 \mathrm{~V}$ | $2.2 \mathrm{~V}$ | $2.4 \mathrm{~V}$ |

