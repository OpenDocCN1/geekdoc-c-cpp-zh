break to terminate execution of an iteration statement before the loop-continuation condition becomes false. This saves unnecessary iterations of the loop if the task is completed before loop termination.

Another instance of unstructured programming is the goto statement—an unconditional branch. The result of the goto statement is a change in the flow of control to the first statement after the label specified in the goto statement. A label is an identifier followed by a colon. A label must appear in the same function as the goto statement that refers to it. Labels need not be unique among functions. Figure 14.7 uses goto statements to loop ten times and print the counter value each time. After initializing count to 1, line 11 tests count to determine whether it's greater than 10 (the label start: is skipped because labels do not perform any action). If so, control is transferred from the goto to the first statement after the label end: (which appears at line 20). Otherwise, lines 15–16 print and increment count, and control transfers from the goto (line 18) to the first statement after the label start: (which appears at line 9).

```
// Fig. 14.7: fig14_07.c
// Using the goto statement
#include <stdio.h>

int main(void)
{
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

![](bbox=[0.12, 0.76, 0.9, 0.81])

# Fig. 14.7 | Using the goto statement.

In Chapter 3, we stated that only three control structures are required to write any program—sequence, selection and iteration. When the rules of structured programming are followed, it's possible to create deeply nested control structures within a function from which it's difficult to escape efficiently. Some programmers use goto statements in such situations as a quick exit from a deeply nested structure. This eliminates the need to test multiple conditions to escape from a control structure. There are some additional situations where goto is actually recommended—see, for example, CERT recommendation