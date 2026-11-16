
ADD and ADC have already been sufficiently covered in the main text. Refer to section 7.2.1 for ADD examples and section 7.2.2 for an ADC example.

## ADIW (Add Immediate to Word)

ADIW adds an immediate value that can only be between 0 and 63, to one of four register pairs. The result of the addition is placed in the chosen register pair. In the instruction encoding of ADIW, 6 bits are available to represent immediate data encoded in the instruction, which means that 2^6 = 64 different values can be used: 0 to 63. Two bits are available to represent the chosen register pair, giving 2^2 = 4 possible register pairs.

ADIW can be used to perform an increment on a 16-bit number in a single line of code. Because ADIW operates on the register pairs, it can be used to increment a pointer when one of the register pairs is used as a pointer.

The following code shows how to use the ADIW instruction to increment the Z register.

```
.equ NUM = 2048 ; Number > 8 bits
ldi ZL, low(NUM) ; Load number to Z register
ldi ZH, high(NUM)
loop:
adiw ZH:ZL, 1 ; Increment 16-bit number by 1
rjmp loop
```

In the above code, a number that uses up more than 8 bits is equated to the name NUM. NUM is then loaded to the Z register in two parts, 8 bits at a time. In the loop, the value of NUM, which is 2048 and stored in the Z register, is incremented by 1 using ADIW. The notation ZH:ZL refers to the Z register upper and lower bytes. This notation makes it easier to read the code, but actually disassembles to the following:

```
adiw ZH:ZL, 1 ; Increment 16-bit number by 1
00000002 ADIW R30,0x01 Add immediate to word
```

As can be seen in the above code, the first operand of the ADIW instruction, which is the register pair, disassembled to R30 for ZH:ZL. The second operand is the value to add to the selected register pair and is simply displayed in hexadecimal in the disassembly. R30 is ZL, and represents the Z register when used with ADIW. This makes it possible to specify the Z register in four different ways. ZH:ZL can be used, as the example code did or R31:R30. ZL could be used instead of ZH:ZL. Alternatively, R30 could be used. Of the four, ZH:ZL probably gives the clearest meaning when used with ADIW.

Although there are two bits in the ADIW instruction that represent the four possible register pairs, it is not possible to directly use these bits when writing assembly language. If it were so, then the following would be possible.

```
adiw 3, 1 ; Not valid code!
```

The above line of code is meant to increment the Z register by 1, but causes an invalid register error. Although 3, or 11 binary, is encoded in the instruction to represent the Z register, it can't be used this way in assembly language code.

The four register pairs that can be used with ADIW are as follows.

| Register Pair Encoding | Register Pair | Alternate Notation | Single Register Notation | Register Pair Name |
|---|---|---|---|---|
| 0 | R25:R24 | none | R24 | none |
| 1 | R27:R26 | XH:XL | R26 or XL | X register |
| 2 | R29:R28 | YH:YL | R28 or YL | Y register |
| 3 | R31:R30 | ZH:ZL | R30 or ZL | Z register |

In the above table, Register Pair Encoding shows the value that is encoded in the ADIW instruction to represent a register pair. The Register Pair column shows the notation that can be used with ADIW to represent the register pair in the MSB:LSB order. Alternate Notation shows an alternate to the Register Pair notation. The first register pair does not have a register pair name, so has none in the Alternate Notation column. The LSB of the register pair can be used with ADIW, as shown in the Single Register Notation column, instead of the register pair or alternate notation to represent the register pair. The last column shows the register pair names when used in combination as 16-bit registers. Again, the first register pair does not have a name.

From the above table, it can be seen that all of the following lines of code do the same thing and increment the Z register by 1.

```
adiw R31:R30, 1 ; Increment Z register by 1
adiw ZH:ZL, 1 ; Increment Z register by 1
adiw R30, 1 ; Increment Z register by 1
adiw ZL, 1 ; Increment Z register by 1
```

Each of the above lines of code disassemble to the following line of code.

```
ADIW R30,0x01
```

## Subtraction Instructions

### SUB (Subtract Without Carry)

SUB is covered in section 7.3 of Chapter 7.

### SUBI (Subtract Immediate)

We first came across SUBI when looking at disassembled code in section 8.2.2.4 of Chapter 8, it was also used in section 9.3.2.2 of Chapter 9 to force the status register to update.

### SBCI (Subtract Immediate with Carry)

SBCI was used in combination with SUBI to decrement a 32-bit number in section 10.2.2 of Chapter 10, and was subsequently used throughout Chapter 10. It also appeared in the disassembled code in section 8.2.2.4 of Chapter 8.

### SBC (Subtract with Carry)

SBC is like SBCI, but instead of using an immediate value as the second operand, it uses a second register. In other words, it subtracts two registers and takes into consideration the carry flag in the status register. SBC is simple enough to understand, so will not be explained further. Refer to the AVR Instruction Set Manual for more information on SBC.

### SBIW (Subtract Immediate from Word)

SBIW is the subtraction counterpart to ADIW. It works exactly the same way as ADIW, but instead of adding a value between 0 and 63 to a register pair, it subtracts the value. The same four register pairs are operated on. An example is shown in the following code.

```
.equ    NUM = 2048        ; Number > 8 bits
ldi     ZL, low(NUM)      ; Load number to Z register
ldi     ZH, high(NUM)
loop:
sbiw    R31:R30, 1        ; Decrement Z register by 1
sbiw    ZH:ZL, 1          ; Decrement Z register by 1
sbiw    R30, 1            ; Decrement Z register by 1
sbiw    ZL, 1             ; Decrement Z register by 1
rjmp    loop
```

As can be seen in the above code, the same different notations can be used to access the register pair for SBIW as was done for ADIW. The same register pairs from the table under the ADIW section can also be used with SBIW. In the above code, 1 is subtracted from the Z register at each SBIW instruction.

## 11.2.1.2 Logical Instructions

The five logical instructions implemented in the ATtiny25/45/85 and ATtiny13(A) are well covered in Chapter 7, so they are cross referenced here to easily find them in Chapter 7.

### Logical AND

- AND (Logical AND)
- ANDI (Logical AND with Immediate)

AND and ANDI are covered in section 7.4.1 of Chapter 7.

### Logical OR

- OR (Logical OR)
- ORI (Logical OR with Immediate)

OR and ORI are covered in section 7.4.2 of Chapter 7.

### Logical Exclusive OR

- EOR (Exclusive OR)

EOR is covered in section 7.4.3 of Chapter 7. In section 8.2.4.2 of Chapter 8, EOR is used to toggle an LED.

## 11.2.1.3 Increment and Decrement Instructions

### INC (Increment)

The INC instruction simply increments a register by 1 and is demonstrated in section 5.2.2 of Chapter 5. It is also used in section 8.2.1.4 of Chapter 8, and in section 9.3.3 and 9.3.4 of Chapter 9.

### DEC (Decrement)

DEC decrements a register by 1 and was first used in the LED blink assembly code of section 2.3.2 in Chapter 2 to decrement registers in the software time delay subroutine. DEC was also used to demonstrate the use of the Z flag in section 6.5.1 of Chapter 6.

## 11.2.1.4 Sign Change Instructions

### COM (One's Complement)

COM converts the number in a register to one's complement, in other words it inverts each bit in the register, as the following code demonstrates by converting the binary number 1001_0011 to its 1's complement value 0110_1100.

```
ldi R16, 0b1001_0011 ; Load 0x93 to R16
com R16 ; R16 now contains 0b110_1100 (0x6C)
```

### NEG (Two's Complement)

NEG converts the number in a register to the two's complement form of the number. In the following code, 1 is loaded to R16, then converted to -1 in 2's complement format, which is a value of 0xFF. The negative flag and other flags in the status register are affected by the operation.

```
ldi   R16, 1    ; Load +1 to R16
neg   R16       ; Change value in R16 to -1 in 2's complement format
```

## 11.2.1.5 Bit Set and Clear Instructions

### SBR (Set Bits in Register)

SBR performs an OR operation between immediate data and a register in order to set bits in the register. SBR is the same as using ORI and has the same instruction encoding. In the following code example, the SBR and ORI instructions do exactly the same thing, setting the upper four bits in R16, while leaving the lower four bits unchanged.

```
ldi   R16, 0x02
sbr   R16, 0xF0

ldi   R16, 0x02
ori   R16, 0xF0
```

It is interesting to note in the disassembly of the above code that both the SBR and ORI instructions disassemble to the same code, as shown below.

```
ldi   R16, 0x02
0000000 LDI R16, 0x02     Load immediate
sbr   R16, 0xF0
0000001 ORI R16, 0xF0     Logical OR with immediate
ldi   R16, 0x02
0000002 LDI R16, 0x02     Load immediate
ori   R16, 0xF0
0000003 ORI R16, 0xF0     Logical OR with immediate
```

Both instructions disassemble to ORI R16,0xF0 as can be seen above. Looking at both instructions in the AVR Instruction Set Manual shows that they both have the same encoding, shown below.

```
0110 KKKK dddd KKKK
```

This means that SBR is a synonym for, or another name for ORI.
