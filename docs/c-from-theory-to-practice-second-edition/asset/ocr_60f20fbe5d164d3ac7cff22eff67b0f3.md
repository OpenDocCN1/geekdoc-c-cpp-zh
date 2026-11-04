# C Program Life Cycle

The life cycle of a C program involves several steps: write the code, compile the code, link the object code produced by the compiler with any code needed to produce the executable file, and run the program. Usually, a C compiler provides an integrated development environment (IDE) that allows us to perform this set of operations without leaving the environment.

# Writing a C Program

To write a C program, we can use any available text editor. An editor is often integrated with the compiler. The source code must be saved in a file with extension c. When the size of the code is very large, it is a common practice to divide the code into several files, in order to facilitate tasks like testing and maintenance. In such cases, each file is compiled separately.

# Our First C Program

Our first program will be a “rock” version of the program that most programmers begin with. Instead of the classical “Hello world” message, our first program displays on the screen the classical song of Ramones, Hey Ho, Let’s Go. Play it loud, and let’s go …

```
#include <stdio.h>
int main(void)
{
    printf("Hey Ho, Let's Go\n");
    return 0;
}
```

The following sections explain the significance of each program line.

# The #include Directive

The #include directive instructs the compiler to include the contents of the stdio.h file into the program before it is compiled. Regarding syntax, directives always begin with a # character and do not end with a semicolon ; or some other special marker. The stdio.h file and other files contain information about the standard library functions. The typical extension is .h and they are called header files. These files are supplied with the compiler. For example, as shown in Appendix C, the stdio.h (standard input output) file contains declarations of data input and output functions, and because of that, it is almost always included in a program. An included file may also contain #include directives and include other files. In general, when you are using a standard library function,