the default. An int (whether signed or unsigned) is what your system handles most naturally and can usually calculate the fastest.

You can perform arithmetic calculations with the integer types—that is, multiplication and the like. However, you are already reaching the limits of the data type with basic arithmetic operations, because logically an unsigned int cannot take on a negative value. And both the signed and unsigned variants have a limit for large numbers.

To understand what actually happens when calculating with int types and relatives, you only need to know that the computer works in the binary system. This is nothing other than the decimal system that you are used to, except that each digit cannot be 0 to 9, but 0 or 1—one of two possible values (hence the bi in binary). In Section 4.3, I discuss this in the “Binary System”.

The individual positions that can be 0 or 1 are called bits. How many bits fit into a variable of an integer depends on your system. The standard says that char is the smallest and most long is the largest type, with short, int, and long, in order. On today's machines, char is eight bits and long long is 64 bits. Table 4.3 gives examples of two common systems today. The Windows column applies to all 32-bit and 64-bit Windows, as well as 32-bit Linux.

| Bits | Linux, 64-Bit | Windows | Minimum For... |
|---|---|---|---|
| 8 | char | char | char |
| 16 | short | short | short, int |
| 32 | int | int, long | long |
| 64 | long, long long | long long | long long |

**Table 4.3** Bit widths of two architectures and the minimums as examples.

If an unsigned int has 32 bits, then the largest number that data type can represent is 1 · 2³¹ + 1 · 2³⁰ + ... + 1 · 2¹ + 1 · 2⁰ = 2³²-1, which corresponds to just over 4 billion. This is shown in Table 4.4. You must use your program to ensure that an expression of type int never assumes a larger value.