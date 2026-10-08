| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SMP | CKE | D/A | P | S | R/W | UA | BF |

SSPSTAT

bit 7 **SMP**: Sample bit
SPI Master mode:
1 = Input data sampled at end of data output time
0 = Input data sampled at middle of data output time
SPI Slave mode:
SMP must be cleared when SPI is used in Slave mode.

bit 6 **CKE**: SPI Clock Select bit
1 = Transmit occurs on transition from active to Idle clock state
0 = Transmit occurs on transition from Idle to active clock state
**Note:** Polarity of clock state is set by the CKP bit (SSPCON1<4>).

bit 5 **D/A**: Data/Address bit
Used in I2C™ mode only.

bit 4 **P**: Stop bit
Used in I2C mode only. This bit is cleared when the MSSP module is disabled, SSPEN is cleared.

bit 3 **S**: Start bit
Used in I2C mode only.

bit 2 **R/W**: Read/Write Information bit
Used in I2C mode only.

bit 1 **UA**: Update Address bit
Used in I2C mode only.

bit 0 **BF**: Buffer Full Status bit (Receive mode only)
1 = Receive complete, SSPBUF is full
0 = Receive not complete, SSPBUF is empty

# FIGURE 11.7 SSPSTAT (MSSP Status Register) in SPI mode
as follows:

+   • SDI is automatically controlled by the SPI module.
• SDO pin is multiplexed with bit 5 of Port C. Hence, in order to configure SDO as an output pin, bit 5 of TRISC must be cleared to 0.
• SCK (Master mode) pin is multiplexed with bit 3 of Port C. Hence, in order to configure SCK as an output pin, bit 3 of TRISC must be cleared to 0.
• SCK (Slave mode) pin must be configured as an output pin. Hence, bit 3 of TRISC must be set to one.

In Figure 11.5, the master PIC18F4321 initiates the data transfer by sending the SCK signal. The master can initiate the data transfer at any time because it controls the SCK. The master determines when the slave will broadcast data by the software protocol. Data is shifted out of both shift registers on their programmed clock edge and latched on the opposite edge of the clock. Both processors should be programmed to the same Clock