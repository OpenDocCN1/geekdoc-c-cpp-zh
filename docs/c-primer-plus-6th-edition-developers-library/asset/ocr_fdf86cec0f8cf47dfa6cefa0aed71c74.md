# Pass 1: Quick Synopsis

This section presents each line from the program followed by a short description; the next section (Pass 2) explores the topics raised here more fully.

```
#include <stdio.h>      include another file
```

This line tells the compiler to include the information found in the file stdio.h, which is a standard part of all C compiler packages; this file provides support for keyboard input and for displaying output.

```
int main(void)      ←a function name
```

C programs consist of one or more functions, the basic modules of a C program. This program consists of one function called main. The parentheses identify main() as a function name. The int indicates that the main() function returns an integer, and the void indicates that main() doesn’t take any arguments. These are matters we’ll go into later. Right now, just accept both int and void as part of the standard ANSI C way for defining main(). (If you have a pre-ANSI C compiler, omit void; you may want to get something more recent to avoid incompatibilities.)

```
/* a simple program */      ←a comment
```

The symbols /* and */ enclose comments—remarks that help clarify a program. They are intended for the reader only and are ignored by the compiler.

```
{      ←beginning of the body of the function
```

This opening brace marks the start of the statements that make up the function. A closing brace } marks the end of the function definition.

```
int num;      ←a declaration statement
```

This statement announces that you are using a variable called num and that num will be an int (integer) type.

```
num = 1;      ←an assignment statement
```

The statement num = 1; assigns the value 1 to the variable called num.

```
printf("I am a simple ");      ←a function call statement
```

The first statement using printf() displays the phrase I am a simple on your screen, leaving the cursor on the same line. Here printf() is part of the standard C library. It’s termed a function, and using a function in the program is termed calling a function.

```
printf("computer.\n");      ←another function call statement
```

The next call to the printf() function tacks on computer to the end of the last phrase printed. The \n is code telling the computer to start a new line—that is, to move the cursor to the beginning of the next line.

```
printf("My favorite number is %d because it is first.\n", num);
```