
![](img/d75612dcf3ab36327142238ab5bb21d8_148_0.png)

**FIGURE 4.1** The Life Cycle of a C Program

### 4.2.2 Editing the Program

Before writing a program, you need to first identify its input and output and then develop the program logic. Once you have the algorithm or flowchart ready, key in the source code using an editing software. This editor may be provided by the operating system or it may be a component of the compiling software. Save the code in a file having the .c extension using a meaningful name (like `celsius2fahrenheit.c` instead of names like `a.c` or `foo.c`).

For a program to compile successfully, its source code must be *syntactically* correct, i.e. it must conform to the rules of the language. Make a small mistake (like dropping the `;` in a C statement) and your program will refuse to compile. Every time one or more errors are generated, you have to re-invoke the editor to carry out the changes. The file containing the source code must be backed up to allow for future modifications. If you lose this file, you cannot reverse-engineer the machine code to retrieve the source code.

### 4.2.3 The Three-Phase Compilation Process

As just noted, a C program depends on information maintained externally, so the compilation procedure in C is somewhat different from other languages. Compilation in C is a three-step process that involves the use of three separate programs:

- The *Preprocessor* — This program acts on lines that begin with a `#`. They occur mostly at the beginning of a program and are called *preprocessor directives*. A directive may insert the contents of a header file at that location (like `#include <stdio.h>`) or perform a substitution (like `#define PI 3.142`) in the program itself. The preprocessor thus *modifies* the source code to make it suitable for use in the next phase. This modification is carried out on a copy; the original file containing the source code is left undisturbed.
- The *Compiler* — This program checks the source code after it has been modified by the preprocessor. If the compiler detects one or more syntax errors in this code, it displays them and stops further processing. Otherwise, the compiler creates intermediate *object code*. This code is incomplete and not ready to run because it doesn’t contain the code for the standard C functions (like `printf` and `scanf`). The compiler merely leaves *unresolved references* to these functions (3.15).
- The *Linker* — This program acts on the unresolved references left behind by the compiler. The linker does this by adding the machine code of functions available in separate libraries to the object code created by the compiler. The resultant code is a standalone executable that is run by the program loader. *The linker fills the holes left by the compiler.*

Even though every C distribution contains the three programs, they may or may not be invoked separately (unless you are handling an application that comprises multiple programs). Generally, these programs are invoked by one principal program, but it will stop in its tracks if it encounters syntax errors in the source code. For instance, the linker won’t be invoked if the compiler detects syntax errors, which means that the executable won’t be created. If that happens, you have to edit the source file and repeat this three-phase cycle.

Does the compiler directly translate the source code to machine code? Some compilers (like the Linux GCC compiler) find it more convenient to perform translation to assembly language first. A separate program (the *assembler*) then converts the assembly language code to machine code. The intermediate file is removed once the final machine code is created. However, GCC also supports an option that retains the assembly code for use by assembly language programmers.

![](img/d75612dcf3ab36327142238ab5bb21d8_150_0.png)

> **Note:** The term *compiler* is used in two ways in C. It could mean the program that does the job specified in the second phase, or represent a collective term that performs all of the three tasks. The true meaning should be evident from the context, but when it is not, we’ll use the term *compiling software* to refer to the collective meaning.

### 4.2.4 Executing the Program

The default name of the standalone executable is system-dependent—**a.out** on UNIX/Linux systems, and **aout.exe** or **AOUT.EXE** on Windows. (Visual Studio names the executable after the source file, so **foo.c** is compiled to **foo.exe**.) This file can be executed by running ./a.out from the operating system’s shell. If you are using C in a GUI environment (like Visual Studio), you have to use the mouse to select menu options that perform all of the compilation and execution tasks.

It is possible for a program to pass the compilation and linking phases and still fail in execution. Programs fail at *runtime* (i.e., when the program is actually run) on account of *semantic errors* that arise out of mistakes in design. For instance, a division by zero makes the program abort with an error. Use of = instead of == will also yield unexpected results. Faulty logic that doesn’t account for all possibilities can make a program behave erratically as well. The solution is the same: edit the source code and repeat the compilation process before re-execution.

You might argue that if the contents of **stdio.h** are made available by a simple **#include** directive, why not a value (like 3.142 or PI) that is required by multiple programs involving circles? That’s right, C doesn’t encourage you to store the value of PI in every program that computes the area of a circle. You can keep this information in a header file and include it as well.

![](img/d75612dcf3ab36327142238ab5bb21d8_150_1.png)

> **Takeaway:** A program can have syntax errors (on account of wrong use of its grammar) or semantic errors (because of faulty program logic). The former is detected during compilation and the latter during program execution.

## 4.3 KNOW YOUR C COMPILING SOFTWARE

Before you start writing programs, you need to be familiar with the C compiling software (the entire set of programs) installed on your system. Over the years, the footprint of this software has grown in both size and convenience to provide a complete programming environment. This environment generally comprises the following components:

- The main programs—the preprocessor, compiler and linker.
- The standard header files interpreted by the preprocessor.
- The standard library containing the object code of all functions that are part of ANSI C (like `printf`).
- An editor to edit programs and header files.
- A debugger to locate semantic (runtime) errors in programs.

Compiling software is available in both CUI and GUI flavors. Command-line or CUI systems offer separate programs for editing, processing and debugging. These programs are invoked by name and they support several *options* or *switches* that change their default behavior. We won’t need to use these options in this book though (except in Chapter 17).

GUI-based systems offer an *Integrated Development Environment (IDE)* where all actions are invoked by the point-and-click mechanism of the mouse. IDEs are menu-based which dispenses with the need to invoke commands by name. Under the hood, however, these mouse clicks internally invoke standalone programs. Generally, IDE systems also offer a CUI mode for those (this author included) who prefer to invoke commands by name.

### 4.3.1 GCC (Linux)

Linux systems support a CUI system called GCC, the free-to-use package from GNU. It is shipped with every Linux distribution but may not be installed by default. It comprises the following standalone programs: **gcc** (compiler), **cpp** (preprocessor), **ld** (linker) and **gdb** (debugger). GCC doesn’t offer an editor, but Linux supports two powerful editors that are used by most people: **vim** and **emacs**. To check whether GCC is installed on your system, run the **gcc** command from a shell:

```
$ gcc
gcc: no input files
```

> The $ signifies the shell prompt
> gcc exists

This message from the **gcc** compiler points out that a filename needs to be specified. If the GCC package is not installed, you’ll get the message `gcc: command not found`. **gcc** also acts as a frontend to **cpp** and **ld**, so you don’t normally have to bother about running the preprocessor and linker separately. By default **gcc** creates the executable **a.out** which has to be executed as **./a.out**.

### 4.3.2 Microsoft Visual Studio (Windows)

Unlike in Linux, C compiling software is not native to the Windows operating system. But numerous third-party packages are available including the GCC package that has also been ported to this platform. For this book, we’ll refer to the popular GUI-based Visual Studio package, where the *Build* menu in the menu bar offers all the necessary processing options. The essential programming activities and their associated menu options are listed below:

- Compile the program with *Build > Compile*.
- Invoke the linker with *Build > Build*.
- Execute the program with *Build > ! Execute*.

Unlike GCC, Visual Studio supports a built-in editor having limited capabilities. It also permits command-line operation from an MS-DOS shell. The commands to compile and link are **cl.exe** and **link.exe**, respectively. Like **gcc**, **cl.exe** directly invokes the linker (**link.exe**) to create the
