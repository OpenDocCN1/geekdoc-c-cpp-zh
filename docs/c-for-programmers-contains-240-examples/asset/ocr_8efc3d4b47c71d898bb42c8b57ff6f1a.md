```
1 2 3 4 5 6 7 8 9 10
```

Fig. 5.7 | do...while repetition statement. (Part 2 of 2.)

# do...while Statement UML Activity Diagram

Figure 5.8 contains the UML activity diagram for the do...while statement. This diagram makes it clear that the loop-continuation condition is not evaluated until after the loop performs the loop-body action states at least once. Compare this activity diagram with that of the while statement (Fig. 4.5). Again, note that (besides an initial state, transition arrows, a merge, a final state and several notes) the diagram contains only action states and a decision. Imagine, again, that you have access to a bin of empty do...while statement UML activity diagrams—as many as you might need to stack and nest with the activity diagrams of other control statements to form a structured implementation of an algorithm. You fill in the action states and decision symbols with action expressions and guard conditions appropriate to the algorithm.

![](bbox=[0.15, 0.45, 0.83, 0.78])

Fig. 5.8 | UML activity diagram for the do...while repetition statement of Fig. 5.7.

# 5.6 switch Multiple-Selection Statement

We discussed the if single-selection statement and the if...else double-selection statement in Chapter 4. C++ provides the switch multiple-selection statement to perform many different actions based on the possible values of a variable or expression. Each action is associated with the value of a constant integral expression (i.e., any combination of