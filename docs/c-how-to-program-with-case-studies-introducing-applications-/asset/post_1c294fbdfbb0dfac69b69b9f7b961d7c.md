
- c) When a do...while terminates, execution continues with the statement after the while clause.
- d) All of the above statements are true.

Answer: a) is false. Actually, if the while statement's loop-continuation test fails upon entering the loop, the loop's body will not execute.

2 (True/False) Assuming counter is initialized to 1, the following loop displays the numbers 1 through 10:

```
do {
    printf("%d ", counter);
} while (++counter < 10);
```

Answer: False. This loop displays the numbers 1 through 9. To display the numbers 1 through 10, change the < in the loop-continuation condition to <=.

## 4.8 break and continue Statements

The break and continue statements are used to alter the flow of control. Section 4.6 showed that a break encountered in a switch statement terminates the switch's execution. This section discusses how to use break in an iteration statement.

### break Statement

The break statement, when executed in a while, for, do...while or switch statement, causes an immediate exit from that statement. Program execution continues with the next statement after that while, for, do...while or switch. Common uses of break are to escape early from a loop or skip the remainder of a switch (as in Fig. 4.5). Figure 4.7 demonstrates the break statement (line 12) in a for iteration statement.

```
1  // fig04_07.c
2  // Using the break statement in a for statement.
3  #include <stdio.h>
4
5  int main(void) {
6      int x = 1;  // declared here so it can be used after loop
7
8      // loop 10 times
9      for (; x <= 10; ++x) {
10         // if x is 5, terminate loop
11         if (x == 5) {
12             break; // break loop only if x is 5
13         }
14
15         printf("%d ", x);
16     }
17
18     printf("\nBroke out of loop at x == %d\n", x);
19 }
```

Fig. 4.7 | Using the break statement in a for statement. (Part 1 of 2.)

```
1 2 3 4
Broke out of loop at x == 5
```

**Fig. 4.7** | Using the `break` statement in a `for` statement. (Part 2 of 2.)

When the `if` statement detects that x has become 5, `break` executes. This terminates the `for` statement, and the program continues with the `printf` after the `for`. The loop fully executes only four times. Recall that when you declare the control variable in a `for` loop’s *initialization expression*, the variable no longer exists after the loop terminates. We declared and initialized x before the loop in this example, so that we could use its final value after the loop terminates. So, the initialization section of the `for`’s header (before the first semicolon) is empty.

### continue Statement

The `continue` statement, when executed in a `while`, `for` or `do...while` statement, skips the remaining statements in that control statement’s body and performs the next iteration of the loop. In `while` and `do...while` statements, the loop-continuation test is evaluated immediately after the `continue` statement executes. In the `for` statement, the increment expression executes, then the loop-continuation test is evaluated. Figure 4.8 uses `continue` (line 10) in the `for` statement to skip the `printf` statement when x is 5 and begin the next iteration of the loop.

```
1  // fig04_08.c
2  // Using the continue statement in a for statement.
3  #include <stdio.h>
4
5  int main(void) {
6     // loop 10 times
7     for (int x = 1; x <= 10; ++x) {
8        // if x is 5, continue with next iteration of loop
9        if (x == 5) {
10          continue; // skip remaining code in loop body
11       }
12
13       printf("%d ", x);
14    }
15
16    puts("\nUsed continue to skip printing the value 5");
17 }
```

```
1 2 3 4 6 7 8 9 10
Used continue to skip printing the value 5
```

**Fig. 4.8** | Using the `continue` statement in a `for` statement.

### break and continue Notes

Some programmers feel `break` and `continue` violate the norms of structured programming, so they do not use them. The effects of these statements can be achieved by structured programming techniques we’ll soon discuss, but the break and continue statements perform faster.

There’s a tension between achieving quality software engineering and achieving the best-performing software—one is achieved at the expense of the other. For all but the most performance-intensive situations, apply the following guidelines: First, make your code simple and correct, then make it fast and small, but only if necessary.

### Self Check

- 1. *(Multiple Choice)* Which of the following statements a), b) or c) is **false**?
  a) The break statement terminates a switch statement’s execution.
  b) The break statement, when executed in a while, for or do…while statement, causes an immediate exit from that statement.
  c) Common uses of break are to escape early from a loop or to skip the remainder of an if…else.
  d) All of the above statements are *true*.

  **Answer:** c) is *false*. Actually, break skips the remainder of a switch, not an if…else.

- 2. *(Multiple Choice)* Which of the following statements a), b) or c) is **false**?
  a) The continue statement, when executed in a while, for or do…while statement, skips the remaining statements in that control statement’s body and performs the next iteration of the loop.
  b) In while and do…while statements, the loop-continuation test is evaluated immediately after the continue statement executes.
  c) In the for statement, after the continue statement executes, the loop-continuation test is evaluated, then the increment expression executes.
  d) All of the above statements are *true*.

  **Answer:** c) is *false*. Actually, in the for statement, after the continue statement executes, the increment expression executes, then the loop-continuation test is evaluated.

## 4.9 Logical Operators

So far we’ve used simple conditions, such as counter <= 10, total > 1000, and grade != −1. We’ve expressed these conditions in terms of the relational operators (>, <, >= and <=) and equality operators (== and !=). Each decision tested precisely one condition. To test multiple conditions in the process of making a decision, we had to perform these tests in separate statements or in nested if or if…else statements. C provides logical operators that may be used to form more complex conditions by combining simple conditions. The logical operators are && (logical AND), || (logical OR) and ! (logical NOT, which is also called logical negation). We’ll consider examples of each of these operators.

### Logical AND (&&) Operator

Suppose we wish to ensure that two conditions are both true before we choose a certain path of execution. In this case, we can use the logical operator && as follows:

```c
if (gender == 1 && age >= 65) {
    ++seniorFemales;
}
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

### Logical OR (||) Operator

Now let's consider the || (logical OR) operator. Suppose we wish to ensure at some point in a program that either or both of two conditions are *true* before we choose a certain path of execution. In this case, we use the || operator, as in the following program segment:

```c
if (semesterAverage >= 90 || finalExam >= 90) {
    puts("Student grade is A");
}
```

This statement contains two simple conditions. The condition semesterAverage >= 90 determines whether the student deserves an "A" because of a solid performance throughout the semester. The condition finalExam >= 90 determines whether the student deserves an "A" because of an outstanding performance on the final exam. The if statement then considers the combined condition and awards the student an "A" if either or both of the simple conditions are *true*. The message "Student grade is A" prints unless both simple conditions are *false* (zero). The following is a truth table for the logical OR operator (||):
