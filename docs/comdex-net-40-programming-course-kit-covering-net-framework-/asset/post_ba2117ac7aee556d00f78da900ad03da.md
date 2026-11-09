
## Table 1.2: Operators in C# 2010

| Operator Category | Operator Symbol | Description |
|---|---|---|
|  | `x++` (post-increment operator) | Returns the value of the operand (x) and after that increments its value by 1. |
|  | `x--` (post-decrement operator) | Returns the value of the operand (x) and after that decrements its value by 1. |
|  | `new` | Calls the constructor to create objects of classes. |
|  | `typeof` | Obtains the System.Type object for a data type. The System.Type object provides information about the data type. |
|  | `checked` | Enables the checking of the overflow conditions for integral-type operations and conversions. |
|  | `unchecked` | Prevents the checking of overflow for arithmetic operations and conversions on integral data types. |
| **Unary** | `+` (unary plus operator) | Represents an operator that is predefined for all numeric types. The result of a unary + operation on a numeric type is just the value of the operand. |
|  | `-` (unary minus operator) | Represents an operator that is predefined for all numeric types. The result of a unary − operation on a numeric type is the numeric negation of the operand. |
|  | `!` (logical negation operator) | Inverts the result of a Boolean expression. |
|  | `~` (bitwise complement operator) | Performs bitwise complement operation on its operand, that is, it reverses each bit of its operand. |
|  | `++x` (pre-increment operator) | Increases the value of its operand by 1 and then returns the value. |
|  | `--x` (pre-decrement operator) | Decreases the value of its operand by 1 and then returns the value. |
|  | `true` | Returns the Boolean value true, if the given expression satisfies the specified condition. |
|  | `false` | Returns the Boolean value false, if the given expression does not satisfy the specified condition. |
|  | `&` (address operator) | Returns the address of its operand. |
|  | `sizeof` | Returns the size of value types in bytes. |
| **Multiplicative** | `*` (multiplication operator) | Multiplies two operands and returns the result. |
|  | `/` (division operator) | Divides the first operand by the second operand and returns the quotient. |
|  | `%` (modulus operator) | Divides the first operand by the second operand and then returns the remainder. |
| **Additive** | `+` (binary plus operator) | Computes the sum of its operands. |
|  | `-` (binary minus operator) | Computes the difference of its operands. |
| **Shift** | `<<` (left shift operator) | Shifts the left-hand side operand towards left by the number of bits specified by the right-hand side operand, which has to be of int type. |
|  | `>>` (right shift operator) | Shifts the left-hand side operand towards right by the number of bits specified by the right-hand side operand, which has to be of int type. |
| **Relational and type testing** | `<` (less than operator) | Returns true if the left-hand side operand is less than the right-hand side operand. Otherwise, it returns false. |
|  | `>` (greater than operator) | Returns true if the left-hand side operand is greater than the right-hand side operand. Otherwise, it returns false. |
|  | `<=` (less than equal to operator) | Returns true if the left-hand side operand is less than or equal to the right-hand side operand. Otherwise, it returns false. |
|  | `>=` (greater than equal to operator) | Returns true if the left-hand side operand is greater than or equal to the right-hand side operand. Otherwise, it returns false. |
|  | `is` | Returns true if the left-hand side operand and the right-hand side operands are compatible. Otherwise, it returns false. |
|  | `as` | Performs conversion between reference types, if the types are compatible. Otherwise, it returns null. |
| **Equality** | `==` (equality operator) | Returns true if the value type operands have the same value, else returns false. For reference types (except string type), it returns true if the operands refer to the same object, else it returns false (value type and reference type are discussed later in this chapter). |
|  | `!=` (inequality operator) | Returns true if both the operands are unequal, otherwise, it returns false. |
| **Logical AND** | `&` (logical AND) | Returns true if and only if all the operands are true. |
| **Logical XOR** | `^` (logical XOR) | Returns true if and only if only one of its operands is true. |
| **Logical OR** | `\|` (logical OR) | Returns true if and only if at least one of the operands is true. |
| **Conditional AND** | `&&` (logical AND) | Performs logical AND on its Boolean operands. The right-hand side operand is evaluated only if the left-hand side operand evaluates to true. |
| **Conditional OR** | `\|\|` (logical OR) | Performs logical OR on its Boolean operands. The right-hand side operand is evaluated only if the left-hand side operand evaluates to false. |
| **Null-coalescing** | `??` (null-coalescing operator) | Returns one of the two values depending on the null values. It returns the left-hand side operand if its value is not null; otherwise, it returns the right-hand side operand. Only nullable data types support this operator. |
| **Conditional** | `?:` (conditional operator) | Returns one of the two values based on the result produced by the Boolean expression. |
| **Assignment** | `=` (equal operator) | Assigns a value to a variable, property, or an indexer. |
|  | `+=` (addition assignment operator) | Adds the right-hand side operand to the left-hand side operand and assigns the result back to the left-hand side operand. |
|  | `-=` (subtraction assignment operator) | Subtracts the right-hand side operand from the left-hand side operand and assigns the result back to the left-hand side operand. |
|  | `*=` (multiplication assignment operator) | Multiplies the right-hand side operand with the left-hand side operand and assigns the result back to the left-hand side operand. |
|  | `/=` (division assignment operator) | Divides the left-hand side operand by the right-hand side operand and assigns the quotient back to the left-hand side operand. |
|  | `%=` (modulus assignment operator) | Divides the left-hand side operand by the right-hand operand and assigns the remainder back to the left-hand side operand. |
|  | `&=` (AND assignment operator) | Performs bitwise or logical AND operation between the left-hand side and the right-hand side operands and assigns the result back to the left-hand side operand. |
|  | `\|=` (OR assignment operator) | Performs bitwise or logical OR operation between the left-hand side operand and the right-hand side operand and assigns the result back to the left-hand side operand. |
|  | `^=` (XOR assignment operator) | Performs bitwise or logical exclusive-OR operation with the left-hand side and the right-hand side operands and assigns the result back to the left-hand side operand. |
| **Lambda** | `=>` (lambda operator) | Separates the left-hand side operand from the right-hand side operand in a lambda expression. |

![](img/9862a98a1a2d3bb14334137965a1ec60_286_0.png)

> A lambda expression is a function that can contain expressions and statements. You learn more about lambda expressions in Chapter 6, LINQ in C# 2010, of section C# 2010.

Perform the following steps to use operators in a Console application:

- 1. *Start* Visual Studio 2010.
- 2. *Select* File→New→Project from the menu bar. The New Project dialog box opens (Fig. C#-1.3).
- 3. *Select* Visual C#→Windows from the Installed Templates section in the left pane of the New Project dialog box (Fig. C#-1.3). The lists of available project templates in C# are displayed in the middle pane of the New Project dialog box.
- 4. *Select* Console Application from the middle pane of the New Project dialog box, to create a Console application (Fig. C#-1.3).
- 5. *Enter OperatorExample* as the name of the application (also available on the CD) in the Name text box (Fig. C#-1.3).
