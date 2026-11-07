we have an expression of different levels of precedence; associativity is used when we have expressions of the same precedence.

Overflow and underflow define the rules for determining what happens when a number is either too large or too small for a variable.

Sometimes we need to format data. This is done with the help of predefined objects called manipulators. We have manipulators for outputting data and manipulators for inputting data.

To write a program in C++, we need statements. C++ provides many different types of statements, each with a pre-defined task. We discuss five types of statements in this chapter: declaration statement, expression statement, null statement, compound statement, and return statement.

Program design is a process that needs to be carefully followed using at least three steps: understanding the program, developing algorithms, and writing the code.

# ## Problems

+   - **PR-1.** Evaluate the following integer expressions in decimal. Find any errors.
+     a. `0723`    b. `0491`
+     c. `-0241`   d. `-0412`
+   - **PR-2.** Evaluate the following integer expressions in decimal. Find any errors.
+     a. `-0x1A12`    b. `-0xH21B`
+     c. `0xA2EF`      d. `0x4`
+   - **PR-3.** Evaluate the following floating-point expressions. Find any errors.
+     a. `0.0712F`    b. `6.0712`
+     c. `1.234E2`    d. `1123E-2`
+   - **PR-4.** Evaluate the following expressions.
+     `3 + 7 * 2`    `4 * 2 + 7`    `7 / 4 + 3 * 4`
+   - **PR-5.** Evaluate the following expressions.
+     `4 / 3 * 6 / 2 + 8 % 3`    `24 % 5 + 16 % 5 * 4 / 2`
+   - **PR-6.** Assume x = 3, y = 5, and z = 6. Evaluate the following expressions (assume each expression is independent).
+     `x - 3 + y * 2 - z / 2`    `(x + 2) % (y * y)`
+   - **PR-7.** Assume x = 3, y = 5, and z = 6. Evaluate the following expressions (assume each expression is independent).
+     `(y / 3 + x) * z % x`    `y - 2 - x * y`
+   - **PR-8.** Assume x = 4 and y = 2. Find the value of x after evaluating each of the following expressions.
+     `x -= y - 2;`    `x += y + 2;`
+   - **PR-9.** Assume x = 4, y = 2, and z = 5. Find the value of z after evaluating each of the following expressions.
+     `z /= x + y + 4;`    `z %= y * 2 + 3;`