In C, a % prefix denotes a format specifier. All printf() format specifiers are listed below, and those for scanf() here.

| Character: | printf() converts to: |
|---|---|
| d , i | int data type, signed decimal |
| o | int data type, unsigned octal without a leading zero |
| x , X | int unsigned hexadecimal. 0x uses lowercase, such as 0xff, and 0X uses uppercase, such as 0XFF |
| u | int data type, unsigned decimal |
| c | int single character, after conversion to char data type |
| s | char pointer to string, ending with the \0 null character |
| f | double data type in the form xxx.yyyyyy where the number of digits after the decimal point is set by precision. The default precision is 6 digits |
| e , E | double data type in the form xx.yyyyyy±zz or xx.yyyyyyE±zz where the number of digits after the decimal point is set by precision. The default precision is 6 digits |
| g , G | double data type printed as %e or %E conversion or %f conversion, whichever is shorter |
| p | the memory address of a pointer |
| n | not a conversion, but stores the number of characters written so far by the call to the printf() function in an int pointer argument |
| % | not a conversion; prints a % |

<stdio.h>

# Format specifiers for output

| Character: | scanf() converts to: |
|---|---|
| d | int data type, signed decimal integer |
| i | int data type, which may be in octal (leading 0) or hexadecimal (leading 0x or 0X) |
| o | int data type, octal integer with or without a leading zero |