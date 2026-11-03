The operator ? : works as follows: exp1 is evaluated first. If it is nonzero (true), then the expression exp2 is evaluated and becomes the value of the expression. If exp1 is false, exp3 is evaluated and its value becomes the value of the expression. Note that only one of the expressions (either exp2 or exp3) is evaluated. For example, consider the following statements:

```
a = 10;
 b = 15;
 x = (a > b) ? a : b;
```

In this example, x will be assigned the value of b. This can be achieved using the if...else statements as follows:

```
if (a > b)
    x = a;
else
    x = b;
```

# 1.51 BITWISE OPERATORS

C has a distinction of supporting special operators known as bitwise operators for manipulation of data at bit level. These operators are used for testing the bits, or shifting them right or left. Bitwise operators may not be applied to float or double. Table 1.22 lists the bitwise operators and their meanings.

Table 1.22 Bitwise Operators

| Operator | Meaning |
|---|---|
| & | bitwise AND |
| | | bitwise OR |
| ^ | bitwise exclusive OR |
| << | shift left |
| >> | shift right |

# 1.52 SPECIAL OPERATORS

C supports some special operators of interest such as comma operator, sizeof operator, pointer operators (& and *) and member selection operators (. and ->). The comma and sizeof operators are discussed in this section while the pointer operators are discussed in Chapter 14. Member selection operators which are used to select members of a structure are discussed in Chapters 13 and 14.

# 1.52.1 The Comma Operator

The comma operator can be used to link the related expressions together. A comma-linked list of expressions are evaluated left to right and the value of right-most expression is the value of the combined expression. For example, the statement

```
value = (x = 10, y = 5, x+y);
```

first assigns the value 10 to x, then assigns 5 to y, and finally assigns 15 (i.e. 10 + 5) to value. Since comma operator has the lowest precedence of all operators, the parentheses are necessary. Some applications of comma operator are:

+   - In for loops:

```
for ( n = 1, m = 10, n <=m; n++, m++)
```