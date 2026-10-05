# # Appendix E

# # Bitwise Operators

In addition to the common arithmetic operators introduced in Chapter 4, C++ provides a few other special-purpose arithmetic operators. These special operators allow programmers to examine or manipulate the individual bits that make up data values. They are known as the bitwise operators. These operators consist of &, |, ^, ~, and <<. Applications programmers generally do not need to use bitwise operators very often, but bit manipulation is essential in many systems programming tasks.

Consider a typical system which uses 32-bit integers. An integer is a two's complement binary number (see Section D.1) containing 32 bits. The bit positions are usually numbered right to left, starting with zero. Figure E.1 shows how the individual bit positions are often numbered.

![](bbox=[0.216, 0.53, 0.827, 0.574])

Figure E.1: The bit positions of a 32-bit C++ integer

The bitwise and, &, takes two integer subexpressions and computes an integer result. The expression e1 & e2 is evaluated as follows:

+   - If bit 0 in both e_1 and e_2 is 1, then bit 0 in the result is 1; otherwise, bit 0 in the result is 0.
- If bit 1 in both e_1 and e_2 is 1, then bit 1 in the result is 1; otherwise, bit 1 in the result is 0.
- If bit 2 in both e_1 and e_2 is 1, then bit 2 in the result is 1; otherwise, bit 2 in the result is 0.

:

If bit 31 in both e_1 and e_2 is 1, then bit 31 in the result is 1; otherwise, bit 31 in the result is 0.

```
13  = 00000000000000000000000000001101
& 14 = 00000000000000000000000000001110
12  = 00000000000000000000000000001100
```