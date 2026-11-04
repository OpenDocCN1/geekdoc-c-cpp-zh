Finally, because the return type is `int` by default, it is allowed to omit the word `int` and write `main(void)`.

As said, we may use functions of the standard library in our programs. For example, `printf()` is a standard library function that is used for data output. The C standard defines the characteristics of the library functions. Appendix C provides a short description. Since `printf()` is declared in `stdio.h`, we have to include that file in our program. As we'll see in Chapter 2, the new line character `\n` moves the cursor to the beginning of the next line. Functions will be discussed in Chapter 11. Until then, it is enough to know that a function is called by using its name; it performs a task and may optionally return a value.

# Comments

Adding comments improves the readability of the program and makes it easier to understand. A comment begins with the `/*` symbol and ends with `*/`. Comments can extend in more than one line. The compiler ignores anything included between the `/*` `*/` symbols, meaning that the comments do not affect the operation of the program. For example, a comment is added to describe the purpose of the program:

```
```c
#include <stdio.h>
/* This program calls printf() to display a message on the screen. */
int main(void)
{
    printf("Hey Ho, Let's Go\n");
    return 0;
}
```
```

Nested comments are not allowed. For example, the following code is illegal, and the compiler will raise an error message:

```
```
/*
/* Another comment. */
*/
```
```

Adding comments is a must when writing programs. An explanatory program saves you time and effort when you need to modify it, and the time of other people who may need to understand and evolve your program.

Based on what you've learned so far, can you tell us what does the following program output? Consider the spaces inside each `printf()`.

```
```c
#include <stdio.h>
int main(void)
{
    printf("That is "); /* A program with multiple printf()
    printf("the first");
    printf(" trap"); /* That's the last one. */
    return 0;
}
```
```