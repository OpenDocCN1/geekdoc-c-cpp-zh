# 15.9 goto: Unconditional Branching

We've stressed the importance of using structured-programming techniques to build reliable software that's easy to debug, maintain and modify. In some cases, performance is more important than strict adherence to structured-programming techniques. In these cases, some unstructured-programming techniques may be used. For example, we can use break to terminate an iteration statement's execution before the loop-continuation condition becomes false. This saves unnecessary iterations of the loop if the task is completed before loop termination.

Another instance of unstructured programming is the goto statement—an unconditional branch. The goto statement alters the flow of control, continuing execution with the first statement after the label specified in the statement. A label is an identifier followed by a colon (:). A label must appear in the same function as the goto statement that refers to it. Labels need not be unique among functions.

# Demonstrating goto

Figure 15.5 uses goto statements to loop ten times and print a counter value each time. Line 6 initializes count to 1. The label start: is skipped, because labels do not perform any action. Line 9 tests whether count is greater than 10. If so, line 10 transfers control from the goto to the first statement after the label end: (line 19). Otherwise, lines 13–14 print and increment count, and control transfers from the goto (line 16) to the first statement after the label start: (line 9).

```
// fig15_05.c
// Using the goto statement
#include <stdio.h>

int main(void) {
    int count = 1; // initialize count

start: // label
    if (count > 10) {
        goto end;
    }

    printf("%d ", count);
    ++count;

    goto start; // goto start on line 9

end: // label
    putchar('\n');
}
```

![](bbox=[0.12, 0.88, 0.88, 0.93])

Fig. 15.5 | Using the goto statement.