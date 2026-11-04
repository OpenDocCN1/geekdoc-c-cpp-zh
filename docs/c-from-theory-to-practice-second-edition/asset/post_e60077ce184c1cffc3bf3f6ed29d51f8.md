
## Advantages of C

Despite the emergence of many programming languages, C still remains competitive and popular in the programming world for several reasons, such as the following:

- 1. It is a flexible language, which can be used for the development of different kinds of applications, from embedded systems and operating systems to industrial applications. For example, we've used C in the area of communication networks for the development of network protocols and the support of network services.
- 2. A C program is executed very quickly.
- 3. It is a small language. Its vocabulary consists of a few words with special meanings.
- 4. It is portable, meaning that a C program may run under different operating systems.
- 5. It supports structural programming, meaning that a C program may contain functions to perform several tasks.
- 6. It is a language very close to the hardware and it can be used for systems programming.
- 7. Every C compiler comes with a set of ready-to-use functions, called C standard library. The use of these library functions saves considerable programming effort.
- 8. Thanks to the popularity of the C language, there are many C compilers available; some of them free of charge.
- 9. Learning C will help you to learn other languages. For example, getting familiar with C is the first step toward object-oriented programming. Most of the C features are supported in several object-oriented languages, like C++, Java, and C#.

## Disadvantages of C

- 1. Because the C language does not impose many restrictions on the use of its features, it is an error-prone language. When writing a C program, be cautious because you may insert bugs that won't be detected by the compiler.
- 2. C supports only single-thread flow; it does not support multithread programming, parallel operation, and synchronization.
- 3. Although C is a small language, it is not an "easy-to-use" language. C code can be very hard to understand even if it consists of a small number of lines. After reading this book, check out the International Obfuscated C Code Contest (http://www.ioccc.org) to get a feeling.
- 4. C is not an object-oriented language; therefore, it does not support object-oriented features.

## C Program Life Cycle

The life cycle of a C program involves several steps: write the code, compile the code, link the object code produced by the compiler with any code needed to produce the executable file, and run the program. Usually, a C compiler provides an integrated development environment (IDE) that allows us to perform this set of operations without leaving the environment.

### Writing a C Program

To write a C program, we can use any available text editor. An editor is often integrated with the compiler. The source code must be saved in a file with extension .c. When the size of the code is very large, it is a common practice to divide the code into several files, in order to facilitate tasks like testing and maintenance. In such cases, each file is compiled separately.

### Our First C Program

Our first program will be a “rock” version of the program that most programmers begin with. Instead of the classical “Hello world” message, our first program displays on the screen the classical song of Ramones, Hey Ho, Let’s Go. Play it loud, and let’s go …

```c
#include <stdio.h>
int main(void)
{
    printf("Hey Ho, Let's Go\n");
    return 0;
}
```

The following sections explain the significance of each program line.

### The #include Directive

The #include directive instructs the compiler to include the contents of the stdio.h file into the program before it is compiled. Regarding syntax, directives always begin with a # character and do not end with a semicolon; or some other special marker. The stdio.h file and other files contain information about the standard library functions. The typical extension is .h and they are called header files. These files are supplied with the compiler. For example, as shown in Appendix C, the stdio.h (standard input output) file contains declarations of data input and output functions, and because of that, it is almost always included in a program. An included file may also contain #include directives and include other files. In general, when you are using a standard library function, you must include the header file that contains its declaration. The order of their inclusion does not matter. When you get familiar with the C language, you may edit your own header files and include them in your programs.

When the program is compiled, the compiler searches for the included files. The searching rules depend on the implementation. Typically, if the file name is enclosed in brackets <>, the compiler searches in system dependent predefined directories, where system files reside. If it is enclosed in double quotes "", the compiler usually begins with the directory of the source file, then searches the predefined directories. If the file is not found, the compiler will produce an error message and the compilation fails. The file name may include relative or full path information. For example:

```c
#include <d:\projects\serial.h> /* DOS/Windows path. */
#include </port/serial.h> /* Linux path. */
#include "..\projects\test.h" /* Relative path. */
```

However, it'd be better to avoid including path or drive information, because if your program is transferred to another system its compilation might fail.

### The main() Function

Every C program must contain a function named main(). Simply put, a function is a series of declarations and statements that have been grouped together and given a name. The code of the program, or else the body of the function, must be enclosed in braces {}. A statement is a command that will be executed when the program runs. Statements are typically written in separate lines, and, almost always, each statement ends with a semicolon. Although the compiler does not care about the layout of the program, proper indentation and spacing make your program easier to read. Braces are used to group declarations and statements into a block or else a compound statement that the compiler treats as one. Besides functions, we'll use braces in control statements and loops.

The main() function is called automatically when the program runs. The execution of the program ends when the last statement of main() is executed, unless an exit statement such as return is called earlier. The keyword int indicates that main() must return an integer to the operating system when it terminates. This value is returned with the return statement; the value 0 indicates normal termination. This declaration of main() is fairly common. However, you may see other declarations such as:

```c
void main()
```

As we'll see in Chapter 11, the keyword void indicates that main() does not return any value. Although a C compiler may accept this declaration, it is illegal according to the C standard because main() must return a value.

Many programmers often omit the word void and write int main(). It is a habit that might originate either from an older version of C or because of their involvement with C++, where there is no need to use the word void. However, if we want to follow the ANSI C standard, we must use the word void. The reason is that a pair of empty parentheses indicates that the function takes an unknown number of parameters, not any. In Chapter 11, we'll see another declaration of main(), where main() takes parameters.

Finally, because the return type is `int` by default, it is allowed to omit the word `int` and write `main(void)`.

As said, we may use functions of the standard library in our programs. For example, `printf()` is a standard library function that is used for data output. The C standard defines the characteristics of the library functions. Appendix C provides a short description. Since `printf()` is declared in `stdio.h`, we have to include that file in our program. As we'll see in Chapter 2, the new line character `\n` moves the cursor to the beginning of the next line. Functions will be discussed in Chapter 11. Until then, it is enough to know that a function is called by using its name; it performs a task and may optionally return a value.

### Comments

Adding comments improves the readability of the program and makes it easier to understand. A comment begins with the `/*` symbol and ends with `*/`. Comments can extend in more than one line. The compiler ignores anything included between the `/*` `*/` symbols, meaning that the comments do not affect the operation of the program. For example, a comment is added to describe the purpose of the program:

```c
#include <stdio.h>
/* This program calls printf() to display a message on the screen. */
int main(void)
{
    printf("Hey Ho, Let's Go\n");
    return 0;
}
```

Nested comments are not allowed. For example, the following code is illegal, and the compiler will raise an error message:

```c
/*
/* Another comment. */
*/
```

Adding comments is a must when writing programs. An explanatory program saves you time and effort when you need to modify it, and the time of other people who may need to understand and evolve your program.

Based on what you've learned so far, can you tell us what does the following program output? Consider the spaces inside each `printf()`.

```c
#include <stdio.h>
int main(void)
{
    printf("That is "); /* A program with multiple printf() */
    printf("the first");
    printf(" trap"); /* That's the last one. */
    return 0;
}
```
