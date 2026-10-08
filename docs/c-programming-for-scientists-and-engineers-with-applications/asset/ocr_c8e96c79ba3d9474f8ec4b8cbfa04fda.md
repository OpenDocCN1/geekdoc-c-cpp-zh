# 4.1 Relational and Logical Operations

Given the relational expression a > b gives a logical value of false and this value is used to evaluate the logical expression containing the ! operator. The result of this logical expression is true. In a parentheses-free expression, a relational operator has higher priority than a logical operator.

Given the following logical values and relational expressions, the logical expressions are evaluated as follows:

```
expr1 = true, expr2 = false, expr3 = false, and expr4 = true
```

```
expr1 && expr2 is false
expr1 || expr3 is true
expr1 || expr2 && expr4 is true
expr2 || expr1 && expr4 is true
!(expr1) && expr4 is false
expr1 && expr4 is false
expr1 && (expr2 || expr3) is false
expr1 && !(expr2 || expr3) is true
```

The following expressions show the precedence of the operators. They are equivalent for all values of the expression. Therefore the parentheses are not needed.

```
expr1 || (expr2 && expr3) and expr1 || expr2 && expr3
expr1 || !expr2 && expr4 and expr1 || ((expr2) && expr4)
expr3 && (!expr4) and expr3 && !expr4
(!expr2) || expr3 and !expr2 || expr3
expr1 && expr2 || expr3 and (expr1 && expr2) || expr3
```

Parentheses may be used to change the order of the evaluation of the logical expressions. The following examples show the use of parentheses:

```
expr1 && (expr2 && expr3) in this expression expr2 || expr3 is
evaluated first and then && is evaluated.
```

```
!(expr1 || expr2 || expr3) in this expression expr1 ||
expr2 || expr3 is evaluated first and then
! is evaluated.
```