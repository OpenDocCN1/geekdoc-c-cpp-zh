# 4.1.2 Logical Operators and Logical Expressions

In C there are three logical operators. The logical operators are && (AND), || (OR), and ! (NOT). The logical operators && and || are binary requiring two operands and ! is a unary operator requiring one operand. The order of evaluation of the logical operators are as follows: ! evaluated first, followed by the && operator, and then by the || operator in a parentheses-free expression. if there are parentheses then the expression inside the parentheses is evaluated first. The operands of a logical expression must have logical values. The following tables show the results of logical operators &&, ||, and !.

**Operator:** The result of the && operator is true only if both operands are true, otherwise it is false. The following table shows the result of the && operation.

| var1 | var2 | var1 && var2 |
| --- | --- | --- |
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

a && b is the C code of saying that a and b are both true, a claim about a and b that may be true or may false. For example (x > 0 && y > 0) claims that x and y are both positive.

**Operator:** The result of the || operator is “true” if one of the operands is true or both operands are true, otherwise it is false. The following table shows the result of the || operation.

| var1 | var2 | var1 || var2 |
| --- | --- | --- |
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

a || b is the C code way of saying that a and b are not both false, but at least one of them is true. For example (x > y || x > z) claims that x is not the smallest of the three numbers.