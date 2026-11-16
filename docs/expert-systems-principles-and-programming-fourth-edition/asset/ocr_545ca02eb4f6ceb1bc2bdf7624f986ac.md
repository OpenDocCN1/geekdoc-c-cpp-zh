**(multifieldp <expression>)**
Returns TRUE if <expression> is a multifield value, otherwise FALSE.

**(neq <expression>+)**
Returns TRUE if its first argument is not equal in type and value to all its subsequent arguments, otherwise FALSE.

**(not <expression>)**
Returns TRUE if its argument evaluates to FALSE, otherwise TRUE.

**(numberp <expression>)**
Returns TRUE if <expression> is a float or an integer, otherwise FALSE.

**(oddp <expression>)**
Returns TRUE if <expression> is an odd integer, otherwise FALSE.

**(or <expression>+)**
Returns TRUE if any of its arguments evaluate to TRUE, otherwise FALSE.

**(pointerp <expression>)**
Returns TRUE if <expression> is an external address, otherwise FALSE.

**(stringp <expression>)**
Returns TRUE if <expression> is a string, otherwise FALSE.

**(symbolp <expression>)**
Returns TRUE if <expression> is a symbol, otherwise FALSE.

**(= <numeric-expression> <numeric-expression>+)**
Returns TRUE if its first argument is equal in numeric value to all its subsequent arguments, otherwise FALSE.

**(< > <numeric-expression> <numeric-expression>+)**
Returns TRUE if its first argument is not equal in numeric value to all its subsequent arguments, otherwise FALSE.

**(> <numeric-expression> <numeric-expression>+)**
Returns TRUE if, for all its arguments, argument n - 1 is greater than argument n, otherwise FALSE.

**(>= <numeric-expression> <numeric-expression>+)**
Returns TRUE if, for all its arguments, argument n - 1 is greater than or equal to argument n, otherwise FALSE.

**(< <numeric-expression> <numeric-expression>+)**
Returns TRUE if, for all its arguments, argument n - 1 is less than argument n, otherwise FALSE.

**(<= <numeric-expression> <numeric-expression>+)**
Returns TRUE if, for all its arguments, argument n - 1 is less than or equal to argument n, otherwise FALSE.

# Procedural

**(bind <variable> <value>)**
Binds a variable to a specified value.

**(break)**
Terminates the execution of the while, loop-for-count, progn$, do-for-instance, do-for-all-instances, or delayed-do-for-all-instances function in which it is immediately contained.