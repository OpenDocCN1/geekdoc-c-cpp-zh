# Chapter 4

# 179

the following are invalid:

```
length <= 50      // operator out of order
2.0 >> 3.3      // invalid operator
flag = done      // spaces are not allowed
```

Table 4.1 C++ Relational Operators

| Relational Operator | Meaning | Example |
|---|---|--|
| < | Less than | age < 30 |
| > | Greater than | height > 6.2 |
| <= | Less than equal to | taxable <= 20000 |
| >= | Greater than equal to | temp >= 98.6 |
| == | Equal to | grade == 100 |
| != | Not equal to | number != 25 |

The relational expression and condition are frequently used as synonyms, and both terms are used interchangeably in this book. Like all C++ expressions, relational expressions are evaluated to yield a numerical result. In a relational expression, the value of the expression can be only the integer 1 or 0. These values are interpreted as true and false, respectively. A relational expression's true evaluates to an integer value of 1, and a relational expression's false evaluates to an integer value of 0.

For example, because the relationship 3 < 4 is true, this expression has a value of 1, and the relationship 2.0 > 3.0 is false, the value of the expression is 0. This rule is illustrated by the following statements:

```
cout << "The value of 3 < 4 is " << (3 < 4) << endl;
cout << "The value of 2.0 > 3.0 is " << (2.0 > 3.0) << endl;
cout << "The value of true is " << true << endl;
cout << "The value of false is " << false << endl;
```

which results in this:

```
The value of 3 < 4 is 1
The value of 2.0 > 3.0 is 0
The value of true is 1
The value of false is 0
```

A value of a relational expression as hours > 40 depends on the value stored in the variable hours. In a C++ program, a relational expression's value isn't as important as the interpretation C++ places when the expression is used as part of a selection statement. In these statements, which are explained in the next section, you'll see that C++ uses a zero value to represent a false condition and any non-zero value to represent a true condition. The selection of which statement to execute next is based on the value.

In addition to numerical operands, character data can be compared using relational operators. For these comparisons, the char values are coerced to int values automatically for comparison. For example, in Unicode, the letter 'A' is stored by a code for the letter 'B' has a lower numerical value than the

> In this regard, C++ differs from other high-level languages, which yield a Boolean (true or false).