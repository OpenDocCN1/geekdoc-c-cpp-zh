errors. If a program must modify the control variable’s value in the loop’s body, use `while` rather than `for`.

# UML Activity Diagram for the `for` Statement

The `for` statement’s UML activity diagram is similar to that of the `while` statement (Fig. 4.8). Figure 5.4 shows the activity diagram of the `for` statement in Fig. 5.2. The diagram makes it clear that initialization occurs only once—*before* the loop-continuation test is evaluated the first time—and that incrementing occurs *each time* through the loop *after* the body statement executes.

![](bbox=[0.119, 0.501, 0.884, 0.774])

Fig. 5.4 UML activity diagram for the `for` statement in Fig. 5.2.