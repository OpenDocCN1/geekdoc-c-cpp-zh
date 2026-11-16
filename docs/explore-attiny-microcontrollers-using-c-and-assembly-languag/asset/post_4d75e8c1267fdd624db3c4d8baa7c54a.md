
## 7.3 Subtraction

SUB (Subtract without Carry) subtracts the values from two registers. If the result of the subtraction is negative, the result will be in 2's complement format. An example follows that uses the SUB instruction to subtract two registers with a positive result.

```
test_asm : main.asm - Subtraction with positive result
ldi    r16, 145
ldi    r17, 99
sub    r16, r17    ; R16 = R16 - R17 = 145 - 99 = 46 or 0x2E
```

The SUB instruction in the above example subtracts the value in R17 from the value in R16 and stores the result back in R16. Test the code in the Microchip Studio simulator.

In the following code, a subtraction is done that results in a negative result which is stored in the destination register in 2's complement format.

```
test_asm : main.asm - Subtraction with negative result
ldi    r16, 84
ldi    r17, 199
sub    r16, r17    ; R16 = R16 - R17 = 84 - 199 = -115 or 0x8D
```

In the Microchip Studio debugger, the result of the subtraction from the above code is 0x8D found in R16, with the negative flag set in the status register. When R16 is converted to decimal in the Processor Status window, it does not take into consideration that the number is negative and so treats it as a positive number converting the most significant bit to its weight value instead of treating the number as 2's complement. 0x8D in binary is 0b1000_1101. To convert this number from 2's complement format to its actual value we subtract 1 and then invert:

```
0b1000_1101 - 1 = 0b1000_1100
```

Inverting the bits of the result, we get:

```
0b0111_0011 or 115
```

We know that it is a negative number so its actual value is -115 which is the correct result when 199 is subtracted from 84 as in the example code.

This section has only covered the basic subtraction instruction. AVR microcontrollers have other subtraction instructions shown in Chapter 11 and that can be found in the *Instruction Set Summary* section of the AVR datasheets, and in the *AVR Instruction Set Manual*.

## 7.4 Logic Instructions

Logic operations are similar to arithmetic operations, but are performed on a bit at a time according to the values in a truth table. For this reason they are sometimes referred to as bitwise operations. Each different logical operator has its own truth table that shows the results of its logical operation on various combinations of input bits. Logical operations or instructions operate on the logical levels of bits in a register where 0 is logic level zero and 1 is logic level one. In an 8-bit AVR, logical operations are done on 8-bit registers, effectively operating on 8-bits at the same time. Although the actual logical operation is calculated on a bit-by-bit basis, eight calculations are effectively done at the same time in parallel in an 8-bit AVR or other 8-bit microcontroller. This will become clearer as we look at the logical operations in an AVR, starting with the logical AND operation.

### 7.4.1 Logical AND

A logical AND operation of two bits is shown in the truth table in Figure 7.1. The truth table shows the result of an AND operation on all possible combinations of two bits. A and B in the table are input bits, Z is the output and result of an AND operation between A and B.

| A | B | Z |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

![](img/83ef13a6c66cc7882b2f357e97f451dc_142_0.png)

Figure 7.1: AND Truth Table and Example of Bitwise AND Operation

With two input bits, there are four possible numbers or combinations of bits A and B. If one or both of the input bits are 0, then the output of the AND operation is 0. Only if both inputs are 1 will the output of an AND operation be 1. The AND truth table shows the following AND operations:

```
0 AND 0 = 0
0 AND 1 = 0
1 AND 0 = 0
1 AND 1 = 1
```

At the right of Figure 7.1 is an example of how two 8-bit registers are ANDed together. Each bit in the top register is ANDed with the corresponding bit in the register below it. In effect these are 8 AND operations taking place in parallel. Each bit in the top register represents the A input in the truth table. Each bit in the second from top register represents the B input in the truth table. The bottom register holds the result of the 8 AND operations and each bit represents the Z bit from the truth table. Starting at the right, or bit 0 of the registers, 1 from the top register is ANDed with 1 from the register below it. From the truth table we can see that 1 AND 1 = 1, so 1 is the result in bit 0 of the Z register. Moving to bit 1, we have 0 AND 1 = 0, as can be seen from the truth table. Bit 1 of the Z register therefore has a value of 0. And so on for the remaining bits.

The AVR instruction set has two AND instructions, namely AND (Logical AND) and ANDI (Logical AND with Immediate). The AND instruction ANDs the numbers in two registers with each other. ANDI ANDs a register with immediate data, in other words with constant data that is encoded in the ANDI instruction. ANDI can only be used on registers R16 to R31.

The following program demonstrates the AND and ANDI instructions. Load and run it in the debugger with simulator using the test_asm project as usual.

```
test_asm : main.asm - AND and ANDI examples
ldi r16, 0b1100_0101
ldi r17, 0b1001_0111
and r16, r17
ldi r18, 0b1010_1011
andi r18, 0b0000_1111
```

In the above code, the two binary numbers from the example in Figure 7.1 are loaded into R16 and R17. After the AND instruction has run, the result of the operation is placed in R16. Step over the code in the debugger and confirm that the result of the AND operation is 0b1000_0101. Remember that you can right click register R16 and R17 in the Processor Status window and change the format of the register to binary.

The second part of the example program loads 0b1010_1011 to register R18 and then uses the ANDI instruction to AND R18 with a constant data value of 0b0000_1111. The result of the ANDI operation is placed back in R18. Step over the code and confirm the result in the debugger. ANDing register R18 with 0b0000_1111 or 0x0F effectively clears all bits in the upper nibble of the register. This is known as masking the register. The AND operation can be used to clear any bits and leave others unchanged by changing the mask value, which is the constant value used with the ANDI instruction. For example, to clear all bits in the register except the highest two, or upper two bits, use a mask value of 0b1100_0000, or 0xC0. This leaves the upper two bits unchanged.

### 7.4.2 Logical OR

A logical OR operation has a truth table as shown in Figure 7.2.

| A | B | Z |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

![](img/83ef13a6c66cc7882b2f357e97f451dc_144_0.png)

Figure 7.2: OR Truth Table and Example of Bitwise OR Operation

In a logical OR operation, if one or both of the input bits is 1, then the output is 1. The output will only ever be 0 if both inputs are 0. As with the AND operator, the OR is done on the bits in two 8-bit numbers a bit at a time. Each bit in one number is ORed with the corresponding bit in the other number according to the OR truth table. A logical OR performs the following logical operations as can be seen in the truth table:

```
0 OR 0 = 0
0 OR 1 = 1
1 OR 0 = 1
1 OR 1 = 1
```

The AVR instruction set has two logical OR instructions, namely, OR (Logical OR) and ORI (Logical OR with Immediate). These instructions are the equivalent of the AND and ANDI instructions respectively, except that they use the OR truth table in their logical operation. Only registers R16 to R31 can be used with ORI.

Example code using the OR and ORI instructions follows. Step through the code in the debugger using the test project again, as described in the paragraphs that follow.

```
test_asm : main.asm - OR and ORI demonstration

ldi r16, 0b1100_0101
ldi r17, 0b1001_0111
or r16, r17

ldi r18, 0b1010_1011
ori r18, 0b0000_1111
```

In the above code, OR is used to logically OR R16 with R17 and place the result of the operation in R16. Step through the first three instructions in the debugger and confirm the result is as expected from the truth table in Figure 7.2.

ORI uses immediate data, which is constant data encoded in the instruction, to logic OR with a value in a register. Step over the last two instructions from the above code listing to see the ORI instruction ORing an immediate value with R18 and saving the result back to R18. The immediate value is effectively used as a mask value to set the bottom nibble of the value in R18, but leave the top nibble of R18 unchanged.

If a mask value is used with ORI, then all bits of the mask value that are 1 result in an output of 1. All bits in the mask value that are 0 leave the corresponding bits in the input number unchanged. Consider the following example that uses 0b0000_1111 as a mask value and ORs it to 0b1001_0101.

```
0b1001_0101
OR 0b0000_1111
= 0b1001_1111
```

Notice that the result of the OR operation is 0b1001_1111. The upper nibble of the result is the same as the upper nibble of the top number. This is because it was ORed with the upper nibble of the mask value which contains only zeros, and therefore leaves the upper nibble of the first number unchanged.

The lower nibble of the result contains only ones because the mask value contains only ones. This is because anything ORed with 1 is always 1. A mask value used in combination with the OR operation is frequently used to set one or more bits while leaving others unchanged.
