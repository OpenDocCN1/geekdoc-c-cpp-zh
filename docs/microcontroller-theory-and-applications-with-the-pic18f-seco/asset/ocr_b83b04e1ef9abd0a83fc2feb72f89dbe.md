+   6.8 Write a PIC18F assembly language program that is equivalent to the following C code:
```c
if (x > 0)
p = 0;
else
p = 2p;
```

+   6.9 What is the content of WREG after execution of the following PIC18F instruction sequence?
```asm
MOVLW 0x33
ADDLW 0x77
DAW
```

+   6.10 Find two ways to clear [WREG] to 0 using:
(a) a single PIC18F instruction
(b) two PIC18F instructions

+   6.11 Using a single PIC18F instruction, clear the carry flag without changing the contents of any data registers, WREG, or other status flags.

+   6.12 Write the machine code for the following PIC18F instruction sequence:
```asm
ORG 0x200
HERE BRA HERE
```

+   6.13 Write a PIC18F assembly language program at address 0x100 to add two 8-bit numbers (N1 and N2). Data register 0x20 contains N1. The low four bits of N2 are stored in the upper nibble of data register 0x21 while the high four bits of N2 are stored in the lower nibble of data register 0x21. Store result in data register 0x30.

+   6.14 Write a PIC18F assembly language program at address 0x100 to add two 24-bit data items in memory as shown in Figure P6.14. Store the result in data memory location addressed by 0x50. Do not use a loop. The operation with sample data is given by
```
F1 91 B5
PLUS 07 A2 04
-------------
F9 33 B9
```

![](bbox=[0.3, 0.7, 0.75, 0.9])

FIGURE P6.14