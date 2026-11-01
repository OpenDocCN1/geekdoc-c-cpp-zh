
1. Column 1 is what is known as the location counter. It is in hexadecimal and gives, relative to location zero, the starting byte address of each line of code in the machine language image being created by the assembler. Each time a machine language instruction is generated or an area of memory is allocated, the location counter will increment by an amount equal to the effective size of the instruction or data area. To achieve memory address alignment, bytes are occasionally skipped so the location counter increment can sometimes be larger than the size of the instruction or data area (all instructions must begin on halfword boundaries, F type data definitions on fullword boundaries and so forth).

2. Column 2 is also in hexadecimal and is the translation of the assembly language statement (up to the first 8 bytes) of the source code shown in column 6. Not all assembly language source statements generate machine language so this column may be blank.

3. Column 3 is the effective address, relative to zero, of the first operand of the machine language instruction if the first operand is a memory address. If the first operand is not a memory address (for example, a register) this column is blank. The effective address is the location counter address.

4. Column 4 is the effective address, relative to zero, of the second operand if the second operand is a memory address. It is blank otherwise.

5. Column 5 indicates the macro level (first number in the parentheses), the original source code statement line number (second number in the parentheses), and, finally, the actual line number taking into account statements inserted by macro expansions.

6. Column 6 contains your original source code statements.

The reason why we need to know how to read the .PRN file is because it is used in debugging. Very often when we have an error, we need to examine the contents of a memory dump (see Chapter 20) and the .PRN file is our road map to the dump.

For example, look at the line with the location counter value of 72₁₆ (leading zeros omitted). But there are two lines with location counter value of 72₁₆! The first of these, corresponding to original source code line 3 (column 5), is the value of the location counter at the point when the assembler reads the EQUIREGS statement.

EQUIREGS is the name of a macro. The assembler goes to the macro library and inserts the 16 lines of macro code at this point.

Note that source code line number after the EQUIREGS has line jumps from 15 to 33. This increase indicates that lines not shown were inserted.

| Col 1 | Col 2 | Col 3 | Col 4 | Col 5 | Col 6 |
|---|---|---|---|---|---|
| 000000 |  |  |  | (1/1)1 | PRINT NOGEN |
| 000000 |  |  |  | (1/2)2 | ADD SUBENTRY |
| 000072 |  |  |  | (1/3)15 | EQUIREGS |
| 000072 | 1B22 |  |  | (1/4)33 | SR R2,R2 +Hero |
| 000074 | 5A20DDB0 |  | 0000B8 | (1/5)34 | A R2,ONE |
| 000078 | 5A20DDB4 |  | 0000BC | (1/6)35 | A R2,TWO |
| 00007C | 5A20DDB8 |  | 0000C0 | (1/7)36 | A R2,THREE |
| 000080 | 5A20DDBC |  | 0000C4 | (1/8)37 | A R2,FOUR |
| 000084 | 5A20DDC0 |  | 0000C8 | (1/9)38 | A R2,FIVE |
| 000088 | E0200DA200B | 0000AA |  | (1/10)39 | XPRNT MSG,L'MSG |
| 00008E | 5220DCC4 |  | 0000CC | (1/11)40 | XDECO R2,DBL |
| 000092 | E0200DC4000C | 0000CC |  | (1/12)41 | XPRNT DBL,L'DBL |
| 000098 |  |  |  | (1/13)42 | SUBEXIT |
| 0000AA | C184849895874005 |  |  | (1/14)49 | MSG DC C'Adding Numbers' |
| 0000B8 | 00000001 |  |  | (1/15)50 | ONE DC F'1' |
| 0000BC | 00000002 |  |  | (1/16)51 | TWO DC F'2' |
| 0000C0 | 00000003 |  |  | (1/17)52 | THREE DC F'3' |
| 0000C4 | 00000004 |  |  | (1/18)53 | FOUR DC F'4' |
| 0000C8 | 00000005 |  |  | (1/19)54 | FIVE DC F'5' |
| 0000CC |  |  |  | (1/20)55 | DBL DS CL12 |
| 0000DB |  |  |  | (1/21)56 | END |

Figure 47 ADD.PRN

Macro expansions (that is, the lines inserted) are not being shown because of the PRINT NOGEN directive.

In this case, the code inserted by the EQUIREGS does not generate machine language code - the statements consist entirely of assembler directives. Hence, the location counter is unchanged on the line after the EQUIREGS.

Most macros, however, do generate executable assembly language code. Note that the location counter jumps from zero at the beginning of the program to 72₁₆ following the SUBENTRY. This is because the SUBENTRY macro generated 72₁₆ bytes of machine language.

The next line (line 33) has the machine language code 1B22₁₆ which represents the SR instruction. As an RR instruction, the format consists of one byte (2 hex digits) containing the opcode and one byte containing the operands. The opcode is 1B as determined from the listing of instructions in Table 40.

With regard to the second byte of the instruction (22₁₆), the first operand is designated by the first four bits and the second operand by the second four bits. Since a hex digit corresponds to four bits, the first hex digit (2) is the first operand and the second hex digit (2) is the second operand. Hence, the code 1B22₁₆ is the machine language result for SR R2,R2.

Since all RR instructions are two bytes in length, the location counter advances by 2 from 72₁₆ to 74₁₆.

The next instruction is A R2,ONE which says to fetch the 4 bytes beginning at the label ONE and add them to the 4 bytes in register R2, leaving the result in R2. The Add instruction is an RX instruction and, as is the case with nearly all RX instructions (except the BC), has the format shown in section 6.7.2 above (the BC has a mask where R1 normally appears).

From the Add instruction we get the hexadecimal machine language code of 5A20D0B0₁₆. The first byte (5A) is the opcode. The next byte contains the first operand (R2) and the index register (R0). The third byte contains the base register (D₁₆ or R13) and the first 4 bits of the displacement (0). The full displacement is 0B0₁₆ or 176₁₀.

The fully explicit notation for the Add would correspond to:

    A R2,176(R0,R13)

Because we specified the second operand with the label ONE, the assembler has calculated that the address of ONE is at a displacement of B0₁₆ (leading zero omitted) relative to the contents of register 13. This means that, when the program runs, the address of ONE will be the sum of the contents of R13 plus B0₁₆ (176₁₀).

So the question becomes, what's in R13? If you look at the location counter you will see that ONE is at location B8₁₆ from the start of the program but the displacement of ONE, relative to the contents of R13, is B0₁₆. Thus, R13 must have 8 in it!

When we assemble our programs we do not know where in memory they will be placed. So, instead, the assembler tabulates addresses as though programs were all loaded at location zero. When the program runs, the first byte of our program will be located at an actual run time address which will not be zero. (In fact, the emulator makes it appear that our programs are always loaded at runtime at address location 8000₁₆.)

During the first few instructions of our program when our program actually runs, the SUBENTRY macro determines where in memory our program actually is located and sets the base register (R13) accordingly. This can be seen in Figure 3. It shows the expansion of the SUBENTRY macro.

Several things happen in Figure 3. First, the BAL on line 4, loads R15 with the updated address portion of the PSW. This is the actual run time address of the eighth byte of the program. On line 11, the LR instruction copies this value from R15 to R13. Note: system macros use ordinary numbers for the registers, not numbers preceded by the letter R. The USING tells the assembler that R13 is our base register.

Thus, when the program runs, R13 has the actual, real live address of the eighth byte of our program. Because R13 is designated as the base register (line 12 in Figure 3), the assembler calculates all displacements relative to byte 8 which at run time is 8008₁₆ (in the emulator). Thus, if a label is 100 bytes from byte 8 in the assembler location counter listing, it will be 100 bytes from 8008₁₆ at run time.

As noted, the assembler uses R13 as the base register due to the USING on line 12 in Figure 3. USING is an assembler directive that does not generate code but tells the assembler which register to use as a base register and where the base register is pointing. In this case, it tells the assembler that R13 is pointing at HELLO+8, the eighth byte of the program. Since the SUBENTRY macro will always expand the same way in each program (except for the program name and date time stamp), if we use SUBENTRY, R13 will always be our base register, it will always point to the eighth byte of the program, and all displacements relative to the base register will be eight less than the location counter value for the label. SUBENTRY is not the only entry macro. Others may be used which could establish a different base register.

Thus, the assembler, knowing that R13 can be used as a base register and that it is pointing 8 bytes into the program, seeing the label ONE in the Add instruction, calculates, correctly, that the label is at B0₁₆ or 176₁₀ bytes from the 8th byte of the program. Thus we see a displacement of 0B0₁₆ and a base register of R13 in the machine code.

The index register in the Add instructions in Figure 4 are all specified as R0. When R0 is used in an addressing context, it means no register. There is an R0 and you can use it for arithmetic but if you use it in an address, it means no value is contributed regardless of the actual value in R0. Normally, the index register in an address will be R0 unless you explicitly tell the assembler to use it.
