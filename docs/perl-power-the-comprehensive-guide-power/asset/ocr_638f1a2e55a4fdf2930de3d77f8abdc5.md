| Function | Discussion |
|---|---|
| `cos()` | Returns the cosine of the argument you supply. The return value is in radians. |
| `exp()` | Returns e to the power of the argument you supply. To raise a number to a power, use the double asterisks (number ** 3). |
| `hex()` | Returns the decimal value of a hexadecimal number. |
| `int()` | If you have a decimal number, this function returns the integer part of the number. |
| `log()` | Returns the natural logarithm of a number. |
| `sin()` | Returns the sine of the argument you supply. The return value is in radians. |
| `sqrt()` | Returns the square root of the number you supply to it. |
| `square()` | Returns the square of the number you supply to it. |
| `oct()` | Returns the decimal value of an octal number. |
| `ord()` | If you supply a character (in single quotes `c`) to this number, it returns the ASCII value of the character. |
| `rand()` | Returns a rational number greater than or equal to 0 and less than 1 (0.1, 0.2, and so on). However, if you supply an integer argument to the `rand()` function, it generates an integer that is greater than or equal to 0 and less than the number you supply. To deal with most situations, programmers use a tactic called shifting. To shift the return of `rand()` so that you get randomly generated values of 1, 2, 3, 4, and 5, you use an expression along the following lines: `1 + int(rand(5))`. |
| `sin()` | Returns the sine of the number you supply. The value returned is in radians. |
| `srand()` | To make it so that you get different results each time you call the `rand()` function, you help it out by seeding a different starting value into the formula the `rand()` function uses. To accomplish this, you use the `srand()` (for “seed” random) function. |
| `time()` | The number of seconds since January 1, 1970. There are 3,600 seconds in an hour, so the numbers tend to be large. |

# Standard Presentation Using the print() Function

To gain a sense of some of the basic alternatives that exist for you as you formulate numeric expressions in Perl, consider Listing05_03. This program provides a set of numeric identifiers and a display of the values the identifiers store. The program provides a starting point for experimentation in the use of formatting, conversion, printing, and other Perl capabilities.

```
```perl
#Listing05_03
#Scalars initialized to numbers
# Integers
```
```