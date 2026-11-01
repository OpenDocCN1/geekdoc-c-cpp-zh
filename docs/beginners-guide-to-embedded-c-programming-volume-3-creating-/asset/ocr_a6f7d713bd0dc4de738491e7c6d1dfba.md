![](bbox=[0.18, 0.08, 0.85, 0.2])

# Write Command Sequence

![](bbox=[0.18, 0.26, 0.85, 0.36])

# Read Command Sequence

# Figure 2-2: I²C Data Line Message Format

The signal in Figure 2-2 shows a write and a read sequence for communicating with an external EEPROM device. I will use the Microchip 24LC01B EEPROM part to demonstrate how to store and read back data in an external EEPROM using I²C as the communication protocol.

The control byte is a 7-bit wide value, with the eighth bit being either zero for a write or one for a read operation. As you can see, the read sequence requires two control bytes, while a write only requires one. This is because a read operation requires the master to first write the memory-address byte to the EEPROM so it can locate the data and then read the data from the EEPROM. During the write operation, the master sends both the address and data bytes to the EEPROM, therefore only one write-control byte is sent. Notice also that Figure 2-2 shows an optional plural Data Byte(s). This is because you can send or receive a string of bytes from one read or write control-byte command.

The ACK bits are the acknowledge bits. The slave pulls the data line low while the master is still pulsing the clock line. The master looks for that ACK bit before sending the next command byte. This is the only way the slave can tell the master it has successfully received the byte of information.

I²C is not as fast as other communication techniques such as Serial Peripheral Interface (SPI) which I covered in Volume 2, but it’s still fast. Typical clock speeds of 10 khz or 100 khz are common. A high-speed mode runs at 400 khz. You have to make sure your slave parts can handle the speed of the master clock.