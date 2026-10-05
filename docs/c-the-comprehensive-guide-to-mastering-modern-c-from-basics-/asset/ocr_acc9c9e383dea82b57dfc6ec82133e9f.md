individual values as positions in a 256 number system—that is, $7 \cdot 256^3 + 91 \cdot 256^2 + 205 \cdot 256^1 \cdot 256^0$.

The values of bytes are rarely written as decimal numbers. It is very common to write them as hexadecimal numbers—that is, 0x07, 0x5b, 0xcd, and 0x15. This means each byte has exactly two letters (plus the 0x prefix). If you add them together, you get an eight-character hexadecimal number: 0x075bcd15 or, without a leading zero, 0x75bcd15.

With this notation, you can now represent a densely packed sequence of int values in memory (Figure 4.2).

![](bbox=[0.333, 0.319, 0.703, 0.461])

Figure 4.2 Data in memory (big-endian).

The two decimal numbers 123456789 and 44788868 at the beginning are stored directly next to each other. The content of the memory cells is shown in hexadecimal numbers.

The figure contains further data for illustration purposes. The hexadecimal byte sequence 0xe89a is interpreted as 59546 for a uint16_t (e.g., unsigned short). If the byte sequence is read with int16_t (e.g., short), this corresponds to -5990. The C string "Manual" has a terminating \0 byte. Which letters mean hexadecimal byte is terminating in the ASCII standard. Finally, I have the decimal floating-point number 45.45 as *double* and *float*, for which you see the hexadecimal representations.

# Memory Alignment

It is not coincidental that the data elements in the figure are always stored such that their first byte is at an address divisible by four. This is called memory alignment. Four bytes correspond to a 32-bit alignment. Most modern machines work faster when this is