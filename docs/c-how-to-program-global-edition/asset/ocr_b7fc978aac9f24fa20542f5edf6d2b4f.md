# Short-Circuit Evaluation

The && operator has a higher precedence than ||. Both operators associate from left to right. An expression containing && or || operators is evaluated only until truth or falsehood is known. Thus, evaluation of the condition

```
gender == 1 && age >= 65
```

will stop if gender is not equal to 1 (i.e., the entire expression is guaranteed to be false), and continue if gender is equal to 1 (i.e., the entire expression could still be true if age >= 65). This performance feature for the evaluation of logical AND and logical OR expressions is called short-circuit evaluation.

# Performance Tip 4.2

In expressions using operator &&, make the condition that's most likely to be false the leftmost condition. In expressions using operator ||, make the condition that's most likely to be true the leftmost condition. This can reduce a program's execution time.

# Logical Negation (!) Operator

C provides the ! (logical negation) operator to enable you to "reverse" the meaning of a condition. Unlike operators && and ||, which combine two conditions (and are therefore binary operators), the logical negation operator has only a single condition as an operand (and is therefore a unary operator). The logical negation operator is placed before a condition when we're interested in choosing a path of execution if the original condition (without the logical negation operator) is false, such as in the following program segment:

```
if (! (grade == sentinelValue)) {
    printf("The next grade is %f\n", grade);
}
```

The parentheses around the condition grade == sentinelValue are needed because the logical negation operator has a higher precedence than the equality operator. Figure 4.15 is a truth table for the logical negation operator.

| expression | !expression |
|---|---|
| 0 | 1 |
| nonzero | 0 |

Fig. 4.15 | Truth table for operator ! (logical negation).

In most cases, you can avoid using logical negation by expressing the condition differently with an appropriate relational operator. For example, the preceding statement may also be written as:

```
if (grade != sentinelValue) {
    printf("The next grade is %f\n", grade);
}
```