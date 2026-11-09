| Operator | Operation | Precedence number |
|---|---|---|
| ^ | exponentiation (raises a number to a power) | 1 |
| - | negation (reverses the sign of a number) | 2 |
| *, / | multiplication and division | 3 |
| \ | integer division | 4 |
| Mod | modulus | 5 |
| +, - | addition and subtraction | 6 |

**Figure 6-5:** Most commonly used arithmetic operators and their order of precedence

Some of the operators in Figure 6-5 have the same precedence number. For example, both the addition and subtraction operators have a precedence number of 6. When an expression contains more than one operator having the same priority, those operators are evaluated from left to right. In the expression 5 + 12 / 3 - 1, for instance, the division is performed first, then the addition, and then the subtraction. The result of the expression is the number 8, as illustrated in Figure 6-6. You can use parentheses to change the order in which the operators in an expression are evaluated. For example, the expression 5 + 12 / (3 - 1) evaluates to 11 rather than to 8, as illustrated in Figure 6-6. This is because the parentheses tell the computer to perform the subtraction operation first.

```
Original expression                 5 + 12 / 3 - 1
The division is performed first   5 + 4 - 1
The addition is performed next    9 - 1
The subtraction is performed last 8                     result

Original expression                 5 + 12 / (3 - 1)
The subtraction is performed first 5 + 12 / 2
The division is performed next    5 + 6
The addition is performed last    11                    result
```

**Figure 6-6:** Examples showing how expressions are evaluated

Two of the arithmetic operators in Figure 6-5 might be less familiar to you: the integer division operator (\) and the modulus operator (Mod). You use the **integer division operator** (\) to divide two integers (whole numbers), and then return the result as an integer. For example, the expression 211 \ 4 results in 52, which is the integer result of dividing 211 by 4. (If you use the standard division operator [/] to divide 211 by 4, the result is 52.75 rather than 52.) You might use the integer division operator in a program that determines the number of quarters, dimes, and nickels to return as change to a customer. For instance, if a customer should receive 53 cents in change, you could use the expression 53 \ 25 to determine the number of quarters to return; the expression evaluates to 2.