![](bbox=[0.143, 0.1, 0.8, 0.299])

**Figure 4.2** Data in memory (big-endian).

The two decimal numbers 123456789 and 447888868 at the beginning are stored directly next to each other. The content of the memory cells is shown in hexadecimal numbers.

The figure contains further data for illustration purposes. The hexadecimal byte sequence 0xe89a is interpreted as 59546 for a uint16_t (e.g., unsigned short). If the byte sequence is read with an int16_t (e.g., short), this corresponds to -5990. The C string "Manual" has a starting \0 byte. Which letters mean which hexadecimal byte is defined in the ASCII standard. Finally, I have stored the decimal floating-point number 45.45 as double and float, for which you see the hexadecimal representations.

# ### Memory Alignment

It is not entirely coincidental that the data elements in the figure are always stored such that their first byte is at an address divisible by four. This is called *memory alignment*. Four bytes correspond to a 32-bit alignment. Most modern machines work faster when this is the case. To achieve optimum speed, data is not packed close together if necessary, but shifted with “empty” bytes in between. In the example, this is the case at 59546 and -5990: the addresses 0c and 0d in between do not contain any meaningful data.

Some machines cannot even cope if the data of certain data types is not stored with the correct alignment. In this case, the data must first be copied in a time-consuming process when reading. In addition to 32-bit alignment, there is also 16-bit, 64-bit, and even 128-bit alignment. No alignment means that the start position does not matter; this corresponds to 8-bit alignment and occurs in practice as well.

You do not normally have to worry about memory alignment; the compiler does this for you.