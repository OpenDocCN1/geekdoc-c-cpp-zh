# Relational and Equality Operators

There are four relational operators and two equality operators found in the C programming language. Each of these operators are binary operators in which two operands are evaluated. The result of a relational expression is a logical (0, 1) value.

# Relational and Equality Operators (figure 5-4, page 236):

| Type | Operator | Meaning | Precedence |
|---|---|---|---|
| Relational | < | Less than | 10 |
| | <= | Less than or equal to | |
| | > | Greater than | |
| | >= | Greater than or equal to | |
| Equality | == | Equal to (equality) | 9 |
| | != | Not equal to (inequality) | |

# Compound Statements

It is possible combine a series of relational, equality, and logical operators to form what is called a compound statement. The result of such a statement (or expression) will be a (true or false) logical value.

The meaning of some compound logical expressions is clear when they contain only a single variable such as x > 0 && x < 10

Often a compound statement is made easier to read by including parentheses. Can you determine which of the expressions below is different than the other two?

# Example:

```
int x = 3;
int y = 2;
int z = 3;

printf("Result #1 = %d\n", x <= 3 || y >= 2 && z != 3);
printf("Result #2 = %d\n", x <= 3 || (y >= 2 && z != 3));
printf("Result #3 = %d\n", (x <= 3 || y >= 2) && z != 3);
```