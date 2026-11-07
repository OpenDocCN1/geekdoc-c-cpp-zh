filling in the action states and decisions with action expressions and guard conditions in a manner appropriate to form a structured implementation for the algorithm. We’ll continue discussing the variety of ways in which actions and decisions may be written.

# 4.6 `if...else` Double-Selection Statement

The if...else single-selection statement performs an indicated action only when the condition is true; otherwise the action is skipped. The if...else double-selection statement allows you to specify an action to perform when the condition is true and a different action to perform when the condition is false. For example, the pseudocode statement

```
If student's grade is greater than or equal to 60
    Print "Passed"
Else
    Print "Failed"
```

prints “Passed” if the student’s grade is greater than or equal to 60, but prints “Failed” if the student’s grade is less than 60. In either case, after printing occurs, the next pseudocode statement in sequence is “performed.”

The preceding `If...Else` statement can be written in C++ as

```
if ( grade >= 60 )
    cout << "Passed";
else
    cout << "Failed";
```

The body of the else is also indented.

> **Good Programming Practice 4.1**
> 
> *If there are several levels of indentation, each level should be indented the same additional amount of space to promote readability and maintainability.*

Figure 4.5 illustrates the `if...else` statement’s flow of control.

![](bbox=[0.112, 0.715, 0.891, 0.921])

**Fig. 4.5** | `if...else` double-selection statement activity diagram.