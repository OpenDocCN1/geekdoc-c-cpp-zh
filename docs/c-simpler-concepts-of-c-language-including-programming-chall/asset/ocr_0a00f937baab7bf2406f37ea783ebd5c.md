# 6 C-SIMPLER

| Valid | Invalid |
| -233.78 | 90.09,98 (Comma is not allowed) |
| 43.787 E + 02 | -7.8.97 (Number of . is 3, only one . is allowed) |
| 43.787 E - 0.2 | +- 787.0909 (2 successive symbols are not allowed) |

Table 1.7 Valid and invalid float representations

+   c. char: A single character can be represented with Char keyword. It can also be used to represent series of characters strings. It needs 1 byte for storing one character. A character has to be represented as '&', 'a', 'A', '1', etc. While programming is discussed all these will be clearly represented. And most importantly every character has an integer value mapped to it and is governed by ASCII. The integer values corresponding to the characters are called ASCII codes. Few same ASCII codes are presented below in table 1.8.

| Characters | Equivalent ASCII values |
| 'A' | 65 |
| 'B' | 66 |
| 'a' | 97 |
| '0' | 48 |

Table 1.8 ASCII values for characters.

The following table 1.9 has summary of data type modifiers for int, char and float.

| Modifier Type | Size (in bytes) | Range allowed |
| int | 2 | -32768 to 32767 |
| signed int | 2 | -32768 to 32767 |
| unsigned int | 2 | 0 to 65535 |
| unsigned short int | 2 | 0 to 65535 |
| unsigned long int | 4 | 0 to 4294967295 |
| long int | 4 | -2147483648 to 2147483647 |
| short int | 2 | -32768 to 32767 |
| float | 4 | -3.4 E + 48 to 3.4 E + 48 |
| double | 8 | -1.7 E + 308 to +1.7 E + 308 |
| char | 1 | -128 to +127 |
| signed char | 1 | -128 to +127 |
| unsigned char | 1 | 0 to 65535 |

Table 1.9 Data type modifiers

A C program will depict how to find the size of data types. Program 1.0 is meant for the same and result out executing it is presented here.

```
#include <stdio.h>
int main() {
    printf("\n size of char == %d\n", sizeof(char));
    printf("\n size of short == %d\n", sizeof(short));
}
```