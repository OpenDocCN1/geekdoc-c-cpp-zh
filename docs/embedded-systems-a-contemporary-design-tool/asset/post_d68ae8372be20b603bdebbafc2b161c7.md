
1.15 The hidden bit format for floating point numbers provides an extra bit of resolution for free. Someone has suggested applying the same technique to gain two extra bits. What do you think of the idea? Are there any problems with it?

## Instructions

1.16 The essential components of an instruction are the op-code and the operand(s) on which the operation is to be performed. Is it necessary that the op-code always contain the same number of bits? Why or Why not?

1.17 The chapter discussed one-, two-, and three-address instructions. Is it possible to have a zero-address instruction? What are the benefits of such a design?

1.18 How can double indirection be implemented in an instruction?

## An Instruction Set View

1.19 What are the four major pieces of information that an instruction must convey? How are these done?

1.20 In the chapter, several different addressing modes were discussed. Can you think of others that might be useful?

1.21 Are the bits in the machine code representation of an instruction arbitrary, or do they have a specific meaning? If they have meaning, what might it be?

1.22 Microprocessor instructions can be classified into three major groups. What are these groups? Please describe what characteristics instructions in each of the groups.

1.23 If an instruction contains the address of an operand in memory, how can the source or destination of an operation be conveyed if the source or destination is an input or output port on the microprocessor?

## 1.16 PROBLEMS

- 1.1 Express the following decimal numbers in the bases indicated.

  Decimal: 1011, 23.4, 207, 111.439

  - (a) Binary
  - (b) Octal
  - (c) Hexadecimal
  - (d) Binary Coded Decimal (BCD)

- 1.2 Express the following binary numbers in the bases indicated.

  Binary: 101101011, 1101.11001, 1001001110, 111.001

  - (a) Decimal
  - (b) BCD

1.24 If one has an assembly code listing for an embedded program that has been running on a Motorola processor, will that program run on an Advanced Micro Devices (AMD) processor?

1.25 If one has a C code listing for an embedded program that has been running on a Motorola processor, will that program run on an AMD processor?

1.26 Please explain how a branch type of instruction works from an instruction set point of view.

1.27 How does an instruction know how or where to access a flag or condition code register?

1.28 Discuss ways of managing the case of the instruction decoder finding an op-code in an instruction that it does not recognize.

## A Register View

1.29 A RISC architecture frequently incorporates many more registers than does a CISC design? Why is this?

1.30 Explain why a register access is generally faster than a memory access.

1.31 Explain how an indexed type of instruction might be implemented at the register level.

1.32 How can data from multiple sources be transferred into the same register?

1.33 Discuss the advantages and disadvantages of building a register from latches versus flip-flops.

1.34 What are the advantages and disadvantages of tristate gates versus a traditional multiplexer gate for transferring data from one register to another?

- 1.3 Express the following hexadecimal numbers in the bases indicated.

  Hexadecimal: B3D9, CA43, 1234, 5D.06F

  - (a) Decimal
  - (b) BCD
  - (c) Binary

- 1.4 Express the following decimal numbers in the bases indicated.

  Decimal: 12.34, 9503.313

  - (a) Binary
  - (b) Hexadecimal

- 1.5 Express your given name and your family name as ASCII characters in the following format:

  givenName familyName

  The ASCII characters should be written in their binary form and stored so as to use the smallest number of 16-bit words. Check the Web site http://asciitable.com/ for the set of ASCII characters.

- 1.6 We have the following data stored in the first 32 locations of a memory as shown.

| Memory address | Value |
|---|---|
| 00000 | 0000010 |
| 00001 | 0101001 |
| 00010 | 1000001 |
| 00011 | 0101111 |
| 00100 | 0001111 |
| 00101 | 0000011 |
| 00110 | 1110101 |
| 00111 | 1101001 |
| 01000 | 1111101 |
| 01001 | 0001111 |
| 01010 | 0011101 |
| 01011 | 0001011 |
| 01100 | 0000001 |
| 01101 | 0101111 |
| 01110 | 0101001 |
| 01111 | 0100011 |
| 10000 | 0000010 |
| 10001 | 0001101 |
| 10010 | 0111101 |
| 10011 | 0111001 |
| 10100 | 1101001 |
| 10101 | 0011101 |
| 10110 | 0000001 |
| 10111 | 0001111 |
| 11000 | 0011111 |
| 11001 | 0010001 |
| 11010 | 0111101 |
| 11011 | 1001101 |
| 11111 | 1010101 |

(a) Please identify the words at the following hexadecimal addresses.

12, F, 1E, 7, 1C

(b) Please give the hexadecimal addresses for the following words in memory. 1100101, 0010111, 0100011, 0111101

- 1.7 We have the following C code fragment:

```c
unsigned char a = 0xD3;
char b = 'A';
int c = 6;
int d = 9;
int e = -31564;
unsigned int f = 0xFAD7;
float g = 3.1;
float h = 0.0345;
int j;
int* cPtr = &c;
int* dPtr = &d;
int** ccPtr = &cPtr;
int** ddPtr = &dPtr;
float* gPtr = &g;
float* hPtr = &h;
```

| Variable | Memory address | Value |
|---|---|---|
| | 00000 | 1000 |
| | | 1001 |
| | | |
| | | |
| | | |
| | | |
| | | 2000 |
| | | 2001 |
| | | |
| | | |
| | | |
| | | |
| | | 3000 |
| | | 3001 |
| | | |
| | | |
| | | |
| | | |
| | | 4000 |
| | | 4001 |
| | | |
| | | |
| | | |
| | | |

- (a) Please put the values, in binary, for all of the variables into memory. Assume 16-bit words and big endian notation.
- (b) How do the values in memory change after the following code fragment is executed?

```
e = e + f;
*gPtr = *gPtr + *hPtr;
j = **ccPtr - **ddPtr;
```

- 1.8 Convert each of the following floating point numbers into binary. Assume a 16-bit word for which the weight of the least significant bit is 2^-7. Following the conversion, what is the error for each number?

- (a) E = 72.23
- (b) F = 121.034
- (c) G = 98.6
- (d) H = 43.612

- 1.9 Using the numbers and errors from Problem 1.8, perform the following calculations. What is the worst case error for each calculation?

- (a) E + F + G + H
- (b) E*F
- (c) G*H
- (d) (G*H)/(E + F)

- 1.10 Please show the contents of the stack, the position of the stack pointer (SP), and the contents of the indicated registers after the execution of each of the following instructions. The instructions are executed in sequence.

Initially, the registers contain the following values R0 = 1234, R1 = 2345, R2 = 4567, R3 = 8901. For two-operand instructions, assume that the left-hand operand is also the destination.

| PC | Instruction |
| :--- | :--- |
| FACE | ADD R3, R1 |
| FACF | PUSH R2 |
| FAD1 | POP R3 |
| FAD6 | ADD R1, R2 |

| Registers | | Stack |
| :--- | :--- | :--- |
| R0 | | |
| R1 | | |
| R2 | | |
| R3 | | |
| PC | | |

| Registers | | Stack |
| :--- | :--- | :--- |
| R0 | | |
| R1 | | |
| R2 | | |
| R3 | | |
| PC | | |

| Registers | | Stack |
| :--- | :--- | :--- |
| R0 | | |
| R1 | | |
| R2 | | |
| R3 | | |
| PC | | |

| Registers | | Stack |
| :--- | :--- | :--- |
| R0 | | |
| R1 | | |
| R2 | | |
| R3 | | |
| PC | | |

| Registers | | Stack |
| :--- | :--- | :--- |
| R0 | | |
| R1 | | |
| R2 | | |
| R3 | | |
| PC | | |

- 1.11 Using the assembly language instructions introduced in the chapter, write a program to solve the following problem.
\[
\left( \frac{(A \cdot B)}{(C - D)} \right) \cdot E
\]

The variables A–E are already stored in the registers R1–R5. The result is to be placed into register R6. You may not change what is stored in registers R1–R5.

- 1.12 How does your program in Problem 1.11 change if the processors contain the addresses of the variables rather than the values of the variables?

- 1.13 Given the memory locations, values below, and a one-address machine with an accumulator (the accumulator is the default destination), what values do the following instructions load into the accumulator? Assume that R1 and R3 contain the values 0x5000 and 0x3000, respectively.

| Memory location | Contents | Accumulator |
|---|---|---|
| 1000 | 2000 | |
| 2000 | 3000 | |
| 3000 | FACE | |
| 4000 | 5000 | |
| 5000 | 1000 | |

```
MOVE R1 5000
LOADI 0x5000
MOVE *R1
LOADI 0xFACE
MOVE *R2 3000
```

- 1.14 A partial set of specifications for a typical embedded processor are given as:

- 16-bit architecture – 16-bit-wide data words.
- 20-bit instructions.
- 8 general-purpose registers.
- One-, two-, and three-address instructions.
- Each address field is qualified by a 2-bit field to identify any of the following four different addressing modes: register direct, register indirect, pc relative, indexed.

(a) Please give the format for a one-, two-, and three-address instruction for this machine. Observe that the width of the instruction is different from the width of the data. This is not a problem.

(b) Please show how the following instructions would be implemented using the format you designed.

ADD2, SUB2, MUL, DIV
opcodes: 0001, 0010, 0011, 0100
respectively.
add, subtract, multiply, divide two operands.
MOVE opcode: 0101
Move a word from memory into a register.
Move a word to a memory address location that is contained in a register.
JUMP opcode: 0110
Jump to a location.
BR, BE opcodes: 00111, 01000
Load a 16-bit integer into a register.
CMP opcode: 01001

Compare two operands and set the appropriate condition code.

CALL, RET opcodes: 01010, 01011
PC is replaced by a specified address and control is transferred to the address.
Control is returned to the calling context.

- 1.15 We have the following requirements for a microprocessor.

Assume that the processor has 32-bit instructions. Let each register operand address be specified by a 5-bit field for the address and qualified by a 2-bit field to identify any of the following four different addressing modes: register direct, register indirect, pc relative, indexed.

Assume there are K two-operand instructions and L zero-operand instructions (e.g. HALT) required.

- (a) What is the maximum number of one-address instructions that can be provided in the computer?
- (b) Give the format for zero-, one-, and two-address instructions. How are these distinguished?
- (c) How would the following instructions be expressed using your format:
  - Move a word from memory into a register.
  - Move a word to a memory address location that is contained in a register.
  - Jump to a location.
  - Add, subtract, multiply, divide two operands.
  - Load the integer 99 into a register.
  - Read from the keyboard.

- 1.16 Consider the following state of a computer:

```
Register R1 contains 800
Register R2 contains 3000
Memory location 1000 contains 2000
Memory location 2000 contains 3000
Memory location 3000 contains 1000.
```

All numbers are expressed in hex notation.

For the following three instructions, each is executed from the above initial state.

- (a) What is the effect of executing each instruction?
- (b) How many words does each instruction occupy?
- (c) How many memory accesses does the fetching and execution of each instruction require?

Assume each instruction is independent of the others

```
MOVE *R2, R1 // move R1 to what R2 is pointing at
MOVE *R2, 1800(R1) // move the contents of the memory location // indexed by R1 to what R2 is pointing at
MOVE *R2, #DEAD // move the constant // DEAD to what R2 // is pointing at.
```
