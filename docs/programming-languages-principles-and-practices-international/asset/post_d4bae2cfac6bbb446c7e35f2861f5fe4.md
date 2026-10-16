
```
0010001000000100
0010010000000100
0001011001000010
0011011000000011
1111000000100101
0000000000000101
0000000000000110
0000000000000000
```

Figure 1.2 A machine language program

In this program, each line of code contains 16 bits or binary digits. A line of 16 bits represents either a single machine language instruction or a single data value. The last three lines of code happen to represent data values—the integers 5, 6, and 0—using 16-bit twos complement notation. The first five lines of code represent program instructions. Program execution begins with the first line of code, which is fetched from memory, decoded (interpreted), and executed. Control then moves to the next line of code, and the process is repeated, until a special halt instruction is reached.

To decode or interpret an instruction, the programmer (and the hardware) must recognize the first 4 bits of the line of code as an opcode, which indicates the type of operation to be performed. The remaining 12 bits contain codes for the instruction’s operands. The operand codes are either the numbers of machine registers or relate to the addresses of other data or instructions stored in memory. For example, the first instruction, 0010001000000100, contains an opcode and codes for two operands. The opcode 0010 says, “copy a number from a memory location to a machine register” (machine registers are high-speed memory cells that hold data for arithmetic and logic computations). The number of the register, 001, is found in the next 3 bits. The remaining 9 bits represent an integer offset from the address of the next instruction. During instruction execution, the machine adds this integer offset to the next instruction’s address to obtain the address of the current instruction’s second operand (remember that both instructions and data are stored in memory). In this case, the machine adds the binary number 100 (4 in binary) to the number 1 (the address of the next instruction) to obtain the binary number 101 (5 in binary), which is the address of the sixth line of code. The bits in this line of code, in turn, represent the number to be copied into the register.

We said earlier that execution stops when a halt instruction is reached. In our program example, that instruction is the fifth line of code, 1111000000100101. The halt instruction prevents the machine from continuing to execute the lines of code below it, which represent data values rather than instructions for the program.

As you might expect, machine language programming is not for the meek. Despite the improvement on the earlier method of reconfiguring the hardware, programmers were still faced with the tedious and error-prone tasks of manually translating their designs for solutions to binary machine code and loading this code into computer memory.

## 1.1.2 Assembly Language, Symbolic Codes, and Software Tools

The early programmers realized that it would be a tremendous help to use mnemonic symbols for the instruction codes and memory locations, so they developed assembly language for this purpose.

This type of language relies on software tools to automate some of the tasks of the programmer. A program called an assembler translates the symbolic assembly language code to binary machine code. For example, let’s say that the first instruction in the program of Figure 1.2 reads:

```
LD R1, FIRST
```

in assembly language. The mnemonic symbol LD (short for “load”) translates to the binary opcode 0010 seen in line 1 of Figure 1.2. The symbols R1 and FIRST translate to the register number 001 and the data address offset 000000100, respectively. After translation, another program, called a loader, automatically loads the machine code for this instruction into computer memory.

Programmers also used a pair of new input devices—a keypunch machine to type their assembly language codes and a card reader to read the resulting punched cards into memory for the assembler. These two devices were the forerunners of today’s software text editors. These new hardware and software tools made it much easier for programmers to develop and modify their programs. For example, to insert a new line of code between two existing lines of code, the programmer now could put a new card into the keypunch, enter the code, and insert the card into the stack of cards at the appropriate position. The assembler and loader would then update all of the address references in the program, a task that machine language programmers once had to perform manually. Moreover, the assembler was able to catch some errors, such as incorrect instruction formats and incorrect address calculations, which could not be discovered until run time in the pre-assembler era.

Figure 1.3 shows the machine language program of Figure 1.2 after it has been “disassembled” into the LC-3 assembly language. It is now possible for a human being to read what the program does. The program adds the numbers in the variables FIRST and SECOND and stores the result in the variable SUM. In this code, the symbolic labels FIRST, SECOND, and SUM name memory locations containing data, the labels R1, R2, and R3 name machine registers, and the labels LD, ADD, ST, and HALT name opcodes. The program is also commented (the text following each semicolon) to clarify what it does for the human reader.

```
.ORIG x3000      ; Address (in hexadecimal) of the first instruction
LD  R1, FIRST    ; Copy the number in memory location FIRST to register R1
LD  R2, SECOND   ; Copy the number in memory location SECOND to register R2
ADD R3, R2, R1   ; Add the numbers in R1 and R2 and place the sum in
                 ; register R3
ST  R3, SUM      ; Copy the number in R3 to memory location SUM
HALT             ; Halt the program
FIRST .FILL #5   ; Location FIRST contains decimal 5
SECOND .FILL #6  ; Location SECOND contains decimal 6
SUM   .BLKW #1   ; Location SUM (contains 0 by default)
.END             ; End of program
```

Figure 1.3 An assembly language program that adds two numbers

Although the use of mnemonic symbols represents an advance on binary machine codes, assembly language still has some shortcomings. The assembly language code in Figure 1.3 allows the programmer to represent the abstract mathematical idea, “Let FIRST be 5, SECOND be 6, and SUM be FIRST + SECOND” as a sequence of human-readable machine instructions. Many of these instructions must move

data from variables/memory locations to machine registers and back again, however; assembly language lacks the more powerful abstraction capability of conventional mathematical notation. An **abstraction** is a notation or way of expressing ideas that makes them concise, simple, and easy for the human mind to grasp. The philosopher/mathematician A. N. Whitehead emphasized the power of abstract notation in 1911: “By relieving the brain of all unnecessary work, a good notation sets it free to concentrate on more advanced problems.… Civilization advances by extending the number of important operations which we can perform without thinking about them.” In the case of assembly language, the programmer must still do the hard work of translating the abstract ideas of a problem domain to the concrete and machine-dependent notation of a program.

A second major shortcoming of assembly language is due to the fact that each particular type of computer hardware architecture has its own machine language instruction set, and thus requires its own dialect of assembly language. Therefore, any assembly language program has to be rewritten to port it to different types of machines.

The first assembly languages appeared in the 1950s. They are still used today, whenever very low-level system tools must be written, or whenever code segments must be optimized by hand for efficiency. You will likely have exposure to assembly language programming if you take a course in computer organization, where the concepts and principles of machine architecture are explored.

## 1.1.3 FORTRAN and Algebraic Notation

Unlike assembly language, high-level languages, such as C, Java, and Python, support notations closer to the abstractions, such as algebraic expressions, used in mathematics and science. For example, the following code segment in C or Java is equivalent to the assembly language program for adding two numbers shown earlier:

```
```c
int first = 5;
int second = 6;
int sum = first + second;
```
```

One of the precursors of these high-level languages was FORTRAN, an acronym for FORmula TRANslation language. John Backus developed FORTRAN in the early 1950s for a particular type of IBM computer. In some respects, early FORTRAN code was similar to assembly language. It reflected the architecture of a particular type of machine and lacked the structured control statements and data structures of later high-level languages. However, FORTRAN did appeal to scientists and engineers, who enjoyed its support for algebraic notation and floating-point numbers. The language has undergone numerous revisions in the last few decades, and now supports many of the features that are associated with other languages descending from its original version.

## 1.1.4 The ALGOL Family: Structured Abstractions
and Machine Independence

Soon after FORTRAN was introduced, programmers realized that languages with still higher levels of abstraction would improve their ability to write concise, understandable instructions. Moreover, they wished to write these high-level instructions for different machine architectures with no changes. In the late 1950s, an international committee of computer scientists (which included John Backus) agreed on
