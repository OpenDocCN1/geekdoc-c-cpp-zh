that requires the use of operating system commands to transfer back and forth between the word processor and the compiler. Many C++ programming environments include debugger programs, which are useful in identifying errors in a program. Debugger programs allow us to see values stored in variables at different points in a program and to step through the program line by line.

As we present new statements in C++, we will also point out common errors associated with the statements or useful techniques for locating errors associated with the statements. The debugging aids will be summarized at the end of each chapter.

# 1.4 Data Representation and Storage

Recall that the design of the Analytical Engine's storage unit consisted of an indefinite number of columns of discs, each disc inscribed with the 10 decimal digits (0–9). By arranging the the discs of one column, a decimal number could be stored.

A modern digital computer follows a similar design except information is represented in base 2, or binary, rather than base 10. The base two number system has only two binary digits, 0 and 1, so a binary digit can be represented by one bit in a digital computer. The value of the bit at any given time can be either 0 or 1. In hardware terms, the bit is said to be off, or low, if it has a value of 0 or on, or high, if it has a value of 1.

Binary numbers can be stored in memory as a sequence of bits, called a word. The right most bit of a word represent the one's position, the next bit represents the two's position, the next bit represents the four's position, and the left most bit represents the 2^(n-1) position where n is the number of bits. Each additional bit in a word increases the word size by a power of 2, and doubles the range of values that can be represented. The number of words available in memory is referred to as the memory space, or address space.

Figure 1.4 provides a diagram of memory that has an address space of 8 (2^3) and a word size of 16 (2^4). The binary value stored at address 000 is 0001010110111010_2 = 2781_10. It is important to note that the word size determines the range of values that can be stored in one word of memory or the address space determines the number of words that can be stored. The theoretical Analytical Engine has a word size defined by the number of discs on a column and a memory space defined by the number of columns.

The C++ programming language has built-in data types for representing integer values, floating point values, characters, and boolean values. Each built-in data type has a pre-determined size measured in bytes, where a byte is a sequence of 8 bits. Type declaration statements are required to define identifiers and allocate memory. When an identifier

| Address | Sixteen Bit Word |
|---|---|
| 000 | 0000101011011101 |
| 001 | 0101000010010000 |
| 010 | 0001011010010100 |
| 011 | 0110110100101011 |
| 100 | 0010110100001000 |
| 101 | 0001000000010000 |
| 110 | 0111111111111111 |
| 111 | 0000101010010110 |

Figure 1.4 Memory Diagram: Address Space = 8, Word Size = 16