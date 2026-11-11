
![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_126_0.png)

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_126_1.png)

## STRUCTURE OF A ‘C’ PROGRAM

As we have already seen, to solve a problem there are three main things to be considered. Firstly, what should be the output? Secondly, what should be the inputs that will be required to produce this output and thirdly, the steps of instructions which use these inputs to produce the required output. As stated earlier, every programming language follows a set of rules; therefore, a program written in C also follows predefined rules known as syntax. C is a case sensitive programming language. All C programs comprise one or more functions. One function that must be present in every C program is main ( ). This is the first function called up when the program execution begins. Basically, main ( ) outlines what a program does. Although main is not given in the keyword list, it cannot be used for naming a variable. The structure of a C program is illustrated in the following where functions func1 ( ) through funcn ( ) represent user defined functions.

```text
Preprocessor directives
Global data declarations
main ( ) /* main function*/
{
Declaration part;
Program statements;
}
/*User defined functions*/
func1 ( )
{
***********
}
func2 ( )
{
***********
}
funcn ( )
{
***********
}
```

Structure of a C Program.

## A SIMPLE C PROGRAM

From the above sections, you have become familiar with a programming language and the structure of a C program. It is now time to write a simple C program.

This program will illustrate how to print out the message “This is my First Program”.

### Example

**Write a program to print a message on the screen.**

```c
/*Program to print a message*/
#include <stdio.h> /* header file*/
void main ( ) /* main function*/
{
printf("This is my First Program\n"); /* output statement*/
}
```

The explanation of the above program is as follows: Every C program contains a function called **main ( )**. This is the starting point of the computer program. This is the point from where the execution begins. It will usually call other functions to help perform its job, some that we write and others from the standard libraries provided.

**#include <stdio.h>** is a reference to a special file called stdio.h which contains information that must be included in the program when it is compiled. The inclusion of this required information will be handled automatically by the compiler. You will find it at the commencement of almost every C program. Basically, all the statements starting with **#** in a C program are called preprocessor directives. These will be considered in the later units. Just remember that this statement allows you to use some predefined functions such as **printf()**, in this case.

**main()** declares the start of the function, while the two curly brackets { } shows the start and finish of the function. Curly brackets in C are used to group statements together as a function, or in the body of a loop. Such a grouping is acknowledged as a compound statement or a block. Every statement within a function ends with a terminator semicolon (;). **printf("This is my First Program\n");** prints the words on the screen. The text to be printed is put in double quotes. The \n at the end of the text tells the program to print a new line as part of the output. That means now if we give a second printf statement, it will be printed in the next line.

Comments may appear anywhere within a program, as long as they are placed within the delimiters /* and */. Such comments are helpful in identifying the program’s principal features or in explaining the underlying logic of various program features. While useful for teaching, such a simple computer program has few practical uses. Let us think something rather more practical. Let us look into the example given below, the complete program development life cycle.

## RUNNING C PROGRAMS

If we want to run the C programs then we have to use the concept of The Edit-Compile-Link-Execute Process.

*The Edit-Compile-Link-Execute Process*

Developing a program in a compiled language such as C requires at least four steps:

- 1. **Editing** (or writing) the program
- 2. **Compiling** it
- 3. **Linking** it
- 4. **Executing** it

We will now cover each step separately.

### Editing

You write a computer program with words and symbols that are understandable to human beings. This is the *editing* part of the development phase. You type the program immediately into a window on the screen and save the resulting text as a separate file. This is often referred to as the *source file* (you can read it with the TYPE command in DOS or the **cat** command in UNIX). The tradition is that the text of a C program is stored in a file with the extension .c for C programming language.

### Compiling

You cannot directly execute the source file. To run on any computer system, the source file must be translated into binary numbers understandable to the computer’s Central processing unit (for example, the 80x87 microprocessor). This process develops an intermediate object file with the extension .obj, the .obj represents Object.

### Linking

The first question that comes to most people's minds is *why is linking necessary?* The main cause is that many compiled languages come with library routines which can be added to your program. These functions are written by the manufacturer of the compiler to perform a variety of tasks, from input/output to complicated mathematical functions. In the case of C the standard input and output routines are contained in a library (stdio.h) so even the most basic program will require a library function. After linking, the file extension is .exe, which is denoted as executable files.

### Executing

Thus the text editor produces .c source files, which go to the compiler, which produces .obj object files, which go to the linker, which produces .exe executable file. You can then run .exe files as you can other applications, simply by typing their names at the DOS prompt or run utilizing Windows menu.

Graphically it is represented as follows:

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_128_0.png)

## C Language Using Microsoft Windows Environment

If we want to use Microsoft Windows/DOS environment then we have to follow the following steps to execute any C program:

### Edit Stage

The direct executable file of C language is TC.exe then firstly we have to find tc.exe file and then double click on it then automatically the editor of Turbo C environment is open and we have to write the program on this environment:

### Compile and Link

For the Turbo C environment, firstly we have to save the program with filename.c and then compile it with the help of ALT+F9 and if any errors are occurred then that particular errors are reported to the user and then we link the program with the help of CTRL+F9 then automatically the direct executable file is created.

### Execute

When the source file is compiled and then the .obj file is created then we have to link it then automatically the direct executable file is created and the program is automatically executed.

### Errors

First error highlighted. Use **Next Error** from **Search** menu for advanced errors if applicable. If you get an error message, or you find that the program does not work when you finally run it (at least not in the way you anticipated) you will have to go back to the source file, the .c file, to make alterations and go through the whole development process again!

## C Language Using UNIX Environment

On all UNIX systems further help on the C compiler can be obtained from the on-line manual. Type **man cc** on your local UNIX system for more information.

Please note that UNIX is a case sensitive operating system and files named firstprog.c and FIRSTPROG.c are handled as two separate files on these systems. By default the UNIX system compiles and links a program in one step, as follows:

```bash
cc firstprog.c
```

This command creates an executable file called a.out that overwrites any existing file called a.out. Executable files on UNIX are run by typing their name. In this case the program is executed as follows:

```bash
a.out
```

To change the name of the executable file type:

```bash
cc -o firstprog firstprog.c
```

This produces an executable file called firstprog which is run as follows:

```bash
firstprog
```

## GENERAL INSTRUCTIONS FOR WRITING A PROGRAM IN TURBO C ENVIRONMENT

The following are the general instructions for writing a program in TURBO C environment.

- 1. Firstly we have to write a program using TURBO C environment and then save it as first.c where first is the primary name of the file and .c is the extension of that file.
- 2. Then we have to compile it with the help of ALT+F9 then automatically the object file is created, i.e. First.obj that is written in machine language.
- 3. Then we have to LINK it with the help of CTRL+F9 then automatically the direct executable file is created i.e. First.exe and the program is automatically executed.

## ADD COMMENTS TO A PROGRAM

A comment is a note to yourself (or others) that you put into your source code. All comments are dismissed by the compiler. They exist solely for your benefit. Comments are used mainly to document the intent and purpose of your source code, so that you can remember later how your functions and how
