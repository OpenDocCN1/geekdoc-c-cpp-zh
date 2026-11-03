...cont'd

2 Two lines below the preprocessor instruction, add an empty main function

int main()
{ 
}

This function declaration specifies that an integer value, of the int data type, should be returned by the function upon completion.

Hot tip
Whitespace between the code and the C compiler is ignored but program code should always end with a newline character.

3 Between the braces, insert a line of code that calls upon one of the functions defined in the standard input/output library – made available by the preprocessor instruction
printf ( "Hello World!\n" ) ;

Here the printf() function specifies a single string argument between its parentheses. In C programming, strings must always be enclosed within double quotes. This string contains the text Hello World and the \n "newline" escape sequence that moves the print head to the left margin of the next line.

4 Between the braces, insert a final line of code to return a zero integer value, as required by the function declaration
return 0 ;

Traditionally, returning a value of zero after the execution of a program indicates to the operating system that the program executed correctly.

Don't forget
Each statement must be terminated by a semi-colon character.

5 Check that the program code looks exactly like the listing below, then add a final newline character (hit Return after the closing brace) and save the program as "hello.c"

```
```c
#include <stdio.h>

int main()
{
    printf( "Hello World!\n" );
    return 0 ;
}
```
```

The complete program in text format is now ready to be compiled into machine-readable byte format as an executable file.