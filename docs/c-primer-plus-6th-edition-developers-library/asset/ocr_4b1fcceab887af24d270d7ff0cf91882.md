# Summary: Operating in C

Here are the operators we have discussed so far:

# Assignment Operator:

= Assigns the value at its right to the variable at its left.

# Arithmetic Operators:

+ Adds the value at its right to the value at its left.
- Subtracts the value at its right from the value at its left.
- As a unary operator, changes the sign of the value at its right.
* Multiplies the value at its left by the value at its right.
/ Divides the value at its left by the value at its right. The answer is truncated if both operands are integers.
% Yields the remainder when the value at its left is divided by the value to its right (integers only).
++ Adds 1 to the value of the variable to its right (prefix mode) or to the value of the variable to its left (postfix mode).
-- Like ++, but subtracts 1.

# Miscellaneous Operators:

sizeof Yields the size, in bytes, of the operand to its right. The operand can be a type specifier in parentheses, as in sizeof (float), or it can be the name of a particular variable, array, and so forth, as in sizeof foo.

(type) As the cast operator, converts the following value to the type specified by the enclosed keyword(s). For example, (float) 9 converts the integer 9 to the floating-point number 9.0f.

# Function with Arguments

By now, you’re familiar with using function arguments. The next step along the road to function mastery is learning how to write your own functions that use arguments. Let’s preview that skill now. (At this point, you might want to review the butler() function example near the end of Chapter 2, “Introducing C”; it shows how to write a function without an argument.) Listing 5.15 includes a pound() function that prints a specified number of pound signs (#). (This symbol also is called the number sign and the hash symbol.) The example also illustrates some points about type conversion.