# for Statement UML Activity Diagram

The for repetition statement’s UML activity diagram is similar to that of the while statement (Fig. 4.6). Figure 5.4 shows the activity diagram of the for statement in Fig. 5.2. The diagram makes it clear that initialization occurs once before the loop-continuation test is evaluated the first time, and that incrementing occurs each time through the loop after the body statement executes. Note that (besides an initial state, transition arrows, a merge, a final state and several notes) the diagram contains only action states and a decision.

![](bbox=[0.143, 0.247, 0.857, 0.603])

**Fig. 5.4** | UML activity diagram for the for statement in Fig. 5.2.

# 5.4 Examples Using the for Statement

The following examples show methods of varying the control variable in a for statement. In each case, we write the appropriate for statement header. Note the change in the relational operator for loops that decrement the control variable.

+   a) Vary the control variable from 1 to 100 in increments of 1.
+   
+   b) Vary the control variable from 100 down to 1 in decrements of 1.
+   
+   c) Vary the control variable from 7 to 77 in steps of 7.
+   
+   d) Vary the control variable from 20 down to 2 in steps of −2.

```
for ( int i = 1; i <= 100; ++i )
```

```
for ( int i = 100; i >= 1; --i )
```

```
for ( int i = 7; i <= 77; i += 7 )
```

```
for ( int i = 20; i >= 2; i -= 2 )
```