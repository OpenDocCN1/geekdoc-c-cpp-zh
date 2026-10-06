# AN INTRODUCTION TO C AND PROGRAMMING

# ARITHMETIC SHORTHAND
allows shortcuts for some common operations (for example instead of typing a = a + 1 you can just enter a++ or a -= 3 a *= 3)

Don't forget to use %f instead of %d as the print specifier when changing
the int values to float values in the example

![](bbox=[0.063, 0.285, 0.936, 0.638])

# DECIMAL PLACES
you can set the number of decimal places to display for a floating-point type using
printf by putting a decimal point and the number of places between the % and the f
%.3f will show a float value with three digits after the decimal point

Other types
Another common variable type is char; a character value This is used, as the name suggests,
to store a single character The ASCII character encoding uses a single value between 0 and
127 for each letter, number, and punctuation symbol, so a char is a single byte; it's really just
an integer value which can only hold small numbers The compiler allocates several bytes to
to store an int or a float, but only allocates a single byte of memory to store a char.