next depends on whether the command is a read or write operation; if read the EEPROM will output data to Master to read, if it is a write operation the Master will output data from the EEPROM to store. Most EEPROM are not typically high speed devices and a memory write cycle may take several milliseconds. The API handles this.

![](bbox=[0.22, 0.25, 0.78, 0.78])

+5V external power source or tap off of TP1

Figure 8-4 Schematic