Since C++20, the numbers listed under "Bits" apply as the minimum widths of the implementation for the data types specified in the "Minimum For..." column. However, you don't have to get used to this, as all implementations actually adhered to these widths even before standardization. However, you will probably still find people for a long time who believe that C++ does not specify minimum widths except for char. Now you can shine with new knowledge.

A note on the names of the integer types: officially, the types are called int, unsigned int, long int, and long long int. I myself abbreviate unsigned int to unsigned, but you will often see it written out in full. With long and long int, the written-out version with int behind it is rarely used.

| Bits | Unsigned | Signed |
|---|---|---||
| 8 | 0 ... 255 | -128 ... 127 |
| 16 | 0 ... 65 535 | -32 768 ... 32 767 |
| 32 | 0 ... 4 294 967 295 | -2 147 483 648 ... 2 147 483 647 |
| 64 | 0 ... 18 446 744 073 551 615 | -9 223 372 036 854 775 808 ... 9 223 372 036 854 775 807 |

Table 4.4 Numerical ranges.

# Physical Representation of Integers

Have you noticed that the number of bits that can be integers wide is divisible by eight? I'm probably not telling you anything new by saying that in most computer systems, eight bits make up one byte (there are exceptions). In C++, a byte is the smallest address data unit. A byte in memory has an address x; the byte next to it has address x+1.

On a typical system, an unsigned int has 32 bits—that is, four bytes, as you can see in Table 4.3. The unit that is particularly advantageous on