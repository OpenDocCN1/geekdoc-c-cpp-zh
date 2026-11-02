```
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 2
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Passed 9
Failed 1
Bonus to instructor!
```

**Fig. 3.10** | Analysis of examination results. (Part 3 of 3.)

# 3.11 Assignment Operators

C provides several assignment operators for abbreviating assignment expressions. For example, the statement

```
c = c + 3;
```

can be abbreviated with the addition assignment operator += as

```
c += 3;
```

The += operator adds the value of the expression on the *right* of the operator to the value of the variable on the *left* of the operator and stores the result in the variable on the *left* of the operator. Any statement of the form

```
variable = variable operator expression;
```

where *operator* is one of the binary operators +, −, *, / or % (or others we’ll discuss in Chapter 10), can be written in the form

```
variable operator= expression;
```

Thus the assignment c += 3 adds 3 to c. Figure 3.11 shows the arithmetic assignment operators, sample expressions using these operators and explanations.

| Assignment operator | Sample expression | Explanation | Assigns |
|---|---|---|---|
| *Assume: int c = 3, d = 5, e = 4, f = 6, g = 12;* |  |  |  |
| += | c += 7 | c = c + 7 | 10 to c |
| -= | d -= 4 | d = d - 4 | 1 to d |
| *= | e *= 5 | e = e * 5 | 20 to e |
| /= | f /= 3 | f = f / 3 | 2 to f |
| %= | g %= 9 | g = g % 9 | 3 to g |

**Fig. 3.11** | Arithmetic assignment operators.