# 6.16 THE LOGICAL OPERATORS

In real-life programming, decisions can’t always be made by making simple relational tests. C handles complex decision making using the following three *logical operators*:

+   - `&&` represents logical AND
+   - `||` represents logical OR
+   - `!` represents logical NOT

The first two operators are binary while the third one is unary. These operators are meant to be used with relational expressions even though any expression that evaluates to a value is a valid operand for them.

# 6.16.1 The && || Operators

The logical operators, `&&` and `||`, evaluate two expressions *exp1* and *exp2* individually as true or false and then use these values to evaluate the combined or compound expression as true or false. The syntax of both operators are shown below:

| Syntax | Meaning |
|---|---|
| `exp1 && exp2` | *exp1* and *exp2* evaluate to true or false |
| `exp1 || exp2` | Ditto |

`&&` and `||` are also known as the logical AND and logical OR operators, respectively. They conform to the truth tables of the AND and OR gates, respectively (Figs. 3.1 and 3.2). Thus, the value of the compound expression is true when

+   - in the case of `&&`, both *exp1* and *exp2* individually evaluate to true.
+   - in the case of `||`, at least one of them is true.

Here’s an example of a compound expression that uses the `&&` with two relational expressions as its operands:

```
a > 0 && b > 0
```

If a has the value 0 and b has the value 5, the resultant expression evaluates to false because the first expression is false. Now, let’s replace the `&&` in the previous expression with `||`:

```
a > 0 || b > 0
```

Assuming the same values of a and b, the compound expression is true because one of the expressions is true (b > 0). In both cases, evaluation will begin from the left but it will stop mid-way if the outcome of the entire expression has already been determined. For the `&&`, evaluation stops if a > 0 is false. For the `||`, evaluation stops if a > 0 is true.

Both operators have a precedence lower than the relational operators but higher than the assignment ones (Table 6.2). Thus, no parentheses are needed to enclose the relational expressions. Between themselves, the `&&` has a higher priority than the `||`, but both have L-R associativity.

Chapters 7 and 8 fully exploit the power of the logical operators. It could still be helpful to know how they are used in a program, say, by an *if* statement: