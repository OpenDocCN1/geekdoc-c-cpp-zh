# LESSON 14 Working with the Screen, Printer, and Keyboard

TABLE 14.3 The Type Specifier Characters Used in scanf() Conversion Specifiers
| Type | Argument | Meaning of Type |
| --- | --- | --- |
| d | int * | A decimal integer. |
| i | int * | An integer in decimal, octal (with leading 0), or hexadecimal (with leading 0x or 0X) notation. |
| o | int * | An integer in octal or without the leading 0. |
| u | unsigned int * | An unsigned decimal integer. |
| x | int * | A hexadecimal integer with or without the leading 0x or 0X. |
| c | char * | One or more characters are read and assigned sequentially to the memory location indicated by the argument. If a field width argument isn't given, one character is read. If a field width argument is given, that number of characters, including white space (if any), is read. |
| s | char * | A string of non-space characters is read into the specified memory location, and a terminating \0 is added. |
| a,f,g | float * | A floating-point number. Numbers can be input in decimal or scientific notation. |
| [...] | char * | A string of the characters listed between the brackets are accepted. Input ends as soon as a nonmatching character is encountered, the specified field width is reached, or Enter is pressed. To accept the } character, list it first: [...]. A \0 is added at the end of the string. |
| [^...] | char * | The same as {...}, except that only characters listed between the brackets are accepted. |
| % | None | Literal: Reads the % character. No assignment is made.|

Before seeing some examples of scanf(), you need to understand the precision modifiers, which are listed in Table 14.4.

TABLE 14.4 The Precision Modifiers
| Precision Modifier | Meaning |
| --- | --- |
| hh | When placed before the type specifier d, i, o, u, x, or n, the modifier hh specifies that the argument is a pointer to a signed char or unsigned char. |
| h | When placed before the type specifier d, i, o, u, x, or n, the modifier h specifies that the argument is a pointer to type short int or unsigned short int.|