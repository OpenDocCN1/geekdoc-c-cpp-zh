
to determine the operation and the address of the operand, fetch the operand, and then perform the required operation, using the ALU if necessary.

Programming in the machine language of an early computer was obviously a very difficult and time-consuming task in which errors were common. Only later did it become possible to write programs in **assembly language**, which uses mnemonics (names) in place of numeric opcodes and variable names in place of numeric addresses. For example, the preceding sequence of instructions might be written in assembly language as

1. LOAD a, ACC
2. MULT b, ACC
3. ADD c, ACC
4. STORE ACC, x

An assembler, which is part of the system software, translates such assembly language instructions into machine language.

```asm
LOAD a, ACC
MULT b, ACC
ADD c, ACC
STORE ACC, x
```

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_34_0.png)

Today, most programs are written in **high-level languages** such as C++ and Java. Such programs are known as **source programs**. The instructions that make up a source program must be translated into machine language before they can be executed. For some languages (e.g., C++), a **compiler** that translates the source program into an **object program** carries this out. For example, for the preceding problem, a programmer might write the C++ statement

```cpp
x = a * b + c;
```

which instructs the computer to multiply the values of a and b, add the value of c, and assign the value to x. A C++ compiler would translate this statement into a sequence of machine language instructions like those considered earlier.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_34_1.png)

For a complete program like those in the chapters that follow, the compiler will convert each C++ statement into machine language. A **linker** will then be used to connect items such as input/output libraries that are defined outside of the resulting object file with their definitions to produce an **executable program**, which can then be loaded into memory and executed by the computer to generate the output produced by the program.

## EXERCISES

1. Match each item in the first column with the associated item in the second column.

- _____ peripheral devices
- _____ bit
- _____ byte
- _____ megabyte
- _____ object program
- _____ source program
- _____ CPU
- _____ K
- _____ RAM
- _____ cache

- A. high-speed memory used by the CPU
- B. central processing unit
- C. 1024
- D. terminals, scanners, printers
- E. binary digit
- F. group of binary digits
- G. 1024 K bytes
- H. written in machine language
- I. written in high-level language
- J. language translator

Briefly define each of the terms in Exercises 2–16.

2. ALU
3. CPU
4. peripheral devices
5. bit
6. byte
7. word
8. K
9. megabyte
10. source program
11. object program
12. machine language
13. assembly language
14. compiler
15. assembler
16. interpreter

## Programming and Problem Solving—Software Engineering

- 2.1 A Sneak Peek at C++ 22
- 2.2 Programming and Problem Solving—An Overview 24
- Chapter Summary 34
- Test Yourself 35
- Exercises 35
- Programming Problems 36

> If we really understand the problem, the answer will come out of it, because the answer is not separate from the problem.
>
> JIDDU KRISHNAMURTI

> People always get what they ask for; the only trouble is that they never know, until they get it, what it actually is that they have asked for.
>
> ALDOUS HUXLEY

> It’s the only job I can think of where I get to be both an engineer and an artist. There’s an incredible, rigorous, technical element to it, which I like because you have to do very precise thinking. On the other hand, it has a wildly creative side where the boundaries of imagination are the only real limitation.
>
> ANDY HERTZFELD

### 2.1 A Sneak Peek at C++

A program is a collection of statements written in a programming language. In the same way that grammar rules dictate how to construct English sentences, there are C++ grammar rules that govern how C++ statements are formed and combined into more complex statements and into programs. Much of this text is devoted to learning these rules, and in this section we take a first look at a few of these in a simple C++ program.

It is traditional to use as a first example a program like the one in Example 2.1 that displays a greeting. The user is prompted to enter his or her first name and then a greeting is output. We will use this program to illustrate the basic structure of C++ programs.

**Example 2.1 Greeting a User**

```cpp
/* Program that greets the user.
    Written by John Doe for CS 104, Assignment 1, Feb. 2, 2012

    Input:  the name of the user
    Output: a personalized greeting
    ---------------------------------------------------------------*/

#include <iostream>      // cin, cout, <<, >>
#include <string>        // string
using namespace std;

int main()
{
    cout << "What is your first name? ";
    string firstName;
    cin >> firstName;

    cout << "\nWelcome to CS 104, " << firstName << "!\n";
}
```

**SAMPLE RUN:**

```
What is your first name? Sharlene ← user input
Welcome to CS 104, Sharlene!
```

The first line of the program begins with the pair of characters `/*` and the seventh line ends with the pair `*/`. In a C++ program, anything contained between these character pairs is a comment. This multiline comment in these opening lines of the program is opening documentation that gives information about the program such as what it does, who wrote it, when it was written (or last updated), and what is input to and output by the program. The dashes in the sixth line are optional and are used in the examples of this text as a border to set this opening documentation off from the program statements that follow.

The two lines that follow begin with `#include` and are called compiler directives. The first one instructs the compiler to add to the program the items in the library `iostream` that are needed to perform input and output; it will appear in all of our C++ programs. The second directive adds the items in the library `string` that are needed to process character strings. The `//` following each directive indicates that what follows to the end of the line is a comment. Here these comments indicate which items from the libraries are being used.

The next line `using namespace std;` will be present in nearly all of our programs. It informs the compiler that we want these to be the standard libraries from the namespace named `std`. Without it, we would have to qualify each library item (such as `cout`) with the prefix `std::`; for example:

```cpp
std::cout << "What is your first name? ";
```

However, this soon becomes annoying because the standard library identifiers such as `cin` and `cout` are used so frequently.

The rest of the program has the form

```cpp
int main()
{
    A list of C++ statements
}
```

This is actually a function named `main` and is called the main function of the program. The C++ keyword `int` preceding the word `main` specifies the return type of the function and indicates that it will return an integer value to the operating system. Normal termination is indicated by returning zero; nonzero return values indicate abnormal termination. Some programmers use (and some older compilers may require) a return statement `return 0;` as the last statement in the program.

Execution of this program will begin with the first statement enclosed between the curly braces (`{` and `}`) in this main function and proceed through the statements that follow it. Note that each statement must end with a semicolon.

In the program in Example 2.1, the `<<` operator in the first statement will output a message to the screen (`cout`) that prompts the user to enter her or his first name:

```cpp
cout << "What is your first name? ";
```

The next statement

```cpp
string firstName;
```

> 1 In 1997, the C++ ANSI standard gave new names to the standard libraries (e.g., `iostream` in place of `iostream.h`) and stored these names and others in containers called namespaces. The ANSI standard identifiers are stored in the namespace `std`. With non-ANSI-compliant compilers, it may be necessary to use the older library names (e.g., `iostream.h` instead of `iostream`, and `math.h` instead of `cmath`) and remove the `using namespace std;` line.
