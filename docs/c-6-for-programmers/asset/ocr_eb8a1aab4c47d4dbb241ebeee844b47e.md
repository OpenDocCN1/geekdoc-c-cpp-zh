+   - 50 displays as $50.00 in the United States (U.S.), as 50,00 e (e for euros) in Germany and many and as ¥50 in Japan.
+   - 4382.51 displays as $4,382.51 in the U.S., as 4.382,51 e in Germany and as ¥4,382 in Japan.
+   - 1254827.40 displays as $1,254,827.40 in the U.S., as 1.254,827,40 e in Germany and as ¥1,254,827 in Japan.

Figure 4.13 lists additional format specifiers.

| Format specifier | Description |
|---|---|
| C or c | Formats the string as currency. Includes an appropriate currency symbol ($ in the U.S.) next to the number. Separates digits with an appropriate separator character (in the U.S. its a comma between every three digits for thousands, millions, etc.) and sets the number of decimal places to two by default. |
| D or d | Formats the string as a whole number (integer types only). |
| N or n | Formats the string with a thousands separator and a default of two decimal places. |
| E or e | Formats the number using scientific notation with a default of six decimal places. |
| F or f | Formats the string with a fixed number of decimal places (two by default). |
| G or g | Formats the number normally with decimal places or using scientific notation, depending on context. If a format item does not contain a format specifier, format G is assumed implicitly. |
| X or x | Formats the string as hexadecimal (base 16 numbers; we discuss these in the online Number Systems appendix). |

Fig. 4.13 | string format specifiers.

# Reading a decimal Value from the User

Line 19 (Fig. 4.12) prompts the user to enter a deposit amount for account1. Line 20 declares local variable depositAmount to store each deposit amount entered by the user. Unlike instance variables (such as name and balance in class Account), local variables (like depositAmount in Main) are not initialized by default, so they normally must be initialized explicitly. As you'll learn momentarily, variable depositAmount's initial value will be determined by the user's input.

> **Common Programming Error 4.3**
> 
> The C# compiler will issue the compilation error "Use of unassigned local variable 'variableName'" if you attempt to use the value of an uninitialized local variable—in the error message, variableName will be the actual variable name. This helps you avoid dangerous execution-time logic errors. It's always better to get the errors out of your programs at compilation time rather than execution time.

Line 20 obtains the input from the user by calling the Console class's ReadLine method, then passing the string entered by the user to type decimal's Parse method, which returns the decimal value in this string—each simple type has a Parse method. Lines 21–22 display the deposit amount in currency format.