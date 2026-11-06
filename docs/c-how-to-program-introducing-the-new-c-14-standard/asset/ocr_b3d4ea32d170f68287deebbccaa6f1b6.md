# *UML Activity Diagram for an `if` Statement*

**Figure 4.4** illustrates the single-selection `if` statement. This figure contains the most important symbol in an activity diagram—the *diamond*, or **decision symbol**, which indicates that a *decision* is to be made. The workflow continues along a path determined by the symbol’s associated **guard conditions**, which can be *true* or *false*. Each transition arrow emerging from a decision symbol has a guard condition (specified in *square brackets* next to the arrow). If a guard condition is *true*, the workflow enters the action state to which the transition arrow points. In **Fig. 4.4**, if the grade is greater than or equal to 60 (i.e., the condition is *true*), the program prints “Passed,” then transitions to the activity’s final state. If the grade is less than 60 (i.e., the condition is *false*), the program immediately transitions to the final state without displaying a message.

![](bbox=[0.203, 0.601, 0.671, 0.74])

**Fig. 4.4** `if` single-selection statement UML activity diagram.

The `if` statement is a single-entry/single-exit control statement. We’ll see that the activity diagrams for the remaining control statements also contain initial states, transition arrows, action states that indicate