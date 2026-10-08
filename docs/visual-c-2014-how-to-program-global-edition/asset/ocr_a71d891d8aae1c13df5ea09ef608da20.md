# 5.12 Compound Assignment Operators

# 5.12 Compound assignment operators

The compound variable operators abbreviate assignment expressions. Statements like

```
variable = variable expression;
```

where operator is one of the binary operators +, -, *, / or % (or others we discuss later in (the text) can be written in the form

```
operator= expression;
```

For example, you can abbreviate the statement

```
c = c + 3;
```

with the addition compound operator, +=, as

```
c += 3;
```

The += operator adds the value of the expression on its right to the value of the variable on its left and stores the result on the left of the operator. Thus, the assignment expression c += 3 adds 3 to c. Figure 5.14 shows the arithmetic compound assignment operators, examples using the operators and explanations of what the operators do.

| Assignment operator | Sample expression | Explanation | Assigns |
|---|---|---|--|
| Assume int c = 3, d = 5, e = 4, f = 6, g = 12; | | | |
| += | c = 7 | c = c + 7 | 10 to c |
| -= | d = 4 | d = d - 4 | 1 to d |
| *= | e = 5 | e = e * 5 | 20 to e |
| /= | f = 3 | f = f / 3 | 2 to f |
| %= | g = 9 | g = g % 9 | 3 to g |

**Fig. 5.14** | Arithmetic assignment operators.

# 5.13 Increment and Decrement Operators

C provides unary operators for adding 1 or subtracting 1 from the value of a numeric variable (summarized in Fig. 5.15). These are the increment operator, ++, and the decrement operator, --, respectively. An increment can change the value of a variable c using the increment operator, ++, rather than the expression c + 1 or c - 1. An increment or decrement operator that is prefixed (before) a variable is referred to as the prefix increment operator or prefix decrement operator, respectively. An increment or decrement operator that is posted (after) a variable is referred to as the postfix increment operator or postfix decrement operator, respectively.

Using the prefix (or decrement) operator to add 1 to (or subtract 1 from) a variable is known as preincrementing (or decrementing). This causes the variable to be incremented (decremented) by 1; then the new value of the variable is used in the expression in which it appears.