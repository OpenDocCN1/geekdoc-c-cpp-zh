
![](img/57c0d966bb33c67a5a188e6bf39e4e02_27_0.png)

**Figure 1.8:** CPU accessing RAM

![](img/57c0d966bb33c67a5a188e6bf39e4e02_27_1.png)

**Figure 1.9:** CPU accessing the file

![](img/57c0d966bb33c67a5a188e6bf39e4e02_27_2.png)

**Figure 1.10:** Uncommitted writes done to the file

![](img/57c0d966bb33c67a5a188e6bf39e4e02_28_0.png)

When we save the file using the ‘save’ command (a command of the operating system), the operating system copies the file from RAM back to the hard disk. This ensures that the file in the hard disk gets modified with the recent data as shown in Figure 1.11. Therefore, when we open the file next time, new changes will be reflected in the file. However, if we do not ‘save’ the file, which was modified by the CPU in the RAM space, then any changes made to the file in RAM will not be copied to the hard disk and hence the file in the hard disk will not be modified. Therefore, when we ‘open’ the file next time, we will see the older version of the file. This means that all the uncommitted writes to the file will be lost as the file in the hard disk was never modified with the updates made by the CPU in RAM. In summary, every program that is ‘opened’ for execution at a particular instant of time must be brought into the RAM space; whereas, every program that is ‘inactive’ or ‘closed’ can be present in the secondary memory or hard disk. Therefore, a hard disk memory is typically very large in size when compared to the RAM space of the computer system (the size of the hard disk is specified in gigabytes whereas the size of RAM is specified in megabytes as a part of computer system configuration).

## 1.3 C/C++ Development Environment

So as to fully translate the high-level language into the machine language, every C/C++ program has to go through the set of system programs before the machine can execute the code to generate the required output. The list of system programs involved in the process of translating the high-level language into a low-level language is as given below:

- 1. Editor
- 2. Pre-processor
- 3. Compiler
- 4. Linker
- 5. Loader

### 1.3.1 Editor

Editor provides an integrated development environment (IDE) to create and develop a C/C++ program. An editor is a system program that provides the programmer with multiple menu options so as to facilitate creation and maintenance of a software project. Some of the key facilities provided by editor include:

- 1. Creation of a new program
- 2. Editing an existing program
- 3. Debugging of a program
- 4. Initiate compilation and execution of the program

In summary, an editor is a system software using which we can create and save a C/C++ file on the disk. A C++ file which contains the source code is generally saved with an extension as `.cpp` on the hard disk. (C program file has an extension `.c`.) Figure 1.12 shows a screen shot of a Turbo C/C++ editor, which is available in the DOS mode. The detailed description of all the menu options provided by the editor is out of the scope of this text book.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_29_0.png)

### 1.3.2 Pre-processor

We can give an abbreviation for group of instructions to be executed in a C/C++ program. Such an abbreviation is called as a *macro*. The macro facility enables us to attach a name with the sequence of instructions, which are to be executed repeatedly in the program. The advantage of such naming is that we can now use a name of a macro each time we need to execute the sequence of instructions instead of actually typing the same instructions again and again in the program.

A *macro pre-processor* is a system program that resolves the macro references by substituting a ‘macro name’ with its ‘definition’. All the macro references made by the programmer in the source code will actually be substituted by the sequence of instructions and the data which are defined by the macro. The pre-processor runs just before the compilation of the program starts. Hence, the compiler will not see any abbreviations or macros because they would already be expanded by pre-processor before the compilation of the code kicks off. The pre-processor creates a file without macros on the disk which is used by the compiler for the translation of the code as shown in Figure 1.13.

The instructions within the program that are understood by the pre-processor are called as *pre-processor directives*. The pre-processor directives are generally prefixed by a symbol # in C/C++. Some of the pre-processor directives are:

- 1. `#include` – The directive is used to include a header file in the C/C++ program.
- 2. `#define` – The pre-processor directive is used to define macros in the C/C++ program.

We will discuss the details of these directives in Chapter 2 of this text book.

### 1.3.3 Compiler

- 1. Syntax analysis: The component inside the compiler that validates the syntax of the program is called a parser. The parser will throw an 'error' message to the programmer if any of the syntax rules are violated. The translation process is immediately terminated if at least one error is located in the input program. Every programming language has a grammar, which defines the syntactical rules of that language. A parser is a program that checks if the input sentence preserves the syntactical rules, which are defined by the grammar of the language, thereby detecting syntax errors (if any) in the source code. So as to examine the sentence for syntax errors, the compiler partitions the sentence into discrete tokens. The process of partitioning a single sentence into separate tokens is called 'lexical analysis', which happens before the 'syntax analysis' phase of the compilation process.
- 2. Semantic analysis: The phase is used to check the input program for semantic errors. The semantic rules define the 'data types' over which a specific operation can be performed. The semantic phase will throw an error and stop the translation process if there is a 'data type' mismatch while performing an operation. We discuss the details of 'data types' and operations in Chapters 2 and 3 of this text book.
- 3. Code generation: Once the syntax and semantic analyses are completed successfully, the code generation phase generates the optimized object code (which is the machine language) on the disk. The object code for the program is created and stored as an '.obj' file on the disk.

The total time required for the compilation of the source code so as to generate the object file is often referred to as 'compile time' of the program.

### What is Lexical analysis?

Before initiating translation, the compiler needs to ensure that the programmer has not violated any of the syntactical rules which are defined by the language. To check the syntax of each of the statements written by the programmer, the compiler needs to split each statement into different tokens. A token is the smallest indivisible part of each statement. For example, if the value of z is to be calculated as the addition of x and y, the statement must be written as:

```c
z = x+y;
```

This statement has 6 different tokens: z, =, x, +, y and ;. Splitting of this statement into different tokens is as shown below.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_31_0.png)

This process of splitting an instruction into a set of tokens is called lexical analysis. The syntax analysis phase now determines if all the tokens are organized correctly in the statement. The syntax analysis will throw an error if there is any incorrect formation of tokens detected in a particular statement. For example, the following statement would result in a compilation error.

This is because it organizes the tokens incorrectly according to the syntax defined by the language. The syntax of C/C++ is such that the operator + must be written exactly in between the two operands x and y which are to be added. The compiler does not allow writing the symbol + at the right side (or left side) of both the operands whose values are to be added.

```c
z = x y+;
```

### 1.3.4 Linker

It is possible that the C/C++ program contains references to functions or data, which are actually defined in external libraries. These libraries can provide the definitions of the common functions or the data required throughout the development of the project, and hence the program may be required to refer to functions and data present in multiple such libraries. Creation and usage of libraries facilitate reusability of the code in the project. The object file generated by the compiler will contain certain ‘gaps’ due to such external references present in the source code. The ‘linker’ is a system program, which links the object code produced by the compiler with the object code for the external libraries by resolving all the external symbol references, thereby filling the gaps present in the object file. Once all the external references are resolved, the linker generates an executable code (which is named as an ‘.exe’ file) on the disk as shown in Figure 1.13.

### 1.3.5 Loader

The linker generates the executable code (.exe file) on the disk. Recall from Section 1.2.4 that CPU cannot make a direct access to the code present in the hard disk. Therefore, the executable code must be first placed in RAM. A loader is the system program that loads the executable code in the main memory of the computer system (in RAM) so that the code can be executed by the CPU.

After the code is loaded into RAM, the processor can start executing the program, thereby generating the output. The time required to execute the ‘executable code’ of the program is often referred to as the ‘run time’ of the program.

## 1.4 Evolution of Programming Languages

Along with the growth in hardware systems, the features provided by the programming languages are also being enhanced with time. In general, the computer programming paradigms can be categorized as ‘structured programming’ and ‘object-oriented programming’. The type of the programming style to be used is dependent on the type of the application to be developed. In this section, we understand the difference between a ‘structured programming’ paradigm and an ‘object-oriented programming’ paradigm.
