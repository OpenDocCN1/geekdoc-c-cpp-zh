pletron’s memory may contain an instruction, a data value used by a program or an unused (and hence undefined) area of memory. The first two digits of each SML instruction are the *operation code* that specifies the operation to be performed. SML operation codes are shown in Fig. 8.23.

The last two digits of an SML instruction are the *operand*—the address of the memory location containing the word to which the operation applies.

| Operation code | Meaning |
|---|---|
| *Input/output operations* | |
| `const int READ = 10;` | Read a word from the keyboard into a specific location in memory. |
| `const int WRITE = 11;` | Write a word from a specific location in memory to the screen. |
| *Load and store operations* | |
| `const int LOAD = 20;` | Load a word from a specific location in memory into the accumulator. |
| `const int STORE = 21;` | Store a word from the accumulator into a specific location in memory. |
| *Arithmetic operations* | |
| `const int ADD = 30;` | Add a word from a specific location in memory to the word in the accumulator (leave result in accumulator). |
| `const int SUBTRACT = 31;` | Subtract a word from a specific location in memory from the word in the accumulator (leave result in accumulator). |
| `const int DIVIDE = 32;` | Divide a word from a specific location in memory into the word in the accumulator (leave result in accumulator). |
| `const int MULTIPLY = 33;` | Multiply a word from a specific location in memory by the word in the accumulator (leave result in accumulator). |
| *Transfer-of-control operations* | |
| `const int BRANCH = 40;` | Branch to a specific location in memory. |
| `const int BRANCHNEGATIVE = 41;` | Branch to a specific location in memory if the accumulator is negative. |
| `const int BRANCHZERO = 42;` | Branch to a specific location in memory if the accumulator is zero. |
| `const int HALT = 43;` | Halt—the program has completed its task. |

**Fig. 8.23** | Simpletron Machine Language (SML) operation codes.

Now let’s consider two simple SML programs. The first (Fig. 8.24) reads two numbers from the keyboard and computes and prints their sum. The instruction +1007 reads the first number from the keyboard and places it into location 07 (which has been initialized to zero). Instruction +1008 reads the next number into location 08. The *load* instruction, +2007, places (copies) the first