| Bit 3-0 | SSPM<3:0>: Synchronous Serial Port Mode Select bits |
|---|---|
| 0000 | SPI Slave mode, clock = Fosc/4 |
| 0001 | SPI Master mode, clock = Fosc/16 |
| 0010 | SPI Master mode, clock = Fosc/64 |
| 0011 | SPI Master mode, clock = TMR2 output/2 |
| 0100 | SPI Slave mode, clock = SCK pin, SS pin control enabled |
| 0101 | SPI Slave mode, clock = SCK pin, SS pin control disabled, SS can be used as I/O pin |
| 0110 | I²C Slave mode, 7-bit address |
| 0111 | I²C Slave mode, 10-bit address |
| 1000 | I²C Master mode, clock = Fosc / (4 * (SSPADD+1)) |
| 1001 | Load function |
| 1010 | Reserved |
| 1011 | I²C Firmware controlled Master mode (Slave idle) |
| 1100 | Reserved |
| 1101 | Reserved |
| 1110 | I²C Slave mode, 7-bit address with Start and Stop bit interrupts enabled |
| 1111 | I²C Slave mode, 10-bit address with Start and Stop bit interrupts enabled |

The bit 4 is not used in Master mode so we leave that cleared or zero. We want to enable the clock so we set the SSPEN bit to 1 which is bit 5.

| Bit 5 | SSPEN: Synchronous Serial Port Enable bit |
|---|---|
|  | In both modes, when enabled, these pins must be properly configured as input or output |
| In SPI mode |  |
| 1 | Enables serial port and configures SCK, SDO, SDI and SS as the source of the serial port pins |
| 0 | Disables serial port and configures these pins as I/O port pins |
| In I²C mode |  |
| 1 | Enables the serial port and configures the SDA and SCL pins as the source of the serial port pins |
| 0 | Disables serial port and configures these pins as I/O port pins |

| Bit 4 | CKP: Clock Polarity Select bit |
|---|---|
| In SPI mode |  |
| 1 | Idle state for clock is a high level |
| 0 | Idle state for clock is a low level |
| In I²C Slave mode |  |
|  | SCK release control |
| 1 | Enable clock |
| 0 | Holds clock low (clock stretch). (Used to ensure data setup time.) |
| In I²C Master mode |  |
|  | Unused in this mode |

Bit 6 and 7 are status bits so we just leave them set to zero for the setup. Add this all up and you get a hex value of 0x38. Therefore in our software we will set the SSPCON register to 0x38.

The next register is the SSPCON2 register which has many status bits and a few setup bits. We initialize all of it to zeros as we will modify or read these later in the process of sending data.