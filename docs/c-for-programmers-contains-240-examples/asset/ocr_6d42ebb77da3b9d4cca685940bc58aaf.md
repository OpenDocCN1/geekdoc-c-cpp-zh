```
( semesterAverage >= 90 ) || ( finalExam >= 90 )
```

and awards the student an “A” if either or both of the simple conditions are true. Note that the message “Student grade is A” prints unless both of the simple conditions are false. Figure 5.16 is a truth table for the logical OR operator (||).

The && operator has a higher precedence than the || operator. Both operators associate from left to right. An expression containing && or || operators evaluates only until the truth or falsehood of the expression is known. Thus, evaluation of the expression

```
( gender == 1 ) && ( age >= 65 )
```

stops immediately if gender is not equal to 1 (i.e., the entire expression is false) and continues if gender is equal to 1 (i.e., the entire expression could still be true if the condition age >= 65 is true). This performance feature for the evaluation of logical AND and logical OR expressions is called short-circuit evaluation.

# Performance Tip 5.6

In expressions using operator &&, if the separate conditions are independent of one another, make the condition most likely to be false the leftmost condition. In expressions using operator ||, make the condition most likely to be true the leftmost condition. This use of short-circuit evaluation can reduce a program’s execution time.

| expression1 | expression2 | expression1 || expression2 |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

Fig. 5.16 | || (logical OR) operator truth table.

# Logical Negation (!) Operator

C++ provides the ! (logical NOT, also called logical negation) operator to enable a programmer to “reverse” the meaning of a condition. Unlike the && and || binary operators, which combine two conditions, the unary logical negation operator has only a single condition as an operand. The unary logical negation operator is placed before a condition when we are interested in choosing a path of execution if the original condition (without the logical negation operator) is false, such as in the following program segment:

```
if ( ! ( grade == sentinelValue ) )
    cout << "The next grade is " << grade << endl;
```

The parentheses around the condition grade == sentinelValue are needed because the logical negation operator has a higher precedence than the equality operator.

In most cases, you can avoid using logical negation by expressing the condition with an appropriate relational or equality operator. For example, the preceding if statement also can be written as follows: