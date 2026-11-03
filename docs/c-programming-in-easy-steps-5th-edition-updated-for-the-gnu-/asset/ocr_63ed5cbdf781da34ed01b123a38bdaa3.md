# Assessing logic

The logical operators most commonly used in C programming are listed in the table below:

![](bbox=[0.12, 0.33, 0.28, 0.46])

| Operator: | Operation: |
|---|---|
| && | Logical AND |
| || | Logical OR |
| ! | Logical NOT |

The logical operators are used with operands that have the Boolean values of true or false, or an expression that can convert to true or false.

The logical && AND operator will evaluate two operands and return true only if both operands are themselves true. Otherwise, the && AND operator will return false.

This is used in conditional branching, where the direction of a C program is determined by testing two conditions. If both conditions are satisfied, the program will go in a certain direction, otherwise it will take a different direction.

Unlike the && AND operator that needs both operands to be true, the || OR operator will evaluate two operands and return true if either one of the operands is itself true. If neither operand is true then the || OR operator will return false. This is useful in C programming to perform a certain action if either one of two test conditions has been met.

The third logical ! NOT operator is a “unary” operator – that is used before a single operand. It returns the inverse value of the given operand, so if the variable var is a true value then !var would return a false value. The ! NOT