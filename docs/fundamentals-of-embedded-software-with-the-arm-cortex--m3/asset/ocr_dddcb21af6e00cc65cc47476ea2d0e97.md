32-bit words of 4 bytes each, with each word beginning on a mod-4 address as shown below.

| Address 15 | Address 14 | Address 13 | Address 12 |
| Address 11 | Address 10 | Address 9 | Address 8 |
| Address 7 | Address 6 | Address 5 | Address 4 |
| Address 3 | Address 2 | Address 1 | Address 0 |

A 32-bit word of data can be stored within *any* contiguous set of 4 bytes. For example, the word starting at address 4 is highlighted below:

| Address 15 | Address 14 | Address 13 | Address 12 |
| Address 11 | Address 10 | Address 9 | Address 8 |
| Address 7 (MSByte) | Address 6 | Address 5 | Address 4 (LSByte) |
| Address 3 | Address 2 | Address 1 | Address 0 |

However, we could just as easily store a word starting at address 6:

| Address 15 | Address 14 | Address 13 | Address 12 |
| Address 11 | Address 10 | Address 9 (MSByte) | Address 8 |
| Address 7 | Address 6 (LSByte) | Address 5 | Address 4 |
| Address 3 | Address 2 | Address 1 | Address 0 |

The difference is that the word at address 4 can be read from memory in a single memory cycle, but because the word at address 6 is split between two “physical” words, two memory read cycles are required to retrieve all 32 bits. The first read cycle would retrieve 4 bytes from addresses 4 through 7; of these, the bytes from addresses 4 and 5 are discarded, and those from addresses 6 and 7 are moved to the far right:

| | | Address 7 | Address 6 (LSByte) |

The second read cycle retrieves 4 bytes from addresses 8 through 11; the bytes from addresses 10 and 11 are discarded, and those from addresses 8 and 9 are moved to the far left:

| Address 9 (MSByte) | Address 8 | | |

Finally, the two halves are combined to form the desired 32-bit operand:

| Address 9 (MSByte) | Address 8 | Address 7 | Address 6 (LSByte) |