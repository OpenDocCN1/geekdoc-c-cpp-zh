# 6.4.1  The +, -, * and /: The Four Basic Operators

The operators + and - are meant to do what everyone knows. Multiplication and division are handled by * and /. These four binary operators support a mix of integer and floating point operands which must have the right data types. Here are some situations that can cause problems:

+   - `256 * 256` — *Value is 65536; can’t hold in a short*
+   - `22 / 7` — *Value is 3 not 3.142!*
+   - `22.0 / 7` — *Value is 3.142857; 7 converted to 7.0*
+   - `5 / 0` — *Program aborts; division by zero not permitted*

As evident from the first example, the multiplication is the most common source of data overflow problems. The second example is an eye-opener; it evaluates to 3 because integer division leads to truncation of the decimal portion. The next example shows that an expression is evaluated using floating point arithmetic only if at least one operand is of the floating point type. Finally, your programs must have adequate checks to ensure that the denominator is never zero.

# 6.4.2  The %: The Modulus Operator

The other arithmetic operator we consider is the %, known as the *modulus operator*. This operator evaluates the remainder of a division between two integers. The expression 10 % 7 (10 modulo 7) evaluates to 3. Consider a few more examples:

+   - `55 % 2` — *Value is 1; suitable for odd or even number check*
+   - `21 % 7` — *Value is 0; suitable for day of the week check*
+   - `5 % 8.0` — *Error; only integers allowed*
+   - `-14 % 5` — *Implementation dependent; usually evaluates to -4*

As seen from the third example, the operation fails if one of the operands is a real number. The % provides a simple solution to some common tasks like checking for even or odd numbers and determining whether a year is a leap year or not.

**TABLE 6.1  The Arithmetic Operators**

| Operator | Significance |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus (integers only) |

# 6.5  computation.c: MAKING SIMPLE CALCULATIONS

Let’s use the arithmetic operators in our next program (Program 6.2). The program takes as input an even number from the user and computes the sum of all integers from 1 to the value that is input. The computation uses an interesting technique that is documented in the program itself. A validation check ensures that you don’t key in odd integers. The program is invoked three times but with only one successful outcome.