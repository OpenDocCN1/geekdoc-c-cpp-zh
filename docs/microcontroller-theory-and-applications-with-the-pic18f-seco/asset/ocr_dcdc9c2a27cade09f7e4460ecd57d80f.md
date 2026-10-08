# 6.3.2 Arithmetic Instructions

The PIC18F arithmetic instructions allow:

+   * 8-bit addition and subtraction
    * 8-bit by 8-bit unsigned multiplication. The PIC18F does not provide any signed
        multiplication and division (Signed and Unsigned) instructions.
    * Negate instruction
    * Decrement and Increment Instructions
    * BCD Adjust (BCD Correction)

As mentioned before, typical microcontrollers utilize common hardware to perform addition and subtraction operations for both unsigned and signed numbers. The instruction set of microcontrollers include the same ADD and SUBTRACT instructions for both unsigned and signed numbers. The interpretations of unsigned and signed ADD and SUBTRACT operations are performed by the programmer.

Unsigned and signed multiplication and division operations can be performed using various algorithms. Typical 32-bit microprocessors such as the Pentium contain separate instructions for performing these multiplication and division operations. The PIC18F provides only unsigned multiplication instruction. The other multiplication and division instructions can be obtained by writing PIC18F assembly language programs using appropriate algorithms. This is shown in Chapter 7.

The PIC18F arithmetic instructions are summarized in Table 6.6. Next, we will explain the arithmetic instructions using the access bank and specifying F or W in place of 'd'.

+   * All instructions in Table 6.6 are executed in one cycle.
* The size of each instruction is one word.
* a = 0 means that the data register is located in the access bank while a = 1 means that
    the contents of BSR specify the address of the bank.
* For destination: d = 0 means that the destination is WREG while d = 1 means that the
    destination is file register. As mentioned before, W or F instead of 0 or 1 will be used in
    this book for better clarity.
* The PIC18F does not provide any multiplication (signed) and division (signed and
    unsigned) instructions.

**Addition and Subtraction Instructions** The PIC18F addition and subtraction instructions are illustrated by means of numerical examples in the following. All flags are affected. Assume signed numbers.

**ADDLW data8 (ADDLW 0x02) instruction adds the 8-bit contents of WREG with 8-bit immediate data, and stores the result in WREG. For example, Consider ADDLW 0x02.**

Prior to execution of ADDLW 0x02: [WREG] = 12H.
After execution of ADDLW 0x02: [WREG] = 12H + 02H = 14H.
The flags are affected based on the result as follows:

```
Previous carry → 0000 010 Intermediated Carries
[WREG]= 12H = 0001 0010
Add immediate data, 02H = 0000 0010
-----------------
final carry → 0 0001 0100 = 14H
```