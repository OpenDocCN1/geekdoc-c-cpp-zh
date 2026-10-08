
## 6 Assembly Language Programming with the PIC18F: Part 1

In this chapter we provide the first part of the PIC18F's instruction set. We also cover the fundamental concepts associated with assembly language programming relating to the PIC18F microcontroller. Topics include basics of the PIC18F MPLAB assembler, PIC18F instruction format, instruction set, and assembly language programming.

### 6.1 Introduction to the PIC18F MPLAB assembler

As mentioned in Chapter 3, the assembly language program is translated into binary via a program called *assembler*. In this section, we will review the concepts described in Chapter 3 relating them to the PIC18F MPLAB assembler. For convenience, some of the topics will be repeated.

The assembler reads each instruction of an assembly language program as ASCII characters and translates them into the respective binary op-codes. For example, the PIC18F assembler translates the SLEEP (places the PIC18F in sleep mode; same as HALT instruction in other processors) instruction into its 16-bit binary op-code is 0000 0000 0000 0011 (0003 in hex), as depicted in Table 6.1.

A notable advantage of the assembler is its ability to handle address computation. Most programs use addresses within the program as data storage or as targets for jumps or calls. When programming in machine language, these addresses must be calculated by hand. The assembler solves this problem by allowing the programmer to assign a symbol to an address. The programmer may then reference that address elsewhere by using the symbol. The assembler computes the actual address for the programmer and fills it in automatically.

One can obtain hands-on experience with a typical assembler for a microcontroller by downloading it from the Internet. The MPLAB assembler/simulator is used to assemble and debug all PIC18F assembly language programs in this book. It can be downloaded free of charge from the web site: www.microchip.com.

As mentioned in Chapter 4, each line in an assembly language program includes four fields:

- Label field
- Mnemonic or op-code field
- Operand field
- Comment field

The rules associated with the MPLAB will be used in explaining the meaning of these fields. The assembler ignores the comment field but translates the other fields.

**TABLE 6.1** Conversion of SLEEP instruction into its Binary Op-Code

| | Assembly Code | Binary Form of ASCII Codes as Seen by the Assembler | Binary Op-Code Created by the MPLAB PIC18F Assembler |
|---|---|---|---|
| | S | 0101 0011 | |
| | L | 0100 1000 | 0000 0000 0000 0011 |
| | E | 0100 0101 | |
| | E | 0100 0101 | |
| | P | 0101 0000 | |

The label field must start with an alphabetic character, and can have a maximum length of 32 characters.

The assembler must know where one field starts and another ends. The MPLAB, like most assemblers, allows the programmer to use a special symbol or delimiter to indicate the beginning or end of each field. Typical delimiters used are spaces, commas, and semicolons:

- Spaces are used between fields.
- Commas (,) are used between addresses in an operand field.
- A semicolon (;) is used before a comment.
- No symbol is used after a label.

To handle numbers, most assemblers consider all numbers as decimal numbers unless specified otherwise. The MPLAB assembler, however, recognizes a number without any prescript or postscript as a hexadecimal number. Most assemblers, including the MPLAB assembler, will also allow other number systems, including hexadecimal. For example, with the MPLAB assembler, the user can define a hexadecimal number usually in three ways using:

- 0x before the number
- H after the number
- default (without any prescript or postscript)

This means that 60 in hexadecimal can be represented as 0x60, 60H, or 60. A `0` is used by most assemblers if the first digit of the hexadecimal number is a letter; otherwise, the assembler will generate an error. This is done to distinguish between numbers and labels. However, the MPLAB assembler does not require a `0` to be placed in front of the number if the first digit of the hexadecimal number is a letter. These symbols (0x or H or none) will be used interchangeably throughout the book to represent hexadecimal numbers.

The MPLAB uses D before a `number` to specify a decimal number. For example, decimal number 60 can be represented as D`60`. A binary number is specified by the MPLAB using B before the `Number`. For example, 8-bit binary number 01011100 can be represented by the MPLAB as B`01011100`.

ASCII characters are represented using MPLAB by the symbols `c ' or A ` . For example, PIC18F is represented as `PIC18F' or A`PIC18F` to be recognized as ASCII characters in MPLAB.

Assemblers use pseudoinstructions or directives to make the formatting of the edited text easier. These directives are not translated directly into machine language instructions. Typical assembler directives are discussed in the following.

### ORIGIN (ORG)

The directive ORG specifies the starting address of a program or data. For example, after assembling the following statements, the MPLAB will place the assembled code for MOVLW 0x50 starting at address 0x100:

```
ORG           0x100
MOVWL         0x50
```

### Equate (EQU)

The EQU assigns a value in its operand field to an address in its label field. This allows the user to assign a numerical value to a symbolic name. The user can then use the symbolic name in the program instead of its numerical value. A typical example of EQU is START EQU 0x20, which assigns the value 20 in hexadecimal to the label START.

To illustrate the EQU directive, consider the following instruction sequence:

```
TEST EQU    0x20
      MOVWL   TEST
      MOVWF   TEST
```

The instruction MOVWL TEST, in the above, moves the constant 0x20 into WREG. The instruction MOVWF TEST, on the other hand, moves the contents of WREG into the data register with address 0x20.

### Define Byte (DB)

The directive DB is generally used to set a memory location to a certain byte value. For example,

```
START DB      0x45
```

will store the data value 45 hex to the address START. The DB directive can be used to generate a table of data as follows:

```
ORG    0x70
DB     0x20,0x30,0x40,0x50
```

In this case, 20 hex is the first data of the memory location 70 hex; 30 hex, 40 hex, and 50 hex occupy the next three memory locations. Therefore, the data in memory will look like this:

| Address | Data |
|---|---|
| 70 | 20 |
| 71 | 30 |
| 72 | 40 |
| 73 | 50 |

### Define Word (DW)

The directive DW is typically used to assign a 16-bit value to two memory locations. For example,

```
ORG           0x50
DW            0x4AC2
```

will assign C2 to location 50 hex and 4A to location 51 hex. It is assumed that the assembler will assign the low byte first (C2) and then the high byte (4A). The DW directive can be used to generate a table of 16-bit data as follows:

```
ORG     0x80
DW      0x5000,0x6000, 0x7000
```

In this case, the three 16-bit values 5000 hex, 6000 hex, and 7000 hex are assigned to memory locations starting at the address 80 hex. That is, the array would look like this:

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_128_0.png)

### INCLUDE

The directive INCLUDE includes source code or a file from the MPLAB library for a specific device. This will allow the MPLAB to assemble a program for that device. Note that using INCLUDE <P18F4321.INC> at the beginning of a program will add appropriate files from the MPLAB library required to assemble the program.

For example, the INCLUDE <P18F4321.INC> includes files which will insert SFR addresses during the assembly. This will allow the programmer to use variable names rather than their physical addresses. The programmer can use variable names such as PORTA in the program, and the assembler will insert its SFR address (F80H) whenever it will encounter PORTA in the program. This is very convenient for the programmer.

### END

The END directive indicates the end of assembly language program.

Let us now explain how one can write a typical PIC18F assembly language program. A simple program for adding two 8-bit numbers written in PIC18F assembly language is provided below:

| Label Field | Mnemonic Field | Operand Field | Comment Field |
| :--- | :--- | :--- | :--- |
|  | INCLUDE | <P18F4321.INC> |  |
| SUM | EQU | 0x40 |  |
|  | ORG | 0x100 | ; STARTING ADDRESS |
|  | MOV LW | 0x02 | ; MOVING 2 INTO WREG |
|  | ADDLW | 0x05 | ; ADDING WREG and 5 |
|  | MOV WF | SUM | ; STORE RESULT IN SUM |
|  | SLEEP |  | ; HALT |
|  | END |  | ; END OF PROGRAM |

Let us explain the above program. INCLUDE <PIC18F4321.INC> at the beginning of the program will add appropriate files from the MPLAB library required to assemble the program.

SUM EQU 0x40 assigns 40 (hex) to label SUM. ORG 0x100 assembles the program at address 100 (hex). MOV LW 0x02 moves 02 (hex) into WREG. ADDLW 0x05 adds the contents of WREG with 05 (hex), and stores the 8-bit result, 07 (hex) in WREG. The instruction MOV WF SUM stores the 8-bit contents of WREG (07 hex) in file register SUM with address 40 (hex). The SLEEP instruction halts the program. Finally, the MPLAB assembler directive "end" indicates the end of the program. Note that the directive "end" must be present at the end of all PIC18F assembly language programs.

The assembly language program described above called a source file, contains all the instructions required to execute a program. It should be mentioned that the source code for the MPLAB assembler is not case sensitive. However, it is a good idea to type the
