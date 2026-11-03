uses one bit for sign and 15 bits for the magnitude of the number. Similarly, a 32 bit word length can store an integer ranging from −2, 147, 483, 648 to 2, 147, 483, 647.

In order to provide some control over the range of numbers and storage space, C has three classes of integer storage, namely short int, int, and long int, in both signed and unsigned forms. For example, short int represents fairly small integer values and requires half the amount of storage as a regular int number uses. Unlike signed integers, unsigned integers use all the bits for the magnitude of the number and are always positive. Therefore, for a 16 bit machine, the range of unsigned integer numbers will be form 0 to 65,535.

We declare long and unsigned integers to increase the range of values. The use of qualifier signed on integers is optional because the default declaration assumes a signed number. Table 3.6 shows all the allowed combinations of basic types and qualifiers and their size and range on a 16-bit machine.

# Table 3.6 Size and Range of Data Types on a 16-bit Machine

| Type | Size (bits) | Range |
|---|---|---|
| char or signed char | 8 | − 128 to 127 |
| unsigned char | 8 | 0 to 255 |
| int or signed int | 16 | − 32,768 to 32,767 |
| unsigned int | 16 | 0 to 65535 |
| short int or signed short int | 8 | − 128 to 127 |
| unsigned short int | 8 | 0 to 255 |
| long int or signed long int | 32 | − 2,147,483,648 to 2,147,483,647 |
| unsigned long int | 32 | 0 to 4,294,967,295 |
| float | 32 | 3.4E-38 to 3.4E+38 |
| double | 64 | 1.7E−308 to 1.7E+308 |
| long double | 80 | 3.4E−4932 to 1.1E + 4932 |

# Floating Point Types

Floating point (or real) numbers are stored in 32 bits (on all 16 bits and 32 bit machines), with 6 digits of precision. Floating point numbers are defined in C by the keyword float. When the accuracy provided by a float number is not sufficient, the type double can be used to define the number. A double data type number uses 64 bits giving a precision of 14 digits. These are known as double precision numbers. Remember that double type represents the same data type that float represents, but with a greater precision. To extend the precision further, we may use long double which uses 80 bits.

# Character Types

A single character can be defined as a character(char) type data. Characters are usually stored in 8 bits (one byte) of internal storage. The qualifier signed or unsigned may be explicitly applied to char. While unsigned chars have values between 0 to 255, signed chars have values from −128 to 127.