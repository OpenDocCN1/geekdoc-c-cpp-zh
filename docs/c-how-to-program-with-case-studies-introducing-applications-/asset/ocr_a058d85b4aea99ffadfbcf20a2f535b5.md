```
```c
if (gender == 1 && age >= 65) {
    ++seniorFemales;
}
```
```

This if statement contains two simple conditions. The condition gender == 1 might, for example, determine whether a person is a female. The condition age >= 65 determines whether a person is a senior citizen. The two simple conditions are evaluated first because == and >= each have higher precedence than &&. The if statement then considers the combined condition gender == 1 && age >= 65, which is *true* if and only if both of the simple conditions are *true*. Finally, if this combined condition is *true*, then the preceding if statement increments seniorFemales by 1. If either or both simple conditions are *false*, the program skips the if's body and proceeds to the next statement in sequence.

The following table summarizes the && operator:

| expression1 | expression2 | expression1 && expression2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | nonzero | 0 |
| nonzero | 0 | 0 |
| nonzero | nonzero | 1 |

The table shows all four possible combinations of zero (*false*) and nonzero (*true*) values for *expression1* and *expression2*. Such tables are often called truth tables. C evaluates all expressions that include relational operators, equality operators, and/or logical operators to 0 or 1. Although C sets a *true* value to 1, it accepts any nonzero value as *true*.

# ### Logical OR (||) Operator

Now let's consider the || (logical OR) operator. Suppose we wish to ensure at some point in a program that either or both of two conditions are *true* before we choose a certain path of execution. In this case, we use the || operator, as in the following program segment:

```
```c
if (semesterAverage >= 90 || finalExam >= 90) {
    puts("Student grade is A");
}
```
```

This statement contains two simple conditions. The condition semesterAverage >= 90 determines whether the student deserves an "A" because of a solid performance throughout the semester. The condition finalExam >= 90 determines whether the student deserves an "A" because of an outstanding performance on the final exam. The if statement then considers the combined condition and awards the student an "A" if either or both of the simple conditions are *true*. The message "Student grade is A" prints unless both simple conditions are *false* (zero). The following is a truth table for the logical OR operator (||):