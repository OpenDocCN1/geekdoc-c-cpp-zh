# 152 Chapter 4 Decision Structures and Boolean Logic

For example, the following pseudocode performs the same operation as the flowchart shown in Figure 4-18.

```
Select month
Case 1:
  Display "January"
Case 2:
  Display "February"
Case 3:
  Display "March"
Default:
  Display "Error: Invalid month"
End Select
```

In this example, the testExpression is the month variable. If in the month variable is 1, the program will branch to the Case 1: section and execute the Display "January" statement that immediately follows it. If in the month variable is 2, the program will branch to the Case 2: section and execute the Display "February" statement that immediately follows it. If in the month variable is 3, the program will branch to the Case 3: section and execute the Display "March" statement that immediately follows it. If in the month variable is not 1, 2, or 3, the program will branch to the Case 1: section and execute the Display "Error: Invalid month" statement that immediately follows it.

> NOTE: In many languages the case structure is called a switch statement.

Case structures are never required because the same logic can be achieved with nested decision structures. For example, Figure 4-19 shows nested decision structures that are equivalent to the case structure in Figure 4-18. In situations where they can be used, however, case structures are straightforward.

# Figure 4-19 Nested decision structures

![](bbox=[0.19, 0.635, 0.81, 0.888])