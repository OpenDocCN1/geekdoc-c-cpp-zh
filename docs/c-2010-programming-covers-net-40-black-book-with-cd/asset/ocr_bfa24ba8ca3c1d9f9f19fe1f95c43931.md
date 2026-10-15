# Table 2.6: Showing the Operators in C#

| Category | Operators | Description |
|---|---|---|
| Logical OR | | | Computes the logical OR of its Boolean operands. For integral operands, | compares the corresponding bits of two integrals and computes the logical bitwise OR of the operands. It returns true if and only if any one of its operands is true. |
| Conditional AND | && | Computes the logical AND of its Boolean operands. It evaluates the second operand whenever necessary and returns true if and only if both its operands are true. |
| Conditional OR | || | Computes the logical OR of its Boolean operands. It evaluates the second operand whenever necessary and returns true if and only if any of its operands is true. |
| Conditional | ?: | Returns one of the two values based on the result produced by the Boolean expression. |
| Assignment | = | Assigns a value to a variable, property, or indexer. |
| Assignment | += | Assigns the result of the sum of the first and second operands to the first operand. |
| Assignment | -= | Assigns the result of the difference of the first and second operands to the first operand. |
| Assignment | *= | Assigns the result of the product of the first and second operands to the first operand. |
| Assignment | /= | Assigns the result of division of the first operand by second operand to the first operand. |
| Assignment | %= | Assigns the remainder of the division of the first operand by second operand to the first operand. |
| Assignment | &= | Assigns the logical AND of the first operand and second operand to the first operand. |
| Assignment | |= | Assigns the logical OR of the first operand and second operand to the first operand. |
| Assignment | ^= | Assigns the logical XOR of the first operand and second operand to the first operand. |
| Assignment | <<= | Assigns the left shift result of the first operand and second operand to the first operand. |
| Assignment | >>= | Assigns the right shift result of the first operand and second operand to the first operand. |
| Null-coalescing | ?? | Returns one of the two values depending on the null values. It returns the left operand if its value is not null; otherwise, it returns the right operand. |
| Lambda | => | Separates the input variable on its left from the statements or expressions on its right. |
| Scope Resolution | :: | Defines the accessibility scope of the specified identifier |

As each and every operator in C# has its own value within an expression; therefore, C# provides them a precedence level that permits the C# compiler to execute the expression in a specific order. With a large set of operators in C#, you can use many of them simultaneously in an expression to perform required calculations. However, the use of two or more operators may result in conflict of the operator precedence, i.e. which operation is performed first. For this purpose, C# associates the precedence with each