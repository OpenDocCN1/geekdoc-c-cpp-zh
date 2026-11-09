# CHAPTER 4

# Macro Functions

# 4.1 Types of Macro Functions

Macro programming is equipped with all the commonly used mathematical functions that are typically available in a high-level computer programming language. The available macro functions can be separated into groups, to make their understanding and usage easier to learn. There are broadly five groups, apart from the usual arithmetic operations:

+   - Trigonometric functions
+   - Rounding functions
+   - Miscellaneous functions
+   - Logical functions
+   - Conversion functions

A value may be assigned to a variable (or an expression that evaluates to a legal variable number) using any combination (that should, of course, be logically correct) of these functions. An unassigned (undefined) variable is called a null variable that is equivalent to 0 in mathematical calculations. So, as a general rule, a variable should not be used in any mathematical expression without first defining it.

# Priority of Operations in Arithmetic Expressions

In a complex expression, involving several functions and brackets, the following priority rule is followed:

+   1. Brackets (only square brackets are permitted)
+   2. Functions (such as SIN, ATAN, SQRT, and EXP)
+   3. Multiplication (*), division (/), and bitwise AND
+   4. Addition (+), subtraction (-), bitwise OR, and bitwise XOR

If more than one operation of equal priority appear in a row, the calculation is done from left to right.