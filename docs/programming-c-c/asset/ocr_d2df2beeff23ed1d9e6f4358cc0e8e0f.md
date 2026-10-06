# Introduction to C Language, Variables, Data Types and Operators

| | | |
| ^= | Bitwise exclusive OR and assignment operator. | C ^= 2 is as same as C = C ^ 2 |
| |= | Bitwise inclusive OR and assignment operator. | C |= 2 is as same as C = C | 2 |

# Special Conditional Operators

Besides the operators discussed above, there are a few other operators called operators including sizeof and ? : supported by the C Language.

| Operator | Description | Example |
| sizeof() | Returns the size of a variable. | sizeof(a), where a is integer, will return 4. |
| & | Returns the address of a variable. | &; returns the actual address of the variable. |
| * | Pointer to a variable. | *a; |
| : | Conditional Expression. | If condition is true ?, then value X : otherwise value Y |

# CONDITIONAL OR TERNARY OPERATORS IN C

Conditional operators return one value if condition is true and returns another value condition is false.

This operator is also called as ternary operator.

Syntax : (Condition?) true_value; false_value);
Example : (A > 100 ? 0 : 1);

In above example, if A is greater than 100, 0 is returned else 1 is returned. This is equal to if else conditional statements.

# Increment and Decrement Operator in C

Increment Operators are used to increase the value of the variable by one and Decrement Operators are used to decrease the value of the variable by one in C programs.

Both increment and decrement operator are used on a single operand and variable. So, it is called as a unary operator. Unary operators are having higher priority than the other operators it means unary operators are executed before other operators.