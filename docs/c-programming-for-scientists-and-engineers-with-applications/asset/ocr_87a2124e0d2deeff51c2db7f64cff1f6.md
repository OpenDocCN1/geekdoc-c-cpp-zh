or lists may be needed. In C, complex data of homogeneous type can be stored in arrays. Arrays are derived data types derived from the basic data types int, float, double, and char.

| loc | 1 | 2 | 3 |
|---|---|---|---|

For example: int loc[] = {1, 2, 3}; is a one-dimensional array named loc representing a position in three-dimensional space. Arrays are presented in detail in Chapters 7 and 8. Character strings are the data type derived from the basic data type char and the derived from data type array.

```
digits = {'0' '1' '2' '3' '4' '5' '6' '7' '8' '9' '\0'}
```

For example: char digits[] = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '\0'}; is a one-dimensional array with 11 elements; each of which is the character representation of a digit except the last one. The last one is the null character. This makes the array into a character string. Character strings are presented in detail in Chapter 9.
Structures are derived data types formed from the basic data types int, float, double, and the derived data types string and array. The members of the structure can be int, float, double, char, array, or string type variables. For example:

| employee "Anderson" | 25.47 |
|---|---|
| name | hourly_wage |

is a structure composed of the structure variable employee with a member name, which is a character string, and a member hourly_wage, which is of the data type float. Structures are presented in Chapter 11.

# 2.2.5 Pointer and Pointer Variables

A pointer is a powerful feature incorporated in C that allows the programmer to manipulate data using the memory address of a variable. In C, like any other programming language, when a variable is declared it allocates storage space in memory and such such storage space is identified by a unique number called a memory address. The value of a pointer is simply a memory address of a variable. The