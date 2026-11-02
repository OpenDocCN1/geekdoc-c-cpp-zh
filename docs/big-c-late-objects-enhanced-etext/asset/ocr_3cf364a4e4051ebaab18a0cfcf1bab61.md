# Syntax 3.2 Comparisons

![](bbox=[0.27, 0.16, 0.95, 0.62])

EXAMPLE CODE See sec02 of your companion code for a program that compares numbers and strings.

Table 2 summarizes how to use relational operators in C++.

| Expression | Value | Comment |
|---|---|---|
| 3 <= 4 | true | 3 is less than 4; <= tests for "less than or equal". |
| 3 =< 4 | Error | The "less than or equal" operator is <=, not =<. The "less than" symbol comes first. |
| 3 > 4 | false | > is the opposite of <=. |
| 4 < 4 | false | The left-hand side must be strictly smaller than the right-hand side. |
| 4 <= 4 | true | Both sides are equal; <= tests for "less than or equal". |
| 3 == 5 - 2 | true | == tests for equality. |
| 3 != 5 - 1 | true | != tests for inequality. It is true that 3 is not 5 - 1. |
| 3 = 6 / 2 | Error | Use == to test for equality. |
| 1.0 / 3.0 == 0.333333333 | false | Although the values are very close to one another, they are not exactly equal. See Common Error 3.3. |
| "10" > 5 | Error | You cannot compare a string to a number. |