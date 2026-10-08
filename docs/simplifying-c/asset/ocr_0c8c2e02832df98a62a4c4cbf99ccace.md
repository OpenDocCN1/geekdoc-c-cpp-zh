It can be observe in Figure 4 that an identifier has name, value, and address. At times we need to utilize the value of the identifier in an expression and make use of the name of the identifier. On the other hand, if we want to store a value that is entered by the user, we refer to an address of the identifier. In C, the address of an identifier is accessed by prefixing ampersand (&) symbol to the identifier name. The most common mistake the new programmers make is that they do not use the ampersand (&) symbol at the time of reading the data. Let us now have a look at how the formatted functions work.

# Input Function

The activity to accept input from a user happens in almost all programs. C language provides a predefined function called scanf to take the input. The syntax of the function is as follows:

```
```c
scanf("format string", address list of identifiers);
```
```

The preceding syntax consists of two parts, namely, a format specifier that identifies the data type and an address list of identifiers. The format string consists of certain predefined set of alphabets. Each alphabet refers to a specific data type. It is possible to read multiple data in one scanf call. In this case, the format specifier will contain the format code usually separated by a space, and the address list will contain addresses of the identifiers in which the data needs to be stored. Table 2 is the list of format specifier that is used for reading or writing data:

Table 2: Format Specifier String
| Data Value | Data Type | Format code |
| :--- | :--- | :--- |
| Integer | short int / int | %d or %i |
| | unsigned int | %u |
| | long unsigned int | %lu |
| | long int | %ld |
| Hexadecimal | int | %x or %p |
| Octal | int | %o |
| Character | signed char | %c |
| | unsigned char | %c |
| | char * (String) | %s |
| Real | float | %f or %g |
| | double | %lf |
| | long double | %Lf |

It can be observed from Table 2 that we have different format specifier for different data types. The format specifier is required to be written in the order that we want the data to be entered. The programs written in earlier chapter has already used the function scanf. Program 1 illustrates the use of scanf function: