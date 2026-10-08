# 6.11 Logical Operators 257

to determine whether the student deserves an A in the course of an outstanding performance on the final exam. If the statement then considers the combined condition

(semesterAverage >= 90) || (finalExam >= 90) and awards the student A if either or both of the simple conditions are true. Only the message "Student grade is A" is not displayed when both of the simple conditions are false. Figure 6.16 is truth table for conditional OR (||). Operator && has a higher precedence than operator ||. Both operators associate from left to right.

expression1 | expression2 | expression1 || expression2 |
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

Fig. 6.16 | || (conditional OR) operator table.

# 6.11.3 Short-Circuit Evaluation of Complex Conditions

The parts of an expression containing && || operators are evaluated only until it's known the condition is true or false. Thus, the expression

```
gender == 'F' && (age >= 65)
st immediately if gender is not equal to 'F' (i.e., the entire expression is false) and continues only if gender is equal to 'F' (i.e., the entire expression could be true if the condition is age >= 65). This feature of conditional AND and OR expressions is called short-circuit evaluation.
```

![](bbox=[0.143, 0.616, 0.213, 0.658])

> Common Programming Error 6.6
In expressions using operator &&, a condition—known as the dependent condition—may require another condition to be true for the dependent condition to be meaningful. the dependent condition should be placed after the other one, or an error might occur. For example, in the expression (i = 0) && (10 / i == 2), the second condition must appear after the first condition, or a divide-by-zero error might occur.

# 6.11.4 Boolean Logical AND (&) and Boolean Logical OR (| Operators

The boolean logical AND (&) and boolean logical inclusive OR (|) operators work identically to the (conditional AND) and || (conditional OR) operators, with exception—the logical operators always evaluate both of their operands (i.e., they do not perform short-circuit evaluation). Therefore, the expression

```
gender == 'F' & (age >= 65)
euates age >= 65 regardless of whether gender is equal to 'F'. This is useful if the right operand of the & | operator has a required side effect—such as a modification of a variable's value. For example, the expression
```