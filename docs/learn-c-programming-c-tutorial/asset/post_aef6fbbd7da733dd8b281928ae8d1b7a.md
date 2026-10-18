
- Decrementing a Pointer ... 106
- Pointer Comparisons ... 107
- Array of Pointers ... 108
- Pointer to Pointer ... 110
- Passing Pointers to Functions ... 112
- Return Pointer from Functions ... 114

## 16. STRINGS ... 117

## 17. STRUCTURES ... 120

- **Defining a Structure** ... 120
- **Accessing Structure Members** ... 121
- **Structures as Function Arguments** ... 122
- **Pointers to Structures** ... 124
- **Bit Fields** ... 126

## 18. UNIONS ... 128

- **Defining a Union** ... 128
- **Accessing Union Members** ... 129

## 19. BIT FIELDS ... 132

- **Bit Field Declaration** ... 133

## 20. TYPEDEF ... 136

- **typedef vs #define** ... 137

## 21. INPUT AND OUTPUT ... 139

- **The Standard Files** ... 139
- **The getchar() and putchar() Functions** ... 139
- **The gets() and puts() Functions** ... 140
- **The scanf() and printf() Functions** ... 141

## 22. FILE I/O ... 143

![](img/6e49c39a6ef9e32d938b03dc613e44f6_6_0.png)

## 27. RECURSION ... 164

### Number Factorial ... 164

### Fibonacci Series ... 165

## 28. VARIABLE ARGUMENTS ... 167

## 29. MEMORY MANAGEMENT ... 170

### Allocating Memory Dynamically ... 170

### Resizing and Releasing Memory ... 172

## 30. COMMAND LINE ARGUMENTS ... 174

## 1. OVERVIEW

C is a general-purpose, high-level language that was originally developed by Dennis M. Ritchie to develop the UNIX operating system at Bell Labs. C was originally first implemented on the DEC PDP-11 computer in 1972.

In 1978, Brian Kernighan and Dennis Ritchie produced the first publicly available description of C, now known as the K&R standard.

The UNIX operating system, the C compiler, and essentially all UNIX application programs have been written in C. C has now become a widely used professional language for various reasons:

- Easy to learn
- Structured language
- It produces efficient programs
- It can handle low-level activities
- It can be compiled on a variety of computer platforms

### Facts about C

- C was invented to write an operating system called UNIX.
- C is a successor of B language which was introduced around the early 1970s.
- The language was formalized in 1988 by the American National Standards Institute (ANSI).
- The UNIX OS was totally written in C.
- Today C is the most widely used and popular System Programming Language.
- Most of the state-of-the-art software have been implemented using C.
- Today's most popular Linux OS and RDBMS MySQL have been written in C.

### Why Use C?

C was initially used for system development work, particularly the programs that make-up the operating system. C was adopted as a system development language because it produces code that runs nearly as fast as the code written in assembly language. Some examples of the use of C might be:

- Operating Systems
- Language Compilers
- Assemblers
- Text Editors
- Print Spoolers
- Network Drivers
- Modern Programs
- Databases
- Language Interpreters
- Utilities

![](img/6e49c39a6ef9e32d938b03dc613e44f6_9_0.png)

### C Programs

A C program can vary from 3 lines to millions of lines and it should be written into one or more text files with extension ".c"; for example, _hello.c_. You can use "vi", "vim" or any other text editor to write your C program into a file.

This tutorial assumes that you know how to edit a text file and how to write source code inside a program file.

## 2. ENVIRONMENT SETUP

### Try it Option Online

You really do not need to set up your own environment to start learning C programming language. Reason is very simple, we already have set up C Programming environment online, so that you can compile and execute all the available examples online at the same time when you are doing your theory work. This gives you confidence in what you are reading and to check the result with different options. Feel free to modify any example and execute it online.

Try the following example using our online compiler option available at [http://www.compileonline.com/](http://www.compileonline.com/).

```c
#include <stdio.h>

int main()
{
    /* my first program in C */
    printf("Hello, World! \n");
    return 0;
}
```

For most of the examples given in this tutorial, you will find the **Try it** option in our website code sections at the top right corner that will take you to the online compiler. So just make use of it and enjoy your learning.

### Local Environment Setup

If you want to set up your environment for C programming language, you need the following two software tools available on your computer, (a) Text Editor and (b) The C Compiler.

### Text Editor

This will be used to type your program. Examples of a few editors include Windows Notepad, OS Edit command, Brief, Epsilon, EMACS, and vim or vi.
