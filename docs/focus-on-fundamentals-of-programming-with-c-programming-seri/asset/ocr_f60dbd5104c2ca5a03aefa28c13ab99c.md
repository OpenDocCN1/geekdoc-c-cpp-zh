The int before main() signifies that the main() function will return an integer value when it completes. The void in parentheses after main() signifies that no information will be passed to the main() function.

The left curly brace, {, marks the beginning of the function (program), and the right curly brace, }, marks the end of the function (program). As you will soon discover, curly braces are used to group together "blocks" of code.

The statement:

```
printf("Hello, world.\n");
```

is a function call which invokes a function called printf() with the argument: "Hello, world.\n".printf() is a library function which prints output to the terminal window: Hello, world.

The program is linked to the I/O library with the preprocessor command:

```
#include <stdio.h>
```

Without this declaration, the compiler would not understand the what the printf() function was to do.

The symbols \n represents a newline character and causes a linefeed to be generated. Note that it consists of two characters in the source file, but consists as one character within the program itself.

Note that we could have written the program as follows:

```
// hello2.c - first C program

#include <stdio.h>

int main(void) {
    printf("Hello, ");
    printf("world. ");
    printf("\n");
    return 0;
}
```