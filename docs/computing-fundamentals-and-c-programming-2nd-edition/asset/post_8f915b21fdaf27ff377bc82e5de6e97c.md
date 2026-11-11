
## 3.11 UNIX SYSTEM

LO 3.6

### 3.11.1 Creating the Program

Once we load the UNIX operating system into the memory, the computer is ready to receive program. The program must be entered into a file. The file name can consist of letters, digits and special characters, followed by a dot and a letter c. Examples of valid file names are:

```
hello.c
program.c
ebg1.c
```

The file is created with the help of a *text editor*, either **ed** or **vi**. The command for calling the editor and creating the file is

```
ed filename
```

If the file existed before, it is loaded. If it does not yet exist, the file has to be created so that it is ready to receive the new program. Any corrections in the program are done under the editor. (The name of your system's editor may be different. Check your system manual.)

When the editing is over, the file is saved on disk. It can then be referenced any time later by its file name. The program that is entered into the file is known as the *source program*, since it represents the original form of the program.

### 3.11.2 Compiling and Linking

Let us assume that the source program has been created in a file named *ebg1.c*. Now the program is ready for compilation. The compilation command to achieve this task under UNIX is

```
cc ebg1.c
```

The source program instructions are now translated into a form that is suitable for execution by the computer. The translation is done after examining each instruction for its correctness. If everything is alright, the compilation proceeds silently and the translated program is stored on another file with the name *ebg1.o*. This program is known as *object code*.

Linking is the process of putting together other program files and functions that are required by the program. For example, if the program is using **exp()** function, then the object code of this function should be brought from the **math library** of the system and linked to the main program. Under UNIX, the linking is automatically done (if no errors are detected) when the cc command is used.

If any mistakes in the **syntax and semantics** of the language are discovered, they are listed out and the compilation process ends right there. The errors should be corrected in the source program with the help of the editor and the compilation is done again.

The compiled and linked program is called the *executable object code* and is stored automatically in another file named **a.out**.

Note that some systems use different compilation command for linking mathematical functions.

```
cc filename -lm
```

is the command under UNIPLUS SYSTEM V operating system.

### 3.11.3 Executing the Program

Execution is a simple task. The command

```
a.out
```

would load the executable object code into the computer memory and execute the instructions. During execution, the program may request for some data to be entered through the keyboard. Sometimes the program does not produce the desired results. Perhaps, something is wrong with the program logic or data. Then it would be necessary to correct the source program or the data. In case the source program is modified, the entire process of compiling, linking and executing the program should be repeated.

### 3.11.4 Creating Your Own Executable File

Note that the linker always assigns the same name a.out. When we compile another program, this file will be overwritten by the executable object code of the new program. If we want to prevent this from happening, we should rename the file immediately by using the command.

```
mv a.out name
```

We may also achieve this by specifying an option in the cc command as follows:

```
cc -o name source-file
```

This will store the executable object code in the file name and prevent the old file a.out from being destroyed.

### 3.11.5 Multiple Source Files

To compile and link multiple source program files, we must append all the file names to the cc command.

```
cc filename-1.c ... filename-n.c
```

These files will be separately compiled into object files called

```
filename-1.o
```

and then linked to produce an executable program file a.out as shown in Fig. 3.11.

![](img/11b034a94fc590add0a7808250a38792_125_0.png)

Fig. 3.11 Compilation of multiple files

It is also possible to compile each file separately and link them later. For example, the commands

```
cc -c mod1.c
cc -c mod2.c
```

will compile the source files mod1.c and mod2.c into object files mod1.o and mod2.o. They can be linked together by the command

```
cc mod1.o mod2.o
```

We may also combine the source files and object files as follows:

```
cc mod1.c mod2.o
```

Only mod1.c is compiled and then linked with the object file mod2.o. This approach is useful when one of the multiple source files needs to be changed and recompiled or an already existing object file is to be used along with the program to be compiled.

## 3.12 MS-DOS SYSTEM

LO 3.6

The program can be created using any word processing software in non-document mode. The file name should end with the characters “.c” like program.c, pay.c, etc. Then the command

```
MSC pay.c
```

under MS-DOS operating system would load the program stored in the file pay.c and generate the object code. This code is stored in another file under the name pay.obj. In case any language errors are found, the compilation is not completed. The program should then be corrected and compiled again.

The linking is done by the command

```
LINK pay.obj
```

which generates the executable code with the filename pay.exe. Now the command

```
pay
```

would execute the program and give the results.

## LEARNING OUTCOMES

- C is a structured, high-level, machine independent language. LO 3.1
- ANSI C and C99 are the standardized versions of C language. LO 3.1
- C combines the capabilities of assembly language with the features of a high level language. LO 3.1
- C is robust, portable and structured programming language. LO 3.1
- Every C program requires a main() function (Use of more than one main() is illegal). The place main is where the program execution begins. LO 3.1
- The execution of a function begins at the opening brace of the function and ends at the corresponding closing brace. LO 3.2
- C programs are written in lowercase letters. However, uppercase letters are used for symbolic names and output strings. LO 3.2
- All the words in a program line must be separated from each other by at least one space, or a tab, or a punctuation mark. LO 3.2
- Every program statement in a C language must end with a semicolon. LO 3.2
- All variables must be declared for their types before they are used in the program. LO 3.2
- A comment can be inserted almost anywhere a space can appear. Use of appropriate comments in proper places increases readability and understandability of the program and helps users in debugging and testing. Remember to match the symbols `/*` and `*/` appropriately. LO 3.2
- Compiler directives such as define and include are special instructions to the compiler to help it compile a program. They do not end with a semicolon. LO 3.2
- The sign # of compiler directives must appear in the first column of the line. LO 3.2
- We must make sure to include header files using #include directive when the program refers to special names and functions that it does not define. LO 3.3
- The structure of a C program comprises various sections including Documentation, Link, Definition, Global Declaration, main () function and Sub program section. LO 3.4
- C is a free-form language and therefore a proper form of indentation of various sections would improve legibility of the program. LO 3.5
- The execution of a C program involves a series of steps including: creating the program, compiling the program, linking the program with functions from C library and executing the program. LO 3.6
- The command used for running a C program in UNIX system is a.out. LO 3.6
- The command used for running a C program in MS-DOS system is file.exe where file is the name of the program that has already been compiled. LO 3.6
- When braces are used to group statements, make sure that the opening brace has a corresponding closing brace. LO 3.6

## KEY TERMS TO REMEMBER

- **#DEFINE:** A preprocessor compiler directive. LO 3.2
- **Printf:** A predefined standard C function that writes the output to the stdout (standard output) stream. LO 3.2
- **Scanf:** A predefined standard C function that reads formatted input from stdin (standard input) stream. LO 3.2
- **Program:** A sequence of instructions written to perform a specific task in the computer. LO 3.1

## REVIEW QUESTIONS

### Fill in the Blanks

- 1. Every program statement in a C program must end with a __________. LO 3.2
- 2. The __________ function is used to display the output on the screen. LO 3.2
- 3. The __________ header file contains mathematical functions. LO 3.3
- 4. The escape sequence character __________ causes the cursor to move to the next line on the screen. LO 3.2

### True or False Statements

- 1. Every line in a C program should end with a semicolon. LO 3.2
- 2. The closing brace of the **main( )** in a program is the logical end of the program. LO 3.2
- 3. Comments cause the computer to print the text enclosed between `/*` and `*/` when executed. LO 3.2
- 4. Every C program ends with an END word. LO 3.2
- 5. A **printf** statement can generate only one line of output. LO 3.2
- 6. The purpose of the header file such as **stdio.h** is to store the source code of a program. LO 3.3
- 7. A line in a program may have more than one statement. LO 3.5
- 8. Syntax errors will be detected by the compiler. LO 3.6

**Levels of Difficulty**

\* Low; \*\* Medium; \*\*\* High
