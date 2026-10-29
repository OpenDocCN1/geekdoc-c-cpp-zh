# Display 2.1 Comparison Operators

| MATH SYMBOL | ENGLISH | C++ NOTATION | C++ SAMPLE | MATH EQUIVALENT |
|---|---|---|---|---|
| = | Equal to | == | x + 7 == 2*y | x + 7 = 2y |
| ≠ | Not equal to | != | ans != 'n' | ans ≠ 'n' |
| < | Less than | < | count < m + 3 | count < m + 3 |
| ≤ | Less than or equal to | <= | time <= limit | time ≤ limit |
| > | Greater than | > | time > limit | time > limit |
| ≥ | Greater than or equal to | >= | age >= 21 | age ≥ 21 |

# The “or” Operator, ||

You can form a more elaborate Boolean expression by combining two simpler Boolean expressions using the “or” operator, ||.

# SYNTAX FOR A BOOLEAN EXPRESSION USING ||

```
(Boolean_Exp_1) || (Boolean_Exp_2)
```

# EXAMPLE WITHIN AN if-else STATEMENT

```
if ( (x == 1) || (x == y) )
    cout << "x is 1 or x equals y.\n";
else
    cout << "x is neither 1 nor equal to y.\n";
```

If the value of x is equal to 1 or the value of y (or both), then the first cout statement will be executed; otherwise, the second cout statement will be executed. (if-else statements are covered a bit later in this chapter, but the meaning of this simple example should be intuitively clear.)

# Evaluating Boolean Expressions

As you will see in the next two sections of this chapter, Boolean expressions are used to control branching and looping statements. However, a Boolean expression has an independent identity apart from any branching or looping statement you might use it