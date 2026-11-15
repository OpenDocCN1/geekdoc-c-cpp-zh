# # PRACTICE!

Give assignment statements for calculating the following values, given the value of x. (Assume that the value of x is in the proper range of values for the calculations.)

+   1. coth x
+   2. sec x
+   3. csc x
+   4. acoth x
+   5. acosh x
+   6. acsc x

# ## 2.9 Character Functions

Numerous functions are available to use with character data. There are functions designed for character input and output, functions to convert characters between uppercase and lowercase, and functions to perform character comparisons. In this section, we will discuss these character functions.

# ### Character I/O

Although printf and scanf functions can be used to print and read characters using the %c specifier, C also contains special functions for reading and printing characters. The getchar function reads the next character from the keyboard and returns the integer value of the character; the putchar function prints a character to the computer screen.

The putchar function takes one integer argument and returns an integer value. The execution of the putchar function causes the character that corresponds to the integer argument to be written to the computer screen. If several putchar function references are made in a row, the characters are printed one after another on the same line, until a newline character is printed. Thus, the following statements cause the characters ab to be printed on one line, followed by the character c on the next line:

```
putchar('a');
putchar('b');
putchar('\n');
putchar('\t');
```

The same information could be printed using the integer values that correspond to the characters (see Table 2.3):

```
putchar(97);
putchar(98);
putchar(10);
putchar(99);
```

The getchar function reads the next character from the keyboard and returns the integer value of the character. If several getchar function references are made in a row, the processing of characters continues until an EOF is received. The EOF is a special value defined as a symbolic constant in stdio.h. Recall that a variable defined with the char data type can represent only the 128 ASCII characters. The value of EOF is outside of this range. Because an integer variable can represent more than 128 values, we use an int type instead of a char