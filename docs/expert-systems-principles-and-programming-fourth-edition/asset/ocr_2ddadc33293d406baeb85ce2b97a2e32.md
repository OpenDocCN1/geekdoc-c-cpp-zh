of rules would be given a pattern indicating in which phase it would be applicable. This technique has two drawbacks. First, as already mentioned, control knowledge is being embedded into the domain knowledge rules, which makes them more difficult to understand. Second, it is not always easy to determine when a phase is completed. This generally requires writing a rule that is applicable only when all the other rules have fired.

# Figure 9.2 Assignment of Salience for Different Phases

![](bbox=[0.13, 0.22, 0.93, 0.45])

The second approach is to use salience to organize the rules, as shown in Figure 9.2. This approach also has two major drawbacks. First, control knowledge is still being embedded into the rules using salience. Second, this approach does not guarantee the correct order of execution. Detection rules will always fire before isolation rules. However, when the isolation rules begin firing they might cause a detection rule to become activated and immediately fire because of its higher salience.

A third and better approach in controlling the flow of execution is to separate the control knowledge from the domain knowledge, as shown in Figure 9.3. Using this approach, each rule is given a control pattern that indicates its applicable phase. Control rules are then written to transfer control between the different phases, as shown here:

```
(defrule detection-to-isolation
    (declare (salience -10))
    ?phase <- (phase detection)
    =>
    (retract ?phase)
    (assert (phase isolation))))
```

```
(defrule isolation-to-recovery
    (declare (salience -10))
    ?phase <- (phase isolation)
    =>
```