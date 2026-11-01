2. X - RX format - the 32 bits from the word in memory addressed by the second operand are exclusive or'ed with the bits in the register designated as the first operand and the result is placed in the first operand.

3. XI - SI format - the 8 bits in the immediate operand are exclusive or'ed with the bits of the byte in memory designated as the first operand and the resulting byte replaces the byte in memory.

4. XC - SS format - from 1 to 256 bytes beginning at the address specified by the second operand are exclusive or'ed with the corresponding bytes beginning at the address specified by the first operand with the resulting bytes replacing the bytes from the first operand.

Table 36 shows all versions of the Exclusive Or. Versions added in later models are shaded.

| OpCode | Type | 1st Operand | 2nd Operand | Result | Operation |
|---|---|---|---|---|---|
| XR | RR | 32 bit register | 32 bit register | 32 bit register | |
| X | RX | 32 bit register | 32 bit memory | 32 bit register | |
| XI | SI | 8 bit memory | 8 bit immediate | 8 bit memory | |
| XC | SS | Memory String | Memory String | Memory String | 2nd operand is bitwise XORed with 1st operand and result remains in 1st operand. In NIH, NILH, NILH, NIL, only 16 bits of the 1st operand altered. |
| XGR | RRE | 64 bit register | 64 bit memory | 64 bit register | |
| XY | RXY | 32 bit register | 32 bit memory | 32 bit register | |
| XG | RXY | 64 bit register | 64 bit memory | 64 bit register | |
| XIY | SIY | 8 bit memory | 8 bit immediate | 8 bit memory | |
| XIHH | RI | 16 bit register | 16 bit immediate | 16 bit register | |
| XIHL | RI | 16 bit register | 16 bit immediate | 16 bit register | |
| XILH | RI | 16 bit register | 16 bit immediate | 16 bit register | |
| XILL | RI | 16 bit register | 16 bit immediate | 16 bit register | |

Table 36 XOR Instructions