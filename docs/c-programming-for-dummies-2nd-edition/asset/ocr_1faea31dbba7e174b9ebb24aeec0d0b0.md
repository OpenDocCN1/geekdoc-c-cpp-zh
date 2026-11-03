# Exercise 7-1: Create a new program using the source code from Listing 7-1. Build and run.

The getchar() function is prototyped in the stdio.h header file, which must be included in the source code. In Listing 7-1, it's included already for the definition of the printf() function. The getchar() function's format is

```
int getchar(void);
```

The function has no arguments, which is why the keyword void is set for the function's argument in its definition. In use, the parentheses are always empty.

The getchar() function returns an integer value — not a char value, despite its being a character I/O function. The integer returned contains a character, which is just how it works.

# Exercise 7-2: Edit Line 9 in the source code from Listing 7-1 so that the %d place-holder is used instead of %c. Build and run.

The value that's displayed when you run the solution to Exercise 7-1 is the character's ASCII code value. The %d displays that value because internally the computer treats all information as values. Only when information is displayed as a character does it look like text.

Appendix A lists ASCII code values.

![](bbox=[0.15, 0.6, 0.25, 0.8])

Depending on how the compiler implements it, getchar() may be a macro, not a function. A macro is a shortcut based on another function. For example, the real function to get characters from standard input may be getc(); specifically, when used like this:

```
c = getc(stdin);
```

In this example, getc() reads from the standard input device, stdin, which is defined in the stdio.h header file. The function returns an integer value, which is stored in variable c.

# Exercise 7-3: Rewrite the source code for Listing 7-1, replacing the getchar() statement with the getc() example just shown.

# Exercise 7-4: Write a program that prompts for three characters; for example:

```
I'm waiting for three characters:
```