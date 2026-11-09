For...Next statement to display (in message boxes) integers from 10 (the *startValue*) through 13 (the *endValue*) in increments of 1 (the *stepValue*).

# FOR...NEXT STATEMENT

Syntax

```
```
For counter [As dataType] = startValue To endValue [Step stepValue]
    [statements]
Next counter
```
```

Processing tasks

+   1. If the counter variable is declared in the For clause, the computer creates and initializes the variable to the *startValue*; otherwise, it just performs the initialization task. This is done only once, at the beginning of the loop.
+   2. The computer evaluates the loop condition by comparing the value in the counter variable with the *endValue*. If the *stepValue* is positive, the comparison determines whether the counter variable’s value is greater than the *endValue*. If the *stepValue* is negative, on the other hand, the comparison determines whether the counter variable’s value is less than the *endValue*.
+   3. If the loop condition evaluates to True, the computer stops processing the loop; processing continues with the statement following the Next clause. If the loop condition evaluates to False, on the other hand, the computer processes the instructions within the loop and then task 4 is performed. Notice that the computer evaluates the loop condition *before* processing the instructions within the loop.
+   4. Task 4 is performed only when the loop condition evaluates to False. In this task, the computer adds the *stepValue* to the contents of the counter variable. It then repeats tasks 2, 3, and 4 until the loop condition evaluates to True.

Example

```
```
For intPrice As Integer = 10 To 13 Step 1
    MessageBox.Show(intPrice.ToString)
Next intPrice
```
```

this portion can be omitted when the *stepValue* is 1

Figure 15-1: Syntax and an example of the For...Next statement