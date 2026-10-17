| Term | Discussion |
|---|---|
| `for` | A `for` loop can be set up in a number of ways. It can use expressions, separated by semicolons, for initialization, setting the loop condition, and establishing the step expression. You have the option of leaving one or all of these out of the `for` statement. You must always use two semicolons as part of the test expression, even if you leave everything else out. The `for` statement precedes the block and allows the statement or statements in the block to continue to execute as long as its control conditions are true. If you set no conditions, then you create an infinite loop. |
| loop controls | If you set no conditions to control a loop, then you create an infinite loop. If your program enters an infinite loop, you have no option but to terminate its execution by using the operating system. |
| `next` | If you place a `next` operator anywhere inside a loop, it causes the flow of your program to skip the remaining statements in the loop. It does not skip out of the loop entirely, however. Instead, it causes the flow of activity to go back to the point of control. You can use a label with the `next` operator. To employ `next` with a label, you follow it with the name of a label (usually in capital letters). The label itself can be placed at a point of control. You follow a label with a colon (`LABEL:`). |
| `last` | This operator allows you to entirely exit a loop. It can also allow you to access a label in the same fashion employed with the `next` operator. |
| `redo` | The `redo` operator causes the flow of the program to jump back to the beginning of a loop without evaluating the control expression of the loop. The result is that the statements in the loop execute even if the control expression if normally evaluated would cause the loop to terminate. |
| `continue` | The `continue` operator is another version of a break. It causes the flow of the program to immediately exit a loop. The flow of the program continues from after the closing brace of the loop. Subsequent statements in the loop are ignored. |

You can find programming examples and extended explanations of items in subsequent sections of this chapter.

# Repetition and the `for` Statement

The `for` statement provides the quintessential vehicle for elementary repetition in a program. It proves convenient to use because it provides you with the chance to introduce three arguments into your repetition activities. Refer to Figure 11.2 as you review the items in the following list:

+   - **The control value.** The control value is a scalar identifier that establishes a starting value. The starting value is often set at zero (0).
+   - **The limit.** A second expression uses a relational operator to compare the value of the control identifier with another value, one that you often provide as a constant value.
+   - **The incremental expression.** The incremental expression usually consists of the control value suffixed or prefixed by an incremental operator.