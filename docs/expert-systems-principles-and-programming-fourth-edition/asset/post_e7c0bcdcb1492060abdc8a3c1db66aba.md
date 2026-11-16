
of rules would be given a pattern indicating in which phase it would be applicable. This technique has two drawbacks. First, as already mentioned, control knowledge is being embedded into the domain knowledge rules, which makes them more difficult to understand. Second, it is not always easy to determine when a phase is completed. This generally requires writing a rule that is applicable only when all the other rules have fired.

### Figure 9.2 Assignment of Salience for Different Phases

![](img/2c460d4de56b7ffaad3834eee20beaa0_525_0.png)

The second approach is to use salience to organize the rules, as shown in Figure 9.2. This approach also has two major drawbacks. First, control knowledge is still being embedded into the rules using salience. Second, this approach does not guarantee the correct order of execution. Detection rules will always fire before isolation rules. However, when the isolation rules begin firing they might cause a detection rule to become activated and immediately fire because of its higher salience.

A third and better approach in controlling the flow of execution is to separate the control knowledge from the domain knowledge, as shown in Figure 9.3. Using this approach, each rule is given a control pattern that indicates its applicable phase. Control rules are then written to transfer control between the different phases, as shown here:

```
(defrule detection-to-isolation
    (declare (salience -10))
    ?phase <- (phase detection)
    =>
    (retract ?phase)
    (assert (phase isolation)))
```

```
(defrule isolation-to-recovery
    (declare (salience -10))
    ?phase <- (phase isolation)
    =>
    (retract ?phase)
    (assert (phase recovery)))
```

```
(defrule recovery-to-detection
    (declare (salience -10))
    ?phase <- (phase recovery)
    =>
    (retract ?phase)
    (assert (phase detection)))
```

### Figure 9.3 Separation of Expert Knowledge from Control Knowledge

![](img/2c460d4de56b7ffaad3834eee20beaa0_526_0.png)

Each of the rules applicable for a particular phase is then given a control pattern that confirms that the appropriate control fact is present. For example, a recovery rule might look like this:

```
(defrule find-fault-location-and-recovery
(phase recovery)
(recovery-solution switch-device
?replacement on)
=>
(printout t "Switch device ?replacement "on" crlf))
```

A salience hierarchy is a description of the salience values used by an expert system. Each level in a salience hierarchy corresponds to a specific set of rules whose members are all given the same salience. If the rules for detection, isolation, and recovery are given a default salience of zero, then the salience hierarchy is as shown in Figure 9.4. Notice that while the fact (phase detection) is in the fact list, the detection-to-isolation rule will be on the agenda. Since it has

### Figure 9.4 Salience Hierarchy Using Expert and Control Rules

![](img/2c460d4de56b7ffaad3834eee20beaa0_527_0.png)

a lower salience than the detection rules, it will not fire until all of the detection rules have had an opportunity to fire. The following output shows a sample run of the three previous control rules:

```
CLIPS> (reset)
CLIPS> (assert (phase detection))
<Fact-1>
CLIPS> (watch rules)
CLIPS> (run 10)
FIRE 1 detection-to-isolation: f-1
FIRE 2 isolation-to-recovery: f-2
FIRE 3 recovery-to-detection: f-3
FIRE 4 detection-to-isolation: f-4
FIRE 5 isolation-to-recovery: f-5
FIRE 6 recovery-to-detection: f-6
FIRE 7 detection-to-isolation: f-7
FIRE 8 isolation-to-recovery: f-8
FIRE 9 recovery-to-detection: f-9
FIRE 10 detection-to-isolation: f-10
CLIPS>
```

Notice that the control rules just keep firing in sequence because there are no domain knowledge rules to be applied during any of the phases. If there were, then the domain knowledge rules would be applied for activated rules during the appropriate phases.

The previous control rules could be more generically written with a deffacts construct and a single rule as:

```
(deffacts control-information
    (phase detection)
    (phase-after detection isolation)
    (phase-after isolation recovery)
    (phase-after recovery detection))
```

```
(defrule change-phase
  (declare (salience -10))
  ?phase <- (phase ?current-phase)
  (phase-after ?current-phase ?next-phase)
  =>
  (retract ?phase)
  (assert (phase ?next-phase)))
```

or they could be written using a sequence of phases to be cycled through as:

```
(deffacts control-information
  (phase detection)
  (phase-sequence isolation recovery detection))
```

```
(defrule change-phase
  (declare (salience -10))
  ?phase <- (phase ?current-phase)
  ?list <- (phase-sequence ?next-phase
      $?other-phases)
  =>
  (retract ?phase ?list)
  (assert (phase ?next-phase))
  (assert (phase-sequence ?other-phases
      ?next-phase)))
```

Additional levels can easily be added to the salience hierarchy. Figure 9.5 shows a hierarchy with two additional levels. The constraint rules represent rules that detect illegal or unproductive states that may occur in the expert system. For example, an expert system scheduling people to various tasks may

### Figure 9.5 Four-Level Salience Hierarchy

![](img/2c460d4de56b7ffaad3834eee20beaa0_528_0.png)

produce a schedule that violates a constraint. Instead of allowing the lower salience rules to continue working on the schedule, the constraint rules will immediately remove violations in the schedule. As another example, the user may enter in response to a series of questions a series of legal values that result in an illegal value being generated. The constraint rules could be used to detect such violations.

The query rules shown in Figure 9.5 represent rules that ask the user particular questions to aid the expert system in determining an answer. These rules have lower salience than the expert rules because it is undesirable to ask the user a question that can be determined by the expert rules. Thus the query rules are fired only when no more information can be derived by the expert rules.

## 9.5 MISUSE OF SALIENCE

Although salience is a powerful tool for controlling execution, it can easily be misused. In particular, people who are just learning rule-based programming tend to overuse salience because it gives them explicit control of execution. It is more like the procedural programming they are used to, in which statements execute sequentially.

Overuse of salience results in a poorly coded program. The main advantage of a rule-based program is that the programmer does not have to worry about controlling execution. A well-designed rule-based program has a natural mode of execution that permits the inference engine to guide rule firings in an optimal manner.

Salience should primarily be used as a mechanism for determining the order in which rules fire. This means that in general a rule that is placed on the agenda is eventually fired. Salience should not be used as a method for selecting a single rule from a group of rules when patterns can be used to express the criteria for selection, nor should salience be used as a “quick fix” to get rules to fire in the proper order.

In general, any salience value used in a rule should correspond to a level in the salience hierarchy of the expert system. The range of salience values from –10,000 to 10,000 is somewhat misleading. Rarely should more than seven salience values ever be required for coding an expert system; most well-coded expert systems need no more than three or four salience values. For large expert systems, it is strongly recommended that programmers use modules to control the flow of execution (as discussed in the next section) and that no more than two or three salience values be used.

As an example of how the use of salience can be avoided, the following is a simple set of rules that suggest which squares to mark in a tic-tac-toe game. The rules are listed in the order in which they should be applied.

- IF a winning square is open, THEN take it.
- IF a blocking square is open, THEN take it.
- IF a square is open, THEN take it.
