# Single Statement in Each Branch—an if-else Structure

![](bbox=[0.185, 0.145, 0.685, 0.345])

The pseudocode is as follows:

```
if(condition)
  stmt1;
else
  stmt2;
```

The execution sequence of this code is as follows:

+   - If the condition is true, statement stmt1 is executed and statement stmt2 in the else clause is skipped.
- If the condition is false, statement stmt2 is executed and statement stmt1 in the true branch is skipped.

A case structure is a selection structure with more than two branches written as nested selection structures as if...else if...else if...else if...else.
The code for the control structure shown in Figure 4.5 has the form:

```
if(cond1)
  stmt1;
else if(cond2)
  stmt2;
else if(cond3)
  stmt3;
else
  stmt4;
```