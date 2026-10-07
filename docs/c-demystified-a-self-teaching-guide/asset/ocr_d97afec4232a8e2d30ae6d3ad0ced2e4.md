# Relational Operators

We compare values all the time, and so do programs. A program may need to determine whether one value is equal to, greater, or less than any value. For example, if a program calculates the cost of a ticket to a movie in which children less than 12 get free, it needs to find out the customer's age is less than 12.

Programs compare values using a relational operator. Table 5-1 lists the relational operators supported by C++.

Table 5-1: Relational Operators

| Operator | Meaning |
| --- | --- |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal to |
| <= | Less than or equal to |
| == | Equal to |
| != | Not equal to |

# Relational Expressions

Like the arithmetic operators discussed in the last chapter, the relational operators are binary—that is, they compare two operands. A statement with two operands and a relational operator between them is called a *relational expression*.

The result of a relational expression is a Boolean value, depicted either true or false. Table 5-2 lists several relational expressions, using different relational operators and their values.

Table 5-2: Relational Expressions and Their Values

| Relational Expression | Value |
| --- | --- |
| 4 == 4 | true |
| 4 < 4 | false |
| 4 <= 4 | true |
| 4 > 4 | false |
| 4 != 4 | false |
| 4 == 5 | false |
| 4 < 5 | true |
| 4 <= 5 | true |
| 4 > 5 | false |
| 4 != 5 | true |