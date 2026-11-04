
## Table 2.4: Operators in C# 2010

| Category | Operators | Description |
|---|---|---|
| Primary | x.y | Dot operator: Accesses the member variables and methods of a class. |
| Primary | f(x) | Parenthesis: Specifies the operation order in an expression as well as performs type conversions. It can also be used to invoke a delegate or method. |
| Primary | a[x] | Square brackets: Specifies that square brackets can be used with arrays, indexers, pointers, and attributes. |
| Primary | x++ | Post-Increment operator: Increases the value of its operand (x) by 1. It first assigns the value of x and then increments its value. |
| Primary | x-- | Post-Decrement operator: Decreases the value of its operand (x) by 1. It first assigns the value of x and then decrements its value. |
| Primary | new | new operator: Creates objects and calls constructors. |
| Primary | typeof | typeof operator: Allows you to discover the information about reference and value types using the Type object. |
| Primary | checked | checked operator: Detects the overflow conditions in integral-type arithmetic operations and conversions. |
| Primary | unchecked | unchecked operator: Ignores the error caused by the overflow conditions and accepts the generated result, regardless of the overflow conditions. |
| Primary | -> | Pointer operator: Combines pointer dereferencing and member access. |
| Unary | + | Unary Plus operator: Specifies that this operator is predefined for all numeric types and the result of a unary + operation on a numeric type is always the value of the operand. For example when you execute the following code snippet, the result displayed is 7 as the result of a unary + operation on 7 is always the value of the operand (7): `int x = 7;` `Console.WriteLine(+x);` |
| Unary | - | Unary minus operator: Specifies that this operator is predefined for all numeric types and the result of a unary - operation on a numeric type is the numeric negation of the operand. For example when you execute the following code snippet, the result displayed is -7 as the result of a unary - operation on 7 is always the numeric negation of the operand (7): `int x = 7;` `Console.WriteLine(-x);` |
| Unary | ! | Logical negation operator: Inverts the result of a Boolean expression. |
| Unary | ~ | Bitwise complement operator: Inverts the binary representation of an expression. |
| Unary | ++x | Pre-increment operator: Increases the value of its operand (x) by 1. The pre-increment operation returns the value of the operand (x) after it has been incremented. |
| Unary | --x | Pre-decrement operator: Decreases the value of its operand (x) by 1. The pre-decrement operation returns the value of the operand (x) after it has been decremented. |
| Unary | (T)x | Parenthesis: Specifies the operation order in the expression as well as converts the types. It can also be used to invoke a delegate or method. |
| Unary | true | true operator: Returns the Boolean value, true when an expression does not satisfy a specified condition |
| Unary | false | false operator: Returns the Boolean value, false to indicate that an expression does not satisfy a specified condition. |
| Unary | & | Address operator: Returns the address of its operand. |
| Unary | sizeof | sizeof operator: Returns the size of value types in bytes. |
| Multiplicative | * | Multiplication operator: Computes the product of its operands. |
| Multiplicative | / | Division operator: Computes the division of its operands by dividing the first operand by the second operand. |
| Multiplicative | % | Modulus operator: Computes the remainder of its operands after dividing the first operand by the second operand. |
| Additive | + | Binary plus operator: Computes the sum of its operands. |
| Additive | - | Binary minus operator: Computes the difference of its operands. |
| Shift | << | Left shift operator: Shifts its first operand to left by the number of bits specified by the second operand. The number of bits should be of an integer value. |
| Shift | >> | Right shift operator: Shifts its first operand to right by the number of bits specified by the second operand. The number of bits should be of an integer value. |
| Relational and type testing | < | Less than operator: Finds out if the first operand is less than the second operand. It returns true if the condition satisfies; otherwise returns false. |
| Relational and type testing | > | Greater than operator: Finds out if the first operand is greater than the second operand. It returns true if the condition satisfies; otherwise returns false. |
| Relational and type testing | <= | Less than equal to operator: Finds out if the first operand is less than or equal to the second operand. It returns true if the condition satisfies; otherwise returns false. |
| Relational and type testing | >= | Greater than equal to operator: Finds out if the first operand is greater than or equal to the second operand. It returns true if the condition satisfies; otherwise returns false. |
| Relational and type testing | is | is operator: Checks the compatibility of a variable with a given type. |
| Relational and type testing | as | as operator: Performs conversions between the compatible reference types. |
| Equality | == | Equality operator: Checks whether the two expressions are same or not. It returns true if the expressions are equal; otherwise it returns false. |
| Equality | != | Inequality operator: Checks whether the two expressions are same or not. It returns true, if the expressions are not equal; otherwise returns false. |
| Logical AND | & | Logical AND: Computes the logical AND of its Boolean operands. For integral operands, (&), the Logical AND operator compares the corresponding bits of two integrals and computes the logical bitwise AND of the operands. It returns true if and only if both of its operands are true. It can be used as a unary or binary operator. |
| Logical XOR | ^ | Logical XOR: Computes the logical exclusive OR of its Boolean operands. It returns true, if and only if one of its operands is true. |
| Logical OR | \| | Logical OR: Computes the logical OR of its Boolean operands. For integral operands, \| it compares the corresponding bits of two integrals and computes the logical bitwise OR of the operands. It returns true if and only if, any one of its operands is true. |
| Conditional AND | && | Logical AND: Used to compute the logical AND of its Boolean operands. It evaluates the second operand whenever necessary and returns true, if and only if both its operands are true. |
| Conditional OR | \|\| | Logical OR: Computes the logical OR of its Boolean operands. It evaluates the second operand whenever necessary and returns true, if and only if any of its operands is true. |
| Null-coalescing | ?? | Null-coalescing operator: Defines a default value for a nullable value type as well as reference type. Returns the left operand, if it is not null; otherwise it returns the right operand. |
| Conditional | ?: | Conditional operator: Returns one of the two values based on the result produced by the Boolean expression. |
| Assignment | = | Equal operator: Assigns a value to a variable, property, or an indexer. |
| Assignment | += | Addition assignment operator: Assigns the result of the sum of the first and second operands to the first operand itself. |
| Assignment | -= | Subtraction assignment operator: Assigns the result of the difference of the first and second operands to the first operand itself. |
| Assignment | *= | Multiplication assignment operator: Assigns the result of the product of the first and second operands to the first operand itself. |
| Assignment | /= | Division assignment operator: Assigns the result of the division of the first operand by second operand to the first operand itself. |
| Assignment | %= | Modulus assignment operator: Assigns the remainder of the division of the first operand by second operand to the first operand itself. |
| Assignment | &= | AND assignment operator: Assigns the logical AND of the first operand and second operand to the first operand itself. |
| Assignment | \|= | OR assignment operator: Assigns the logical OR of the first operand and second operand to the first operand itself. |
| Assignment | ^= | XOR assignment operator: Assigns the logical XOR of the first operand and second operand to the first operand itself. |
| Assignment | <<= | Left-shift assignment operator: Assigns the left shift result of the first operand and second operand to the first operand itself. |
| Assignment | >>= | Right-shift assignment operator: Assigns the right shift result of the first operand and second operand to the first operand itself. |
| Lambda | => | Lambda operator: Separates the input variable on the left side from the statement block or expressions on the right. |

You have learned about operators in C#, next, let's learn to use these operators in an application.
