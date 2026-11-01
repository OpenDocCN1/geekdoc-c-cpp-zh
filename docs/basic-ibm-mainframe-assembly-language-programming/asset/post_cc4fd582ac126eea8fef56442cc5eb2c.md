
which your machine language program is generated from, they do not themselves directly result in the generation of code or data. The main assembler directives we will use are shown in Table 9.

## 4. Macro statements

Macros are small, library resident code modules that contain segments of frequently used code. Rather than re-write the code anew each time, we direct the pre-processor to insert macros into our programs. From the program level, macros look very much like instructions. Internally, macros may contain instructions, data allocation statements and assembler calls as well as statements in the macro language itself. Before your program is seen by the assembler, it is first processed by the macro pre-processor.

| Directive | Description |
|---|---|
| CSECT | start or continue control section. |
| CNOP | align to a boundary. |
| DSECT | start or continuation of a dummy section. |
| ENTRY | define an entry point. |
| EJECT | skip to top of next page in listing. |
| END | end of the source module. |
| EQU | define one symbol to be the equivalent of another. |
| EXTERN | identify symbols defined in other modules. |
| LTORG | placement of literal pool. |
| ORG | adjust location counter. |
| PRINT | assembler print options. |
| SPACE | insert one line feed in listing output. |
| START | initiate first or only control section. |
| TITLE | set title to appear at top of listing page. |
| USING/DROP | designate/undesignate a base register. |

Table 9 Assembler Directives

### 4.4 Line Format and Naming Conventions

Historically, assembly language programs were punched on 80 column cards and followed a format consistent with that media. Although there has been some relaxation of the format in recent years, most assembly programmers follow the original format to this day.

- 1. Labels begin in column one and are from one to eight upper case characters in length.
- 2. The first character of a label is either a letter in the range A through Z, $ # or @.
- 3. Characters after the first character of a label may be any of the above as well as digits in the range 0 through 9.
- 4. The mnemonic (short abbreviation) for the operation code or assembly directive begins in column ten.
- 5. Operands, if any, begin in column sixteen and may not include embedded blanks except within quoted strings.
- 6. After the operands and one blank, comments may be written.
- 7. Comments and operands may not extend beyond column 71.
- 8. If column 1 is an asterisk, the remainder of the line is a comment.
- 9. If an operand is so long that it would extend beyond column 71, place a character (usually an X) in column 72 and continue the operand on column sixteen of the next line. There may be at most two continuation lines.
- 10. Blank lines are ignored.
- 11. Quoted strings use the single quote character, not the double quote. If you want a quoted string to contain single quote, it should be represented in the string as two immediately adjacent single quotes such as: 'Mike''s computer'.
- 12. If you use an ampersand as a character in a quoted string, you must use two immediately adjacent ampersands such as: 'computers && technology'

## 5. Hello World

### 5.1 The z390 Portable Mainframe Project

The examples in this book were developed using the z390 Portable Mainframe Assembler and Emulator. This is a Java based, GPL licensed project to "...Enable z390 and zcobol users to compile, assemble, link, and execute mainframe COBOL and assembler problem state programs with minimum source code changes using Windows, Linux, and other platforms supporting the J2SE runtime...." from the web site:

http://www.z390.org/

The emulator can be run either in a graphical user window or from a command prompt.

### 5.2 Hello World

Now it's time to write the customary Hello World program as shown in Figure 1.

The first few lines of every assembly program deal with assembler directives and linkage. Linkage refers to the process of connecting your program to the program that called it. It involves saving the calling program's registers so they can be restored at exit, establishing a base register for your program, and creating a save area in your program. These will each be discussed later in this book. Normally these actions are done with macros (macros are small, pre-written, disk resident, code modules) as they seldom differ from one program to the next.

The z390 emulator has a macro named SUBENTRY that establishes your program's linkage, its save area, and sets register 13 as your base register.

When you assemble a program, the assembler will generate a file showing your program and its translation to machine language along with other information. This is often referred to as the listing and, in the z390 emulator, will appear as a file with the same name as your program but with the .PRN file extension.

The directive PRINT NOGEN is a directive to the assembler that tells it to display the names of the macros but not show the macro expansion (code) itself in the listing. If PRINT NOGEN is omitted, the assembler will display the contents of the macro expansion which are usually not very interesting after you see them once.

The label on SUBENTRY is HELLO. The SUBENTRY macro uses this label to establish the external linkage name of your program. This is the name other programs would use if they were calling followed by its expansion. Code generated as a result of macro expansion is preceded by plus signs.

```
Label        Op-code       Operands

1 HELLO      SUBENTRY
2+HELLO      CSECT
3            STM           14,12,12(13)
4            BAL           15,104(15)
5            DC            18F'0'
6            DC            CL8'HELLO'
7            DC            CL8'09/06/10'
8            DC            CL8'19.02'
9            ST            15,8(13)
10           ST            13,4(15)
11           LR            13,15
12           USING         HELLO+8,13
14           EQUIREGS
15+R0        EQU           0
16+R1        EQU           1
17+R2        EQU           2
18+R3        EQU           3
19+R4        EQU           4
20+R5        EQU           5
21+R6        EQU           6
22+R7        EQU           7
23+R8        EQU           8
24+R9        EQU           9
25+R10       EQU           10
26+R11       EQU           11
27+R12       EQU           12
28+R13       EQU           13
29+R14       EQU           14
30+R15       EQU           15
33           XPRNT         MSG,L'MSG
34           SUBEXIT
35           LA            15,0
36           L             13,4(13)
37           L             14,12(13)
38           LM            2,12,28(13)
39           BR            14
41 MSG       DC            C'Hello World'
42           END
```

Figure 3 Macro Expansion

Lines 2 through 12 are the expansion of the SUBENTRY macro and, except for lines 2 and 12, are machine instructions and data allocations. Lines 15 through 30 are the result of the EQUIREGS macro and are assembler directives (i.e. not machine instructions or data declarations). Lines 35 through 39 are the result of the SUBEXIT macro and are machine instructions. Further details on the meaning of this code will be covered later. Lines 1, 14 and 34 are the macro invocations themselves that were originally present in the source code module. They are shown for reference purposes.

The left hand portion of the .PRN file (not shown) contains the translation of the program into hexadecimal and other information about the executable module. The left hand side is entirely in hexadecimal. The right hand side is text and numbers are normally in decimal notation with some exceptions. We will examine the left hand side of the page shortly.

### 5.5 Quick Overview of Assembly Language Programming

As we have seen, assembly language programs consist of sequences of instructions that operate on data. In a program, an instruction is written as one or more letters that are an abbreviation or other indicator of the instruction's name or function. These are referred to as mnemonics.

Each instruction in a program has one or more operands which designate the data on which the instructions operate. The operands specify the location of the data which can be in constants, registers, memory or all three.

Typical instructions involve mathematical operations (add, subtract, multiply, divide), logical operations on bits (AND, OR, Exclusive OR, etc.), data movement, and comparisons (is A greater than B?), and branch instructions (GOTOs).

In the IBM architecture, most instructions have two operands and the result of an operation is usually placed in the first operand. The second operand, in most cases, is unchanged.

In some instructions, both operands are in registers, in others the first operand is a register and the second is in memory and, in a few instructions, both operands are in memory. While most instructions have two operands, some have more. In some instructions, one or more operands are constants contained in the instruction itself.

Also, there are instructions to initiate and control input/output. These are normally only executed by the operating system.
