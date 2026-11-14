```
void display (void)
{
    if (dataAvail)
    {
        printf ("The result is %d\n", data);
        prompted = FALSE;
        dataAvail = FALSE;
    }
    return;
}

// keyboard ISR
void getDataISR(void)
{
    data = getchar();
    getchar();
    data = '0';
    dataAvail = TRUE;
    return;
}
```

# Figure 11.18 (Continued)

design. The knowledge of whether a specific task has enough information to execute is best kept with the task rather than with the scheduler. The negative aspect of such a decision is that the overhead of the function call will be incurred whether or not any real work gets done by the task.

In a tightly coupled design, tailored for a specific purpose, such knowledge could be moved to the scheduler. Under such circumstances, the overall flow of the system must be analyzed to confirm that the approach has a temporal advantage.

# 11.12 MEMORY MANAGEMENT REVISITED

The architecture of most contemporary embedded applications is built around multiple tasks/threads. If the design supports the ability to preempt or block a running task or thread and initiate another, there must be a switch to a new context. A context switch often involves:

+   - Saving the existing context.
+   - Switching to the new one.
+   - Restoring the old one.