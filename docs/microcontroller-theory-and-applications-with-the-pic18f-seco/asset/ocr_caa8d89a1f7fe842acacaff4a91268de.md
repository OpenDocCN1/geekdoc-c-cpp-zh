peripherals. They are intended for data transmission from a master to or from one or more slave devices over short distances.

The main purpose of the SPI is to replace parallel interfaces by avoiding routing of parallel buses in a PCB (Printed Circuit Board). The SPI protocol is based on the principle that a bit from an 8-bit shift register can be shifted out on a single pin and a bit can be shifted into another pin. SPI protocol can also be used for data transfer between the CPU (master) and slave devices such as flash memory and ADC.

The original purpose of the I²C protocol was to easily interface a CPU to peripheral chips in a TV. Peripheral devices in an embedded system are typically connected to a microcontroller using memory-mapped I/O. This requires a lot of wiring on the PCB (Printed Circuit Board). In order to refrain from using microcontroller pins and avoid additional circuits, I²C protocol can be used to interface the microcontroller to all the peripherals. This will also reduce wiring and thus, implementation cost.

SPI uses four wires; one for clock, one for data out, one for data in, and one for SS or CS (Slave Select or Chip Select to enable a slave device). I²C, on the other hand, uses two wires; one for clock and one for data. Data transfer using SPI is faster (up to 25MHz) while data transfer using I²C is slower (100KHz to 400KHz). As far as the software is concerned, SPI and I²C perform communication in a similar manner. In both protocols, the master generates the clock and data read or written at the rising or falling edges of the clock. However, SPI protocol is based on a single master and one or more slaves while I²C protocol is based on multi-master with a single or multiple slaves.

Both polled and interrupt I/O can be used for data transfer using SPI and I²C modes. However, polled I/O will be used in this discussion to illustrate the basic concepts.

# 11.4 PIC18F Serial I/O

The PIC18F4321 contains an on-chip Master Synchronous Serial Port (MSSP) module which is a serial interface, useful for communicating with other peripheral or microcontroller devices. The MSSP module can operate in either SPI or I²C mode. We will cover the PIC18F SPI and I²C modes in this section.

# 11.4.1 PIC18F SPI mode

The PIC18F SPI primarily uses four pins of the PIC18F4321. They are SCK (Serial Clock), SDI (Serial Data Input), SDO (Serial Data Output) and SS (Slave Select). The SS pin is provided for applications requiring multiple slave devices. The SS pin may not be used for a single slave in the system. In summary, SCK, SDI, SDO, and SS pins are provided on the PIC18F to support SPI.

Figure 11.4 shows a block diagram interfacing a PIC18F master with a single PIC18F slave. Since SPI is a master/slave protocol, the master is the only device which will control the clock (SCK). Data transfers between the master and the slave are controlled by the SCK clock. This means that sending and reading of data are controlled by SCK.

SDI carries the data into the Master while SDO carries the data sent out from the Master. SS is similar to a chip select signal. SS must be used when more than one slave is present. However, the pin can be disabled via programming for a single slave. This will be illustrated using an example later in this section. For simplicity, a master with a single slave will be covered in this section. Coverage of a master with multiple slaves is beyond the scope of this book.

Figure 11.5 shows a simplified diagram of SPI Master/Slave connection between