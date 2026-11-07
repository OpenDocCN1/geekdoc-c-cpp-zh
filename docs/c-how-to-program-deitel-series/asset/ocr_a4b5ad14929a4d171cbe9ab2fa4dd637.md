The Simpletron contains an *accumulator*—a “special register” in which information is put before the Simpletron uses that information in calculations or examines it in various ways. All information in the Simpletron is handled in terms of *words*. A word is a signed four-digit decimal number, such as +3364, -1293, +0007, -0001, etc. The Simpletron is equipped with a 100-word memory, and these words are referenced by their location numbers 00, 01, …, 99.

Before running an SML program, we must *load*, or place, the program into memory. The first instruction (or statement) of every SML program is always placed in location 00. The simulator will start executing at this location.

Each instruction written in SML occupies one word of the Simpletron’s memory; thus, instructions are signed four-digit decimal numbers. Assume that the sign of an SML instruction is always plus, but the sign of a data word may be either plus or minus. Each location in the Simpletron’s memory may contain an instruction, a data value used by a program or an unused (and hence undefined) area of memory. The first two digits of each SML instruction are the *operation code* that specifies the operation to be performed. SML operation codes are shown in Fig. 8.19.

| Operation code | Meaning |
|---|---|
| *Input/output operations* | |
| `const int read = 10;` | Read a word from the keyboard into a specific location in memory. |
| `const int write = 11;` | Write a word from a specific location in memory to the screen. |
| *Load and store operations* | |
| `const int load = 20;` | Load a word from a specific location in memory into the accumulator. |
| `const int store = 21;` | Store a word from the accumulator into a specific location in memory. |
| *Arithmetic operations* | |
| `const int add = 30;` | Add a word from a specific location in memory to the word in the accumulator (leave result in accumulator). |
| `const int subtract = 31;` | Subtract a word from a specific location in memory from the word in the accumulator (leave result in accumulator). |
| `const int divide = 32;` | Divide a word from a specific location in memory into the word in the accumulator (leave result in accumulator). |
| `const int multiply = 33;` | Multiply a word from a specific location in memory by the word in the accumulator (leave result in accumulator). |
| *Transfer-of-control operations* | |
| `const int branch = 40;` | Branch to a specific location in memory. |
| `const int branchnneg = 41;` | Branch to a specific location in memory if the accumulator is negative. |
| `const int branchzero = 42;` | Branch to a specific location in memory if the accumulator is zero. |
| `const int halt = 43;` | Halt—the program has completed its task. |

**Fig. 8.19** | Simpletron Machine Language (SML) operation codes.