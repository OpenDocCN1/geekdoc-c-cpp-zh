| | |
|---|---|
| * | This is an optional starting asterisk, which indicates that the data is to be read from the stream but ignored, i.e. it is not stored in the corresponding argument. |
| width | This specifies the maximum number of characters to be read in the current reading operation. |
| modifiers | Specifies a size different from int (in the case of d, i and n), unsigned int (in the case of o, u and x) or float (in the case of e, f and g) for the data pointed by the corresponding additional argument: h : short int (for d, i and n), or unsigned short int (for o, u and x) l : long int (for d, i and n), or unsigned long int (for o, u and x), or double (for e, f and g) L : long double (for e, f and g) |
| type | A character specifying the type of data to be read and how it is expected to be read. See next table. |

# **fscanf type specifiers:**

| type | Qualifying Input | Type of argument |
|---|---|---|
| c | Single character: Reads the next character. If a width different from 1 is specified, the function reads width characters and stores them in the successive locations of the array passed as argument. No null character is appended at the end. | char * |
| d | Decimal integer: Number optionally preceded with a + or - sign | int * |
| e, E, f, g, G | Floating point: Decimal number containing a decimal point, optionally preceded by a + or - sign and optionally followed by the e or E character and a decimal number. Two examples of valid entries are -732.103 and 7.12e4 | float * |
| o | Octal Integer: | int * |
| s | String of characters. This will read subsequent characters until a whitespace is found (whitespace characters are considered to be blank, newline and | char * |