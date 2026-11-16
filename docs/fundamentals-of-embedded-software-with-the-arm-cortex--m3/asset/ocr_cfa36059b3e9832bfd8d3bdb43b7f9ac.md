Trying to fix the problem in C by casting the product to a 32-bit value before dividing will not work because it simply extends an incorrect 16-bit product to an equivalent incorrect 32-bit representation. The only solution in C is to cast the operands before the multiplication.

It gets even more interesting if the variables are 32-bit integers containing large values like 10^6. Although casting them into 64-bit integers before multiplying will work, there is no 64 x 64 bit multiply instruction, so the compiler is forced to generate code that calls a library function to do the multiplication. Also note that although you could code in assembly and use the SMULL instruction to produce the 64-bit product from two 32-bit operands, there is no divide instruction that can use a 64-bit dividend.

With that background, now think about trying to write software in C to multiply two 16.16 fixed-point integers x and y to produce a 16.16 fixed-point, z. Although the operands and product are all 32-bit values, you must calculate a 64-bit product because the 16.16 fixed product lies in the middle of the 64-bit integer product. Thus, the only way to do this efficiently is in assembly:

```
LDR R0, x ;R0 ← x (a 16.16 fixed-point real)
LDR R1, y ;R1 ← y (a 16.16 fixed-point real)
SMULL R0,R1,R0,R1 ;R0,R1 ← 64-bit integer product
LSLR R0,R0,#16 ; keep 16 MSBs of least significant half
ORR R0,R0,R1,LSL#16 ;and 16 LSBs f the most significant half
STR R0, z
```

# PROBLEMS

+   1. If register SP contains 12348₁₀ and then a “PUSH {R1}” instruction is executed, what value will be left in register SP?
+   (a) 12347
+   (b) 12346
+   (c) 12345
+   (d) 12344

+   2. Suppose that you have three 32-bit integers named x, y, and z. Give an appropriate sequence of ARM Cortex-M3 assembly language instructions required to implement the assignment statement z = x / y, assuming that the integers are:
+   (a) unsigned
+   (b) signed

+   3. Which of the following registers would not be used to hold the subscript of array when accessing the array element? (Circle all that apply.)
+   (a) R11
+   (b) R12
+   (c) R13
+   (d) R14
+   (e) R15