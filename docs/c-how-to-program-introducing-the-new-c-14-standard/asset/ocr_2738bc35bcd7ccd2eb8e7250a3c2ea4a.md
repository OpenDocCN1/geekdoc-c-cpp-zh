# Are Optional

All three expressions in a `for` header are optional. If the *loopContinuationCondition* is omitted, C++ assumes that the loop-continuation condition is *always true*, thus creating an *infinite loop*. You might omit the *initialization* expression if the program initializes the control variable *before* the loop. You might omit the *increment* expression if the program calculates the increment in the loop’s body or if no increment is needed. The increment expression in a `for` acts as if it were a standalone statement at the end of the `for`’s body. Therefore, the increment expressions

```
```cpp
counter = counter + 1
counter += 1
++counter
counter++
```
```

are equivalent in a `for` statement. Many programmers prefer `counter++` because it’s concise and because a `for` loop evaluates its increment expression *after* its body executes, so the postfix increment form seems more natural. In this case, the variable being incremented does not appear in a larger expression, so preincrementing and postincrementing have the *same effect*. We prefer preincrement.