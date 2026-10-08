Most assemblers allow the programmer to use a special symbol or delimiter to indicate the beginning or end of each field. Typical delimiters used are spaces, commas, semicolons, and colons:

+   - Spaces are used between fields.
- Commas (,) are used between addresses in an operand field.
- A semicolon (;) is used before a comment.
- A colon (:) or no delimiter is used after a label.

# ## 4.3.3 Specifying Numbers by Typical Assemblers

To handle numbers, most assemblers consider all numbers as decimal numbers unless specified otherwise. All assemblers will also specify other number systems, including hexadecimal numbers. The user must define the type of number system used in some way. This is generally done by using a letter or a symbol before or after the number. For example, Intel uses the letter H after a number to represent it as a hex number, whereas Microsoft's MPLAB assembler uses several ways to represent a hex number. Three most common ways are: 0x before the number, or H after the number, or default (without using a letter or a symbol before or after the number), to represent it as a hex number. As an example, 60 in hexadecimal is represented by the MPLAB assembler as either 0x60 or 60H, or simply 60.

Some assemblers such as the MASM 32 assembler for the Pentium microprocessor require hexadecimal numbers to start with a digit (0 through 9). A 0 is typically used if the first digit of the hexadecimal number is a letter. This is done to distinguish between numbers and labels. For example, typical assemblers such as MASM32 will normally require the number F3H to be represented as 0F3H; otherwise, the assembler will generate an error. However, MPLAB assembler used in this book for assembling PIC18F assembly language programs does not require '0' to be used if the first digit of a hexadecimal number is a letter.

The MPLAB uses D before a 'number' to specify a decimal number. For example, decimal number 60 can be represented as `D'60'`. A binary number is specified by the MPLAB using B before the 'Number'. For example, 8-bit binary number 01011100 can be represented by the MPLAB as `B'01011100'`.

# ## 4.3.4 Assembler Directives or Pseudoinstructions

Assemblers use pseudoinstructions or directives to make the formatting of the edited text easier. Pseudoinstructions are not translated directly into machine language instructions. They equate labels to addresses, assign the program to certain areas of memory, or insert titles, page numbers, and so on. To use the assembler directives or pseudoinstructions, the programmer puts them in the op-code field, and if the pseudoinstructions require an address or data, the programmer places them in the label or data field. Typical pseudoinstructions are ORIGIN (ORG), EQUATE (EQU), DEFINE BYTE (DB), and DEFINE WORD (DW).

### **ORIGIN (ORG)**

The directive ORG lets a programmer place programs anywhere in memory. Internally, the assembler maintains a program counter type of register called an *address counter*. This counter maintains the address of the next instruction or data to be processed.

An ORG directive is similar in concept to a JUMP instruction. Note that the JUMP