# 8.12 The “continue” Statement

The continue statement has a similar role as break. However, the current loop is not aborted; only the rest of the current loop iteration is skipped, and the loop continues with the next iteration. In the for and while loops, the loop header is executed next. That means, and in for, that the update and condition are executed, and in while (and do-while), that the condition is checked. If the condition still holds, the loop body instructions are executed again.

You saw an example in Listing 8.18. When the program execution hits continue, it immediately jumps back to for and fetches the next char c from input.

In a switch, a continue has no meaning like break. It thus affects an enclosing loop.