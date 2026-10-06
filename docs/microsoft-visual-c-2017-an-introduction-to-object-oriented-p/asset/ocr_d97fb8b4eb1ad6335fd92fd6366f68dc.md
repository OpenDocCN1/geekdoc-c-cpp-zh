# Chapter Summary

+   - A constant is a data value that cannot be changed after a program is compiled; a value in a variable can change. C# provides for 15 basic built-in types of data. A variable declaration includes a data type, an identifier, an optional assigned value, and a semicolon.

+   - You can display variables by using the variable name within a WriteLine() or Write() method call. To make producing output easier, you can combine strings and variable values into a single Write() or WriteLine() statement by using a format string.

+   - C# supports nine integral data types: byte, sbyte, short, ushort, int, uint, ulong, and char.

+   - C# supports three floating-point data types: float, double, and decimal. You can use format and precision specifiers to display floating-point data to a specified number of decimal places.

+   - You use the binary arithmetic operators +, -, *, and % to manipulate values in your programs. Multiplication, division, and remainder always take place prior to addition or subtraction in unless you use parentheses to override the normal precedence. C# provides several shortcut arithmetic operators, including the binary operators +=, -=, *=, /=, and the unary prefix increment (++) and decrement (--) operators.

+   - A bool variable can hold only two values—true or false. C# supports six comparison operators: >, <, <=, >=, ==, and !=. An expression can return a Boolean value.

+   - When you perform arithmetic with variables or constants of the same type, the result of the arithmetic retains that type. When you perform arithmetic operations with operands of different types, C# provides a unifying type for the result and implicitly converts nonforming operands to the unifying type. You can explicitly override the unifying type imposed by C# by performing a cast.

+   - You use the char type to hold any single character. You place constant character values within string quotation marks—including nonprinting characters such as a space or a tab—in a char variable. To store these characters, you must use an escape sequence, which begins with a backslash.

+   - In C#, you use the string type to hold a series of characters. The value of a string is expressed in double quotation marks. Although the == and != comparison operators can be used with string literals, you can also use the Equals(), Compare(), CompareTo(), and Substring() methods and the Length property that belongs to the String class.