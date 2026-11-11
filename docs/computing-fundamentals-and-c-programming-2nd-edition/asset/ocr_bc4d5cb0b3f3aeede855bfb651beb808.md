Table 6.1 Character Test Functions

| Function | Test |
|---|---|
| isalnum(c) | Is c an alphanumeric character? |
| isalpha(c) | Is c an alphabetic character? |
| isdigit(c) | Is c a digit? |
| islower(c) | Is c lower case letter? |
| isprint(c) | Is c a printable character? |
| ispunct(c) | Is c a punctuation mark? |
| isspace(c) | Is c a white space character? |
| isupper(c) | Is c an upper case letter? |

# 6.3 WRITING A CHARACTER  LO 6.2

Like `getchar`, there is an analogous function `putchar` for writing characters one at a time to the terminal. It takes the form as shown below:

```
```c
putchar (variable_name);
```
```

where `variable_name` is a type `char` variable containing a character. This statement displays the character contained in the `variable_name` at the terminal. For example, the statements

```
```c
answer = 'Y';
putchar (answer);
```
```

will display the character Y on the screen. The statement

```
```c
putchar ('\n');
```
```

would cause the cursor on the screen to move to the beginning of the next line.

# WORKED-OUT PROBLEM 6.3  M

A program that reads a character from keyboard and then prints it in reverse case is given in Fig. 6.3. That is, if the input is upper case, the output will be lower case and vice versa.

The program uses three new functions: `islower`, `toupper`, and `tolower`. The function `islower` is a conditional function and takes the value TRUE if the argument is a lowercase alphabet; otherwise takes the value FALSE. The function `toupper` converts the lowercase argument into an uppercase alphabet while the function `tolower` does the reverse.

```
Program

```c
#include <stdio.h>
#include <ctype.h>
main()
{
    char alphabet;
    printf("Enter an alphabet");
```
```