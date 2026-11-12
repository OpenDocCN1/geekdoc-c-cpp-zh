
advances the file window to the character numbered 15, which is actually the 16th character in the file. Immediately following this operation, you can read the character.

You can also locate a character relative to either the beginning of the file, the current position in the file, or the end of the file by specifying—as the second argument to seekg—

```
ios::mode
```

where mode is one of beg, cur, or end. Thus,

```
myFile.seekg(2, ios::cur)
```

seeks the second character after the one at the present location of the file window.

### G.3 Binary Files

Files that are not text files are called binary (or general or nontext) files. Like a text file, a binary file is a sequence of bytes grouped together into file components. It is important to emphasize that each file component is an indivisible entity. For example, each component of a binary file of integers is an integer in the computer’s internal representation. If you write the integer value 234 to a binary file, the system would write the computer’s internal representation of 234, which is 0000000011101010 in binary, to the file, rather than the three ASCII characters 2, 3, 4, which are, respectively, 00110010, 00110011, and 00110100 in binary. Similar comments are true for a binary file of floating-point numbers. If you could use a text editor to look at the file, you would see gibberish. You create a binary file not by using an editor—as you can for a text file—but rather by running a program.

```
ofstream outFile(myFileName, ios::binary);
```

associates the stream variable outFile with the external binary file whose name is in the string variable myFileName. A binary file has an end-of-file symbol at its end, just as a text file does. However, the notion of lines does not exist for a binary file, although a binary file might contain data that coincidentally looks like an end-of-line symbol. Except for the differences noted here, C++ treats binary files in the same way that it treats text files.

## C++ Header Files and Standard Functions

Appendix H

Here is a list of commonly used C++ header files. Other header files are introduced in the chapters when needed.

### cassert

This library contains only the function assert. You use

```
assert(assertion);
```

to test the validity of an assertion. If assertion is false, assert writes an error message and terminates program execution. You can disable all occurrences of assert in your program by placing the directive #define NDEBUG before the include directive.

### cctype

Most functions in this library classify a given ASCII character as a letter, a digit, and so on. Two other functions convert letters between uppercase and lowercase.

The classification functions return a true value if ch belongs to the specified group; otherwise they return false.

| Function | Description |
| :--- | :--- |
| isalnum(ch) | Returns true if ch is either a letter or a decimal digit |
| isalpha(ch) | Returns true if ch is a letter |
| iscntrl(ch) | Returns true if ch is a control character (ASCII 127 or 0 to 31) |
| isdigit(ch) | Returns true if ch is a decimal digit |
| isgraph(ch) | Returns true if ch is printable and nonblank |
| islower(ch) | Returns true if ch is a lowercase letter |
| isprint(ch) | Returns true if ch is printable (including blank) |
| ispunct(ch) | Returns true if ch is a punctuation character |
| isspace(ch) | Returns true if ch is a whitespace character: space, tab, carriage return, new line, or form feed |
| isupper(ch) | Returns true if ch is an uppercase letter |
| isxdigit(ch) | Returns true if ch is a hexadecimal digit |
| toascii(ch) | Returns the ASCII code for ch |
| tolower(ch) | Returns the lowercase version of ch if ch is an uppercase letter; otherwise returns ch |
| toupper(ch) | Returns the uppercase version of ch if ch is a lowercase letter; otherwise returns ch |

### cmath

The C++ functions in this library compute certain standard mathematical functions. These functions are overloaded to accommodate `float`, `double`, and `long double`. Unless otherwise indicated, each function has one argument, with the return type being the same as the argument type (either `float`, `double`, or `long double`).

- `acos(x)` Returns the arc cosine
- `asin(x)` Returns the arc sine
- `atan(x)` Returns the arc tangent
- `atan2(x, y)` Returns the arc tangent of x/y
- `ceil(x)` Rounds up
- `cos(x)` Returns the cosine
- `cosh(x)` Returns the hyperbolic cosine
- `exp(x)` Returns e raised to the power x
- `fabs(x)` Returns the absolute value
- `floor(x)` Rounds down
- `fmod(x, y)` Returns x modulo y
- `log(x)` Returns the natural log
- `log10(x)` Returns the log base 10
- `modf(x, iptr)` For arguments x and iptr, returns the fractional part of x and sets iptr to point to the integer part of x
- `pow(x, y)` Returns x raised to the power y
- `sin(x)` Returns the sine
- `sinh(x)` Returns the hyperbolic sine
- `sqrt(x)` Returns the square root
- `tan(x)` Returns the tangent
- `tanh(x)` Returns the hyperbolic tangent

### cstdlib

- `abort()` Terminates program execution abnormally
- `abs(x)` Returns the absolute value of an integer
- `atof(s)` Converts a string argument to floating point
- `atoi(s)` Converts a string argument to an integer
- `exit(x)` Terminates program execution, returns x to the operating system
- `rand()` Returns a pseudorandom integer
- `srand(x)` Initializes the pseudorandom number generator to x
- `srand()` Initializes the pseudorandom number generator to 1

### cstring

This library enables you to manipulate C strings that end in \0. Unless noted otherwise, these functions return a pointer to the resulting string in addition to modifying an appropriate argument. The argument ch is a character, n is an integer, and the other arguments are strings.

- `strncat(tos, fromS, n)` Copies at most n characters of fromS to the end of toS and appends '\0'
- `strcmp(str1, str2)` Returns an integer that is negative if str1 < str2, zero if str1 == str2, and positive if str1 > str2
- `strcmpi(str1, str2)` Behaves like strcmp, but ignores case
- `strncmp(str1, str2, n)` Behaves like strcmp, but compares the first n characters of each string
- `strncpy(tos, fromS, n)` Copies n characters of fromS to toS, truncating or padding with '\0' as necessary
- `strspn(str1, str2)` Returns the number of initial consecutive characters of str1 that are not in str2
- `strcspn(str1, str2)` Returns the number of initial consecutive characters of str1 that are in str2
- `strlen(str)` Returns the length of str, excluding '\0'
- `strlwr(str)` Converts any uppercase letters in str to lowercase without altering other characters
- `strupr(str)` Converts any lowercase letters in str to uppercase without altering other characters
- `strchr(str, ch)` Returns a pointer to the first occurrence of ch in str; otherwise returns null ptr
- `strrchr(str, ch)` Returns a pointer to the last occurrence of ch in str; otherwise returns null ptr
- `strpbrk(str1, str2)` Returns a pointer to the first character in str1 that also appears in str2; otherwise returns null ptr
- `strstr(str1, str2)` Returns a pointer to the first occurrence of str2 in str1; otherwise returns null ptr
- `strtok(str1, str2)` Finds the next token in str1 that is followed by str2, returns a pointer to the token, and writes null ptr immediately after the token in str1

### fstream

Defines the C++ classes that support file I/O.

### iomanip

The manipulators in this library affect the format of stream operations. Note that iostream contains additional manipulators.

- `setbase(b)` Sets number base to b = 8, 10, or 16
- `setfill(f)` Sets fill character to f
- `setprecision(n)` Sets floating-point precision to integer n
- `setw(n)` Sets field width to integer n

### iostream

The manipulators in this library affect the format of stream operations. Note that iomanip contains additional manipulators.

- `dec` Tells the subsequent operation to use decimal representation
- `endl` Inserts the new-line character \n and flushes the output stream
- `ends` Inserts the null character \0 into an output stream
- `flush` Flushes an output stream
- `hex` Tells the subsequent I/O operation to use hexadecimal representation
- `oct` Tells the subsequent I/O operation to use octal representation
- `ws` Extracts whitespace characters from the input stream

### stdexcept

Defines several exception classes that can be thrown or extended for specific exceptional conditions.

### string

This library enables you to manipulate C++ strings. Described here is a selection of the methods that this library provides. In addition, you can use the following operators with C++ strings: =, +, +=, [], <, <<, >>, <, <=, and >>. Note that positions within a string begin at 0.

- `erase()` Makes the string empty
- `erase(pos, len)` Removes the substring that begins at position pos and contains len characters
- `find(subString)` Returns the position of the substring subString within the string
- `length()` Returns the number of characters in the string (same as size)
- `replace(pos, len, str)` Replaces the substring that begins at position pos and contains len characters with the string str
- `size()` Returns the number of characters in the string (same as length)
- `substr(pos, len)` Returns the substring that begins at position pos and contains len characters
