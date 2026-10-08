
![](img/5e76fd429fabd2b62e16a7bfd8cf546f_359_0.png)

### SSPSTAT: MSSP Status Register (I²C Mode)

**bit 7** **SMP**: Slew Rate Control bit
*In Master or Slave mode:*
1 = Slew rate control disabled for Standard Speed mode (100 kHz and 1 MHz)
0 = Slew rate control enabled for High-Speed mode (400 kHz)

**bit 6** **SCL**: SMBus Select bit
*In Master or Slave mode:*
1 = Enable SMBus specific inputs
0 = Disable SMBus specific inputs

**bit 5** **D/A**: Data/Address bit
*In Master mode:*
Reserved.
*In Slave mode:*
1 = Indicates that the last byte received or transmitted was data
0 = Indicates that the last byte received or transmitted was address

**bit 4** **P**: Stop bit
1 = Indicates that a Stop bit has been detected last
0 = Stop bit was not detected last
**Note:** This bit is cleared on Reset and when SSPEN is cleared.

**bit 3** **S**: Start bit
1 = Indicates that a Start bit has been detected last
0 = Start bit was not detected last
**Note:** This bit is cleared on Reset and when SSPEN is cleared.

**bit 2** **R/W**: Read/Write Information bit (I²C mode only)
*In Slave mode:*
1 = Read
0 = Write
**Note:** This bit holds the R/W bit information following the last address match. This bit is only valid from the address match to the next Start bit, Stop bit or not ACK bit.
*In Master mode:*
1 = Transmit is in progress
0 = Transmit is not in progress
Note: ORing this bit with SEN, RSEN, PEN, RCEN or ACKEN will indicate if the MSSP is in Active mode.

**bit 1** **UA**: Update Address bit (10-bit Slave mode only)
1 = Indicates that the user needs to update the address in the SSPADD register
0 = Address does not need to be updated

**bit 0** **BF**: Buffer Full Status bit
*In Transmit mode:*
1 = SSPBUF is full
0 = SSPBUF is empty
*In Receive mode:*
1 = SSPBUF is full (does not include the ACK and Stop bits)
0 = SSPBUF is empty (does not include the ACK and Stop bits)

# FIGURE 11.12 SSPSTAT: MSSP STATUS REGISTER (I2C MODE)

Enabling the slew rate control can provide additional distance of bus length with appropriate pull-ups. In our case, SMP will be set to one to disable.

### SSPCON1 register (FIGURE 11.13)

The device will be selected as Master or Slave using the SSPCON1 register. This register also enables or disables the MSSP module.

| | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| bit 7 | bit 6 | bit 5 | bit 4 | bit 3 | bit 2 | bit 1 | bit 0 |
| WCOL | SPOV | SSPEN | CKP | SS3 | SS2 | SS1 | SS0 |

**bit 7**

**WCOL: Write Collision Detect bit**

*In Master Transmit mode:*
1 = A write to the SSPBUF register was attempted while the I²C conditions were not valid for transmission to be started (must be cleared in software)
0 = No collision

*In Slave Transmit mode:*
1 = The SSPBUF register is written while it is still transmitting the previous word (must be cleared in software)
0 = No collision

In Receive mode (Master or Slave modes):
This is a "don't care" bit.

**bit 6**

**SPOV: Receive Overflow Indicator bit**

*In Receive mode:*
1 = A byte is received while the SSPBUF register is still holding the previous byte (must be cleared in software)
0 = No overflow

*In Transmit mode:*
This is a "don't care" bit in Transmit mode.

**bit 5**

**SSPEN: Master Synchronous Serial Port Enable bit**

1 = Enables the serial port and configures the SDA and SCL pins as the serial port pins
0 = Disables serial port and configures these pins as I/O port pins

**Note:** When enabled, the SDA and SCL pins must be properly configured as inputs.

**bit 4**

**CKP: SCK Release Control bit**

*In Slave mode:*
1 = Release clock
0 = Holds clock low (clock stretch), used to ensure data setup time

*In Master mode:*
Unused in this mode.

**bits 3-0**

**SS3:SS0: Master Synchronous Serial Port Mode Select bits**

1111 = I²C Slave mode, 10-bit address with Start and Stop bit interrupts enabled
1110 = I²C Slave mode, 7-bit address with Start and Stop bit interrupts enabled
1011 = I²C Firmware Controlled Master mode (SI2C Idle)
1000 = I²C Master mode, clock = Fosc/(4 * (SSPADD + 1))
0111 = I²C Slave mode, 10-bit address
0110 = I²C Slave mode, 7-bit address

# FIGURE 11.13 SSPCON1: MSSP CONTROL REGISTER 1 (I²C MODE)

and releases or holds SCK for the slave.

### SSPCON2 register (FIGURE 11.14)

- Provides acknowledge status bit for the master (received or not received) for the master
- Initiates START or STOP conditions for the master
- Provides clock stretching. Note that I²C devices can slow down communication by clock stretching (that is, by stretching SCL). During an SCL low phase, any I²C device on the bus may additionally hold down SCL clock to prevent it from rising high again, enabling them to slow down the SCL clock or to stop I²C communication for a while. If SEN is enabled (SSPCON2<0>=1), RC3/SCK/SCL will be held low (clock stretch) following each data transfer. The clock must be released by setting bit CKP (SSPCON1<4>).

| | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| bit 7 | bit 6 | bit 5 | bit 4 | bit 3 | bit 2 | bit 1 | bit 0 |
| GCEN | CKSTAT | ACKDT/ADMSK5 | ACKEN/ADMSK4 | RCEN/ADMSK3 | PEN/ADMSK2 | RSEN/ADMSK1 | SEN |

**bit 7** **GCEN**: General Call Enable bit (Slave mode only)
1 = Enable interrupt when a general call address (0000h) is received in the SSPSR
0 = General call address disabled

**bit 6** **CKSTAT**: Acknowledge Status bit (Master Transmit mode only)
1 = Acknowledge was not received from slave
0 = Acknowledge was received from slave

**bit 5** **ACKDT/ADMSK5**: Acknowledge Data bit
In Master Receive mode: 1 = Not Acknowledge, 0 = Acknowledge
**Note:** Value that will be transmitted when the user initiates an Acknowledge sequence at the end of a receive.
In Slave mode: 1 = Address masking of ADD5 enabled, 0 = Address masking of ADD5 disabled

**bit 4** **ACKEN/ADMSK4**: Acknowledge Sequence Enable bit
In Master Receive mode:
1 = Initiate Acknowledge sequence on SDA and SCL pins and transmit ACKDT data bit. Automatically cleared by hardware.
0 = Acknowledge sequence Idle.
In Slave mode:
1 = Address masking of ADD4 enabled
0 = Address masking of ADD4 disabled

**bit 3** **RCEN/ADMSK3**: Receive Enable bit
In Master Receive mode:
1 = Enables Receive mode for I²C
0 = Receive Idle
In Slave mode:
1 = Address masking of ADD3 enabled
0 = Address masking of ADD3 disabled

**bit 2** **PEN/ADMSK2**: Stop Condition Enable bit
In Master mode:
1 = Initiate Stop condition on SDA and SCL pins. Automatically cleared by hardware.
0 = Stop condition Idle
In Slave mode:
1 = Address masking of ADD2 enabled
0 = Address masking of ADD2 disabled

**bit 1** **RSEN/ADMSK1**: Repeated Start Condition Enable bit
In Master mode:
1 = Initiate Repeated Start condition on SDA and SCL pins. Automatically cleared by hardware.
0 = Repeated Start condition Idle
In Slave mode (7-bit Address mode):
1 = Address masking of ADD1 enabled
0 = Address masking of ADD1 disabled
In Slave mode (10-bit Address mode):
1 = Address masking of ADD1 and ADD0 enabled
0 = Address masking of ADD1 and ADD0 disabled

**bit 0** **SEN**: Start Condition Enable/Stretch Enable bit
In Master mode:
1 = Initiate Start condition on SDA and SCL pins. Automatically cleared by hardware.
0 = Start condition Idle
In Slave mode:
1 = Clock stretching is enabled for both slave transmit and slave receive (stretch enabled)
0 = Clock stretching is disabled
Note that I²C devices can slow down communication by clock stretching (that is, by stretching SCL). During an SCL low phase, any I²C device on the bus may additionally hold down SCL clock to prevent it from rising high again, enabling them to slow down the SCL clock or to stop I²C communication for a while.

# FIGURE 11.14 SSPCON2: MSSP CONTROL REGISTER 2 (I²C MODE)

| | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| bit 7 | bit 6 | bit 5 | bit 4 | bit 3 | bit 2 | bit 1 | bit 0 |
| ADD7 | ADD6 | ADD5 | ADD4 | ADD3 | ADD2 | ADD1 | ADD0 |

**bits 7-0** **ADD<7:0>**: MSSP Address bits
**Note 1:** MSSP Address register in I²C Slave mode. MSSP Baud Rate register in I²C Master mode.

# FIGURE 11.15 SSPADD: MSSP ADDRESS REGISTER

### SSPADD register (FIGURE 11.15)

For the slave device, SSPADD = slave address. For the master device, the 8-bit value of SSPADD will determine the clock frequency in the SCK line. This is called Baud rate. The baud rate formula is:
Baud rate = FOSC/(4*(SSPADD +1))
SSPADD = (FOSC/ (4*Baud rate))-1

### Example 11.7

Figure 11.16 shows a block diagram for interfacing two PIC18F4321 in I²C mode. One of the microcontrollers is the master while the other is the slave. The master PIC18F4321 will input four switches via bits 0-3 of **PORTB** (Switch SW0 connected to bit 0 of Port B, Switch SW1 to bit 1, SW2 to bit 2 and SW3 to bit 3), and then transmit the 4-bit data using its SDA pin to the slave's SDA pin. The slave PIC18F4321 will output this data to four LED's (LED0 connected to bit 0 of Port D, LED1 to bit 1, LED 2 to bit 2, and LED 3 to bit 3), and turn them ON or OFF based on the switch inputs. For example, LED0 will be turned ON if SW0 is one (Open) and will be turned OFF if SW0 is zero (closed), LED1 will be turned ON if SW1 is one (Open) and will be turned OFF if SW1 is zero (closed), and so on.

- Write a PIC18F assembly language program at 0x70 for the master PIC18F4321 that will configure PORTB, initialize STKPTR to 5, initialize SSPSTAT and SSPCON1, input switches, and call a subroutine called SERIAL\_WRITE to place this data into its SSPBUF register.
- Also, write a PIC18F assembly language program at 0x100 for the slave PIC18F4321 that will configure PORTD, initialize SSPSTAT and SSPCON1 registers, input data from its SDA pin, place it in the slave's SSPBUF, and then output to the LED's.
- Repeat (a) using C language. The master PIC18F4321 will configure PORTB, initialize SSPSTAT and SSPCON1, input switches, and place this data into its SSPBUF register.
- Also, write a C language program for the slave PIC18F4321 that will configure PORTD, initialize SSPSTAT and SSPCON1 registers, input data from its SDA pin, place it in the slave's SSPBUF, and then output to the LED's.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_362_0.png)

**FIGURE 11.16** Figure for Example 11.7
