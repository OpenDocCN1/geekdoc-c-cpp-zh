# # Using Character Variables

Like variables, you must declare chars before using them, and you can initialize them at the time of declaration. Here are some examples:

```
char a, b, c;
/* Declare three uninitialized char variables */
char code = 'x';      /* Declare the char variable named code */
                     /* and store the character x there */
code = '!!';         /* Store ! in the variable code */
```

To create literal constants, you must enclose a single character in quotation marks. The compiler automatically translates literal constants into the corresponding ASCII codes, and the numeric code is assigned to the variable.

You can create symbolic constants by using either the #define directive or the
const keyword:

```
#define EX = 'x'

const char code = EX;      /* Sets code equal to 'x' */
const char A = 'Z';
```

Now that you know how to declare and initialize character variables, it's time for a demonstration. Listing 10.1 illustrates the numeric number of character storage using the printf() function you learned in Lesson 7, “Fundamentals of Reading and Writing Information.” The function printf() can be used to print both characters and numbers. The format string %c instructs printf() to print a character, whereas %d instructs it to print a decimal integer. char variables and prints each one, first as a character and as a number.

Input
LISTING 10.1 chart.c--The Numeric Number of Type char Variables

```
1: /* chartest.c--Demonstrates the numeric number of char variables */
2:
3: #include <stdio.h>
4:
5: /* Declare and initialize two char variables */
6:
7: char c1 = 'a';
8: char c2 = 90;
9:
10: int main( )
11: {
12:     /* Print variable c1 as a character, then as a number * */
13:
```