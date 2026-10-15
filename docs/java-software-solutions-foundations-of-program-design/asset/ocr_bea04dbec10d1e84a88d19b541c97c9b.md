+   SR 2.15 How many values can be stored in an integer variable?
+   SR 2.16 What are the four integer data types in Java? How are they different?
+   SR 2.17 What type does Java automatically assign to an integer literal? How can you indicate that an integer literal should be considered a different type?
+   SR 2.18 What type does Java automatically assign to a floating point literal? How can you indicate that a floating point literal should be considered a different type?
+   SR 2.19 What is a character set?
+   SR 2.20 How many characters are supported by the ASCII character set, the extended ASCII character set, and the Unicode character set?

# 2.4 Expressions

An *expression* is a combination of one or more operators and operands that usually perform a calculation. The value calculated does not have to be a number, but it often is. The operands used in the operations might be literals, constants, variables, or other sources of data. The manner in which expressions are evaluated and used is fundamental to programming. For now we will focus on arithmetic expressions that use numeric operands and produce numeric results.

> KEY CONCEPT
> Expressions are combinations of operators and operands used to perform a calculation.

# Arithmetic Operators

The usual arithmetic operations are defined for both integer and floating point numeric types, including addition (+), subtraction (-), multiplication (*), and division (/). Java also has another arithmetic operation: The *remainder operator* (%) returns the remainder after dividing the second operand into the first. The remainder operator is sometimes called the modulus operator. The sign of the result of a remainder operation is the sign of the numerator. Therefore:

| Operation | Result |
|---|---|
| 17 % 4 | 1 |
| -20 % 3 | -2 |
| 10 % -5 | 0 |
| 3 % 8 | 3 |