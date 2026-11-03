
In this case, both the field width and the precision are given as arguments which will supply the values for w and p. For example,

```
printf("%*.*f",7,2,number);
```

is equivalent to

```
printf("%7.2f",number);
```

The advantage of this format is that the values for width and precision may be supplied at run-time, thus making the format a dynamic one. For example, the above statement can be used as follows:

```
int width = 7;
int precision = 2;
........
........
printf("%*.*f", width, precision, number);
```

### Example 5.10

All the options of printing a real number are illustrated in Fig. 5.10.

![](img/65953ea584e494f3d396b2252cb5ea53_130_0.png)

Fig. 5.10 Formatted output of real numbers

Note: Microsoft C supports three digits in exponent part.

## Printing of a Single Character

A single character can be displayed in a desired position using the format

```
%wc
```

The character will be displayed right-justified in the field of w columns. We can make the display left-justified by placing a minus sign before the integer w. The default value for w is 1.

## Printing of Strings

The format specification for outputting strings is similar to that of real numbers. It is of the form

```
%w.ps
```

where w specifies the field width for display and p instructs that only the first p characters of the string are to be displayed. The display is right-justified.

The following examples show the effect of a variety of specifications in printing a string “NEW DELHI 110001”, containing 16 characters (including blanks)

| Specification | Output |
|---|---|
| %s | NEW DELHI 110001 |
| %20s | right justified in 20 columns |
| %20.10s | right justified, first 10 chars |
| %.5s | first 5 chars |
| %-20.10s | left justified, first 10 chars |
| %5s | right justified in 5 columns |

### Example 5.11

Printing of characters and strings is illustrated in Fig. 5.11.

## Mixed Data Output

It is permitted to mix data types in one printf statement. For example, the statement of the type

```
printf("%s%d %f %s %c", a, b, c, d);
```

Program
```
/************************************************/
/*      PRINTING OF CHARACTERS AND STRINGS      */
/************************************************/
main()
{
    char x = 'A';
    static char name[20] = "ANIL KUMAR GUPTA";
    printf("OUTPUT OF CHARACTERS\n");
    printf("%c\n%c\n%5c\n", x,x,x);
    printf("%3c\n%3c\n", x,x);
    printf("\n");
    printf("OUTPUT OF STRINGS\n");
    printf("%s\n", name);
    printf("%20s\n", name);
    printf("%20.10s\n", name);
    printf("%5s\n", name);
    printf("%-20.10s\n", name);
    printf("%5s\n", name);
}
Output
OUTPUT OF CHARACTERS
A
  A
    A
A
OUTPUT OF STRINGS
ANIL KUMAR GUPTA
        ANIL KUMAR GUPTA
    ANIL KUMAR
ANIL
ANIL KUMAR
ANIL KUMAR GUPTA
```

### Fig. 5.11 Printing of characters and strings

Commonly used printf format codes are given in Table 5.3 and format flags in Table 5.4.

### Table 5.3 printf Format Codes

| Code | Meaning |
|------|---------|
| %c | print a single character |
| %d | print a decimal integer |
| %e | print a floating point value in exponent form |
| %f | print a floating point value without exponent |
| %g | print a floating point value either e-type or f-type depending on value |
| %i | print a signed decimal integer |
| %o | print an octal integer, without leading zero |
| %s | print a string |
| %u | print an unsigned decimal integer |
| %x | print a hexadecimal integer, without leading 0x |

The following letters may be used as prefix for certain conversion characters.

- h for short integers,
- l for long integers or double,
- L for long double

### Table 5.4 Output Format Flags

| Flag | Meaning |
|---|---|
| - | Output is left-justified within the field. Remaining field will be blank. |
| + | + or – will precede the signed numeric item. |
| 0 | Causes leading zeros to appear. |
| # (with o or x) | Causes octal and hex items to be preceded by 0 and 0x, respectively. |
| # (with e, f or g) | Causes a decimal point to be present in all floating point numbers, even if it is whole number. Also prevents the truncation of trailing zeros in g-type conversion. |

## Enhancing the Readability of Output

Computer outputs are used as information for analysing certain relationships between variables and for making decisions. Therefore the correctness and clarity of outputs is of utmost importance. While the correctness depends on the solution procedure, the clarity depends on the way the output is presented. Following are some of the steps we can take to improve the clarity and hence the readability and understandability of outputs.

- 1. Provide enough blank space between two numbers.
- 2. Introduce appropriate headings and variable names in the output.
- 3. Print special messages whenever a peculiar condition occurs in the output.
- 4. Introduce blank lines between the important sections of the output.

The system usually provides two blank spaces between the numbers. However, this can be increased by selecting a suitable field width for the numbers or by introducing a ‘tab’ character between the specifications. For example, the statement

```
printf("a = %d\t b = %d", a, b);
```

will provide four blank spaces between the two fields. We can also print them on two separate lines by using the statement

```
printf("a = %d\n b = %d", a, b);
```

Messages and headings can be printed by using the character strings directly in the printf statement.

Examples:

```
printf("\n OUTPUT RESULTS \n");
printf("code\t Name\t Age\n");
printf("Error in input data\n");
printf("Enter your name\n");
```

## CASE STUDIES

### 1. Inventory Report

Problem: The ABC Electric Company manufactures four consumer products. Their inventory position on a particular day is given below:

| Code | Quantity | Rate (Rs) |
|---|---|---|
| F105 | 275 | 575.00 |
| H220 | 107 | 99.95 |
| I109 | 321 | 215.50 |
| M315 | 89 | 725.00 |

It is required to prepare the inventory report table in the following format:

### INVENTORY REPORT

| Code | Quantity | Rate | Value |
|---|---|---|---|
| — | — | — | — |
| — | — | — | — |
| — | — | — | — |
| — | — | — | — |
|  |  |  | Total Value: |

The value of each item is given by the product of quantity and rate.

Program: The program given in Fig. 5.12 reads the data from the terminal and generates the required output. The program uses subscripted variables which are discussed in Chapter 8.

### 2. Reliability Graph

Problem: The reliability of an electronic component is given by
reliability (r) = e^{-λt}

Program
```
/*******************************/
/*      INVENTORY REPORT        */
/*******************************/

#define ITEMS 4
main()
{ /* BEGIN */
    int i, quantity[5];
    float rate[5], value, total_value;
    char code[5][5];
    /* READING VALUES */
    i = 1;
    while (i <= ITEMS)
```
```
{ printf("Enter code, quantity, and rate:"); scanf("%s %d %f", code[i], &quantity[i], &rate[i]); i++; }
/* ............... Printing of Table and Column Headings ............... */
printf("\n"); printf("\t\t\t\t\t\t\t\t\t\tINVENTORY REPORT\t\n"); printf("-------------------------------------------------------------------\n"); printf("\tCode\t\tQuantity\t\tRate\t\tValue\n"); printf("-------------------------------------------------------------------\n");
/* ............... Preparation of Inventory Position .................... */
total_value = 0; i = 1; while (i <= ITEMS) { value = quantity[i] * rate[i]; printf("%s %5d %10.2f %10.2f\n", code[i], quantity[i], rate[i], value); total_value += value; i++; }
/* ............... Printing of End of Table ............................. */
printf("-------------------------------------------------------------------\n"); printf("\t\t\t\t\t\t\t\tTotal Value = %e\n", total_value); printf("-------------------------------------------------------------------\n"); } /* END */
```

Output
Enter code, quantity, and rate:F105  275  575.00
Enter code, quantity, and rate:H220  107  99.95
Enter code, quantity, and rate:I109 321  215.50
Enter code, quantity, and rate:M315  89  725.00

| Code | Quantity | Rate | Value |
|---|---|---|---|
| F105 | 275 | 575.00 | 1.581250e+005 |
| H220 | 107 | 99.95 | 1.069465e+004 |
| I109 | 321 | 215.50 | 6.917550e+004 |
| M315 | 89 | 725.00 | 6.452500e+004 |
|  |  |  | Total Value = 3.025202e+005 |

### Fig. 5.12 Program for inventory report

where λ is the component failure rate per hour and t is the time of operation in hours. A graph is required to determine the reliability at various times, from 0 to 300 hours. The failure rate λ (lamda) is 0.001.

```
Program
/**************************************************************/
/*              RELIABILITY GRAPH                             */
/**************************************************************/
#include <math.h>
```
