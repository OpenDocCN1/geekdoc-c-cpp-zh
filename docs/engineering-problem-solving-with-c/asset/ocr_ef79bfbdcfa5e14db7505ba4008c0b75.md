| A | B | A && B | A || B | !A | !B |
|---|---|---|---|---|---|
| False | False | False | False | True | True |
| False | True | False | True | True | False |
| True | False | False | True | False | True |
| True | True | True | True | False | False |

values for a, b, and c, we can evaluate this condition as true or false. For example, if a is equal to 1, b is equal to 5, and c is equal to 8, then the condition is true. If a is equal to -2, b is equal to 9, and c is equal to 2, then the condition is false.

If A and B are conditions, then the logical operators can be used to generate new conditions A && B, A || B, and !B. The condition A && B is true only if both A and B are true. The condition A || B is true if either A or B are true. The operator ! changes the value of the condition which it precedes. Thus, the condition !A is true only if A is false, and the condition !B is true only if B is false. These definitions are summarized in Table 3.1.

Table 3.1 provides a truth table for the four conditions

```
A && B, A || B, !A, and !B.
```

Truth tables provide the truth values of a condition given the truth values of the boolean operands. In Table 3.1 there are two boolean operands, A and B, and there are 2^2 = 4 unique combinations of values these boolean operands can represent. Each additional boolean operand doubles the number of unique combinations. Consider the condition

```
A && B || B && C.
```

The truth value of this expression depends on the truth values of the three boolean operands A, B, and C, thus there are 2^3 = 8 unique combinations, as illustrated in Table 3.2.

The following program illustrates the use of logical and relational operators to generate the truth table provided in Table 3.2.

| A | B | C | A && B || B && C |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |