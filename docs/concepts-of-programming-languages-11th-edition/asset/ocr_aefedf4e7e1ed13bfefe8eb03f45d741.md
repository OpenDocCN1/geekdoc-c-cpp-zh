Following is an example of nested loops in Java, in which there is a break out of the outer loop from the nested loop:

```
```java
outerLoop:
    for (row = 0; row < numRows; row++)
        for (col = 0; col < numCols; col++) {
            sum += mat[row][col];
            if (sum > 1000)
                break outerLoop;
        }
```
```

C, C++, and Python include an unlabeled control statement, `continue`, that transfers control to the control mechanism of the smallest enclosing loop. This is not an exit but rather a way to skip the rest of the loop statements on the current iteration without terminating the loop construct. For example, consider the following:

```
```text
while (sum < 1000) {
    getnext(value);
    if (value < 0) continue;
    sum += value;
}
```
```

A negative value causes the assignment statement to be skipped, and control is transferred instead to the conditional at the top of the loop. On the other hand, in

```
```text
while (sum < 1000) {
    getnext(value);
    if (value < 0) break;
    sum += value;
}
```
```

a negative value terminates the loop.

**Both last and break** provide for multiple exits from loops, which may seem to be somewhat of a hindrance to readability. However, unusual conditions that require loop termination are so common that such a statement is justified. Furthermore, readability is not seriously harmed, because the target of all such loop exits is the first statement after the loop (or an enclosing loop) rather than just anywhere in the program. Finally, the alternative of using multiple breaks to leave more than one level of loops is even more detrimental to readability.

The motivation for user-located loop exits is simple: They fulfill a common need for goto statements using a highly restricted branch statement. The target of a goto can be many places in the program, both above and below the goto itself. However, the targets of user-located loop exits must be below the exit and can only follow immediately at the end of a compound statement.