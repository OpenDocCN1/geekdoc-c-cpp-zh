
```cpp
// Ex. 8.13: ex08_13.cpp
// What does this program do?
#include <iostream>
using namespace std;

void mystery1(char*, const char*); // prototype

int main() {
    char string1[80];
    char string2[80];

    cout << "Enter two strings: ";
    cin >> string1 >> string2;
    mystery1(string1, string2);
    cout << string1 << endl;
}

// What does this function do?
void mystery1(char* s1, const char* s2) {
    while (*s1 != '\0') {
        ++s1;
    }

    for (; (*s1 = *s2); ++s1, ++s2) {
        ; // empty statement
    }
}
```

**Fig. 8.19 What does this program do?**

- 8.14 **(What Does This Code Do?)** What does this program do?

```cpp
// Ex. 8.14: ex08_14.cpp
// What does this program do?
#include <iostream>
using namespace std;

int mystery2(const char*); // prototype

int main() {
   char string1[80];

   cout << "Enter a string: ";
   cin >> string1;
   cout << mystery2(string1) << endl;
}

// What does this function do?
int mystery2(const char* s) {
   unsigned int x;

   for (x = 0; *s != '\0'; ++s) {
      ++x;
   }

   return x;
}
```

**Fig. 8.20 What does this program do?**

## Special Section: Building Your Own Computer

In the next several problems, we take a temporary diversion away from the world of high-level-language programming. We “peel open” a simple hypothetical computer and look at its internal structure. We introduce machine-language programming and write several machine-language programs. To make this an especially valuable experience, we then build a computer (using software-based *simulation*) on which you can execute your machine-language programs!²

- 2. In Exercises 19.30–19.34, we’ll “peel open” a simple hypothetical compiler that will translate statements in a simple high-level language to the machine language you use here. You’ll write programs in that high-level language, compile them into machine language and run that machine language on your computer simulator.

- 8.15 **(Machine-Language Programming)** Let’s create a computer we’ll call the Simpletron. As its name implies, it’s a simple machine, but, as we’ll soon see, it’s a powerful one as well. The Simpletron runs programs written in the only language it directly understands, that is, Simpletron Machine Language, or SML for short.

The Simpletron contains an *accumulator*—a “special register” in which information is put before the Simpletron uses that information in calculations or examines it in various ways. All information in the Simpletron is handled in terms of *words*. A word is a signed four-digit decimal number, such as `+3364`, `−1293`, `+0007`, `−0001`, etc. The Simpletron is equipped with a 100-word memory, and these words are referenced by their location numbers `00`, `01`, ..., `99`.

Before running an SML program, we must *load*, or place, the program into memory. The first instruction (or statement) of every SML program is always placed in location `00`. The simulator will start executing at this location.

Each instruction written in SML occupies one word of the Simpletron’s memory; thus, instructions are signed four-digit decimal numbers. Assume that the sign of an SML instruction is always plus, but the sign of a data word may be either plus or minus. Each location in the Simpletron’s memory may contain an instruction, a data value used by a program or an unused (and hence undefined) area of memory. The first two digits of each SML instruction are the *operation code* that specifies the operation to be performed. SML operation codes are shown in **Fig. 8.21**.

**Fig. 8.21 Simpletron Machine Language (SML) operation codes.**

| Operation code | Meaning |
|---|---|
| *Input/output operations* | |
| 10 | Read a word from the keyboard into a specific location in memory. |
| 11 | Write a word from a specific location in memory to the screen. |
| *Load and store operations* | |
| 20 | Load a word from a specific location in memory into the accumulator. |
| 21 | Store a word from the accumulator into a specific location in memory. |
| *Arithmetic operations* | |
| 30 | Add a word from a specific location in memory to the word in the accumulator (leave result in accumulator). |
| 31 | Subtract a word from a specific location in memory from the word in the accumulator (leave result in accumulator). |
| 32 | Divide a word from a specific location in memory into the word in the accumulator (leave result in accumulator). |
| 33 | Multiply a word from a specific location in memory by the word in the accumulator (leave result in accumulator). |
| *Transfer-of-control operations* | |
| 40 | Branch to a specific location in memory. |
| 41 | Branch to a specific location in memory if the accumulator is negative. |
| 42 | Branch to a specific location in memory if the accumulator is zero. |
| 43 | Halt—the program has completed its task. |

The last two digits of an SML instruction are the *operand*—the address of the memory location containing the word to which the operation applies.

Now let’s consider two simple SML programs. The first (**Fig. 8.22**) reads two numbers from the keyboard and computes and displays their sum. The instruction `+1007` reads the first number from the keyboard and places it into location `07` (which has been initialized to zero). Instruction `+1008` reads the next number into location `08`. The *load* instruction, `+2007`, places (copies) the first number into the accumulator, and the *add* instruction, `+3008`, adds the second number to the number in the accumulator. *All SML arithmetic instructions leave their results in the accumulator.* The store instruction, `+2109`, places (copies) the result back into memory location `09`. Then the *write* instruction, `+1109`, takes the number and displays it (as a signed four-digit decimal number). The *halt* instruction, `+4300`, terminates execution.

**Fig. 8.22 SML Example 1.**

| Location | Number | Instruction |
|---|---|---|
| 00 | +1007 | (Read A) |
| 01 | +1008 | (Read B) |
| 02 | +2007 | (Load A) |
| 03 | +3008 | (Add B) |
| 04 | +2109 | (Store C) |
| 05 | +1109 | (Write C) |
| 06 | +4300 | (Halt) |
| 07 | +0000 | (Variable A) |
| 08 | +0000 | (Variable B) |
| 09 | +0000 | (Result C) |

The SML program in **Fig. 8.23** reads two numbers from the keyboard, then determines and displays the larger value. Note the use of the instruction `+4107` as a conditional transfer of control, much the same as C++’s `if` statement.

**Fig. 8.23 SML Example 2.**

| Location | Number | Instruction |
|---|---|---|
| 00 | +1009 | (Read A) |
| 01 | +1010 | (Read B) |
| 02 | +2009 | (Load A) |
| 03 | +3110 | (Subtract B) |
| 04 | +4107 | (Branch negative to 07) |
| 05 | +1109 | (Write A) |
| 06 | +4300 | (Halt) |
| 07 | +1110 | (Write B) |
| 08 | +4300 | (Halt) |
| 09 | +0000 | (Variable A) |
| 10 | +0000 | (Variable B) |

Now write SML programs to accomplish each of the following tasks:

- A. Use a sentinel-controlled loop to read positive numbers and compute and display their sum. Terminate input when a negative number is entered.
- B. Use a counter-controlled loop to read seven numbers, some positive and some negative, and compute and display their average.
- C. Read a series of numbers, and determine and display the largest number. The first number read indicates how many numbers should be processed.

### 8.16 *Computer Simulator*

It may at first seem outrageous, but in this problem you are going to build your own computer. No, you won’t be soldering components together. Rather, you’ll use the powerful technique of *software-based simulation* to create a *software model* of the Simpletron. Your Simpletron simulator will turn the computer you are using into a Simpletron, and you actually will be able to run, test and debug the SML programs you wrote in **Exercise 8.15**. When you run your Simpletron simulator, it should begin by displaying

```text
*** Welcome to Simpletron! ***

*** Please enter your program one instruction ***
*** (or data word) at a time. I will type the ***
*** location number and a question mark (?). ***
*** You then type the word for that location. ***
*** Type the sentinel -9999 to stop entering ***
*** your program. ***
```

Your program should simulate the Simpletron’s memory with a single-subscripted, 100-element built-in array `memory`. Now assume that the simulator is running, and let’s examine the dialog as we enter the program of the second example of **Exercise 8.15**:

```text
```
