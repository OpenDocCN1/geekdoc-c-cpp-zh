modifier increases the length of information that a basic type can contain. The following are the basic type modifiers available in C:

+   - signed
+   - unsigned
+   - long
+   - short

An int data type can be modified by all the preceding modifiers; whereas, char can be extended by using only the unsigned and signed modifiers. Table 1.3 lists the lengths of data types in C:

**Table 1.3: Length of Data Types in C**

| Type | Standard size in bits | Range |
| --- | --- | --- |
| char | 8 | -127 to 127 |
| unsigned char | 8 | 0 to 255 |
| signed char | 8 | -127 to 127 |
| int | 16 or 32 | -32,767 to 32,767 |
| unsigned int | 16 or 32 | 0 to 65,535 |
| signed int | 16 or 32 | same as int |
| short int | 16 | -32767 to 32,767 |
| unsigned short int | 16 | 0 to 65,535 |
| signed short int | 16 | same as short int |
| long int | 32 | -2,147,483,647 to 2,147,483,647 |
| long long int | 64 | -(2^63 -1) to 2^63 -1 |
| signed long int | 32 | same as long int |
| unsigned long int | 32 | 0 to 4,294,967,295 |
| unsigned long long int | 64 | 2^64 - 1 |
| float | 32 | IE-37 to IE+37 (six digit precision) |
| double | 64 | IE-37 to IE+37 (ten digit precision) |
| long double | 80 | IE-37 to IE+37 (six digit precision) |

The "signed" modifier is not used in C as the integer declaration in C is always a signed integer. The difference between a signed and unsigned integer is in their representation. The compiler treats the most significant bit of an integer as the sign bit. If the sign bit in an integer is set to zero, then the integer is considered to be positive, else negative. The negative numbers are stored in the form of 2's complement representation in C, where all the bits of the number are reversed except the sign flag and 1 is added to it. Then the sign bit is set to 1. Signed integers restrict the user to use the complete range of the numbers. For example, the positive range of a signed integer becomes 32,767 which is represented as:

```
```
01111111 11111111
```
```

If the higher order bit of this number is set to 1, then this number becomes -1. If the same number is declared as an unsigned integer, then the range goes up till 0 to 65,535, when the higher order bit is set to 1.