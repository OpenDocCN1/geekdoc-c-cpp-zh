command, the internal address counter will point to the address location following the one that was just written. Page write operations are limited to writing bytes within a single physical page (64 bytes), regardless of the number of bytes being written. Physical page boundaries start at addresses that are integer multiples of the page buffer size and end at addresses that are integer multiples of page size -1. If a page write command attempts to write across a physical page boundary, the result is the data wraps around to the beginning of the current page (overwriting data previously stored there), instead of being written to the next page. It is, therefore, necessary for the application software to prevent page write operations that would attempt to cross a page boundary (e.g. when writing long strings care should be taken when crossing a page boundary). Some of the page boundaries in bytes are:

+   Page 1: 0 – 63
+   Page 2: 64 – 127
+   Page 3: 128 – 191
+   Page 4: 192 – 255
+   Page 5: 256......

Notice the data sent to the EEPROM is stored in a temporary buffer since a whole page consisting of 64 bytes is refreshed after every write operation. It is therefore important to detect when a write operation has been successfully completed.

![](bbox=[0.12, 0.62, 0.95, 0.75])

# Memory read operation

Memory read operations are slightly more complex. There are 3 types of reads: current address, random, and sequential. Random read mode is probably the most commonly used mode where the master can randomly access any memory location.

As an example, assume we want to read the byte at memory location 0x0250 (where 0x25 was stored in Figure 7.11). Figure 7.12 shows the read steps in detail. To perform Random Read, the memory address must be sent first. This is done by I2C sending the memory address to the 24LC256 as part of a write operation (R/W bit set to '0'). Once the memory address is sent, the master generates a START condition following the ACK. This terminates the write operation, but not before the internal address counter is set. The master then issues the slave address again, but with the R/W bit set to a 1. The 24LC256 will then issue an ACK and transmit the 8-bit data word. The master will not acknowledge the transfer, though it generates a STOP condition, which causes the EEPROM to discontinue transmission. After a random read command, the internal address counter will point to the address location following the one that was just read.