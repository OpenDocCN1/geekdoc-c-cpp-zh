C is highly portable. This means that C programs written for one computer can be run on another with little or no modification. Portability is important if we plan to use a new computer with a different operating system.

C language is well suited for structured programming, thus requiring the user to think of a problem in terms of function modules or blocks. A proper collection of these modules would make a complete program. This modular structure makes program debugging, testing and maintenance easier.

Another important feature of C is its ability to extend itself. A C program is basically a collection of functions that are supported by the C library. We can continuously add our own functions to the C library. With the availability of a large number of functions, the programming task becomes simple.



Before discussing any specific features of C, we shall look at some sample C programs and analyse and understand how they work. Every program must have exactly one main function. If we use more than one main function, the compiler cannot tell which one marks the beginning of the program.



Consider a very simple program given in Fig. 2.1. This program when executed, will produce the following output:

```
```c
main()
{
/* ............printing begins............. */
printf("I see, I remember");
/* ............printing ends............. */
}
```
```

Fig. 2.1 A program to print one line of text

Let us have a close look at the program. The first line informs the system that the name of the program is main and the execution begins at this line. The main() is a special function used by the C system to tell the computer where the program starts. Every program must have exactly one main function. If we use more than one main function, the compiler cannot tell which one marks the beginning of the program.

The empty pair of parentheses immediately following main indicates that the function main has no arguments (or Parameters). The concept of arguments will be discussed in detail later when we discuss functions (in Chapter 10).

The opening brace '{' in the second line marks the beginning of the function main and the closing brace '}' in the last line indicates the end of the function. In this case, the closing brace also marks the end of the program. All the statements between these two braces form the function body. The function body contains a set of instructions to perform the given task.

In this case, the function body contains three statements, out of which only the printf line is an executable statement. The lines beginning with /* and ending with */ are known as comment lines. These are used in a program to enhance its readability and understanding. Comment lines are not executable.