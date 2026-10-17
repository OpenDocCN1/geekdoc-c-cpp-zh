**Table 1.2 C++ Data Types and Domain Range**

| Data Type | Bytes | Range |
|---|---:|---|
| int | 4 | -2,147,483,648 to 2,147,483,647 |
| Short int | 2 | 32,768 to 32,767 |
| Long int | 4 | -2,147,483,648 to 2,147,483,647 |
| Unsigned int | 4 | 0 to 4,294,967,295 |
| Signed char | 1 | -128 to 127 |
| Unsigned char | 1 | 0 to 255 |
| float | 4 | ±3.4E-38 and ±3.4E38 |
| double | 8 | ±1.7E-308 and ±1.7E308 |
| Long double | 12 | ±1.7E-308 and ±1.7E308 |

# ## 1.5 C++ Execution Flow

Let’s talk about a few basic terms before we move on:

+   - *Machine code* are instructions that only the computer understands, written in binary (0,1), and can be directly executed by a CPU.
+   - *Assembly code* is a low-level language consisting of statements written in English that can be understood by the programmer.
+   - *Debugging* means finding the faults or errors in your program to fix them so the program executes correctly.

A program in C++ executes in four stages, where different tools help us to make the execution process easier:

+   1. *Pre-processor*
+   
+      The first event that occurs in a C++ program is that the pre-processor processes the program before compilation. It includes the header files and any macros, if defined. It prepares the source code for the later stages of execution.
+   
+   2. *Compiler*
+   
+      Now the pre-processed source code passes through the compiler to produce an object file. The compiler translates the programming language code in C++ into the machine language, and checks for any errors, issuing warnings about the errors. The object file contains the assembly code.
+   
+   3. *Linker*
+   
+      The linker connects the libraries and object files together to generate an executable file with the extension .exe.