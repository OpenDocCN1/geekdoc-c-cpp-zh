
What happens when the fire is extinguished and there are no longer any noxious fumes? As the next dialog shows, retracting the emergency fact or noxious-fumes-present fact doesn't affect the use-oxygen-masks fact:

```
CLIPS> (retract 1)
=== > f-1     (emergency (type fire))
=== > f-2     (noxious-fumes-present)
CLIPS> (facts)
f-0     (initial-fact)
f-3     (use-oxygen-masks)
For a total of 2 facts.
CLIPS>
```

CLIPS provides a truth maintenance mechanism for creating dependencies between facts; that mechanism is the logical CE. Modifying the noxious-fumes-present rule as shown below allows a dependency to be created between the facts that match the patterns in the LHS of a rule and the facts that are asserted from the RHS of the rule:

```
(defrule noxious-fumes-present
   (logical (emergency (type fire))
            (noxious-fumes-present))
   =>
   (assert (use-oxygen-masks)))
```

When the noxious-fumes-present rule is executed, a link is created between the facts matching patterns contained within the logical CE in the LHS of a rule and the facts asserted from the RHS of a rule. For this rule, if either the emergency fact or the noxious-fumes-present fact is retracted, then the use-oxygen-masks rule will also be retracted, as the following dialog shows:

```
CLIPS> (unwatch all)
CLIPS> (reset)
CLIPS> (watch facts)
CLIPS> (assert (emergency (type fire))
                 (noxious-fumes-present))
=== > f-1     (emergency (type fire))
=== > f-2     (noxious-fumes-present)
<Fact-2>
CLIPS> (run)
=== > f-3     (use-oxygen-masks)
CLIPS> (retract 1)
=== > f-1     (emergency (type fire))
=== > f-3     (use-oxygen-masks)
CLIPS>
```

The use-oxygen-masks fact receives logical support from the emergency fact and the noxious-fumes-present fact. The emergency fact and the noxious-fumes-present fact provide logical support to the use-oxygen-masks fact. The use-oxygen-masks fact is a dependent of the emergency fact and the noxious-fumes-present fact. The noxious-fumes-present fact and the emergency fact are dependencies of the use-oxygen-masks fact.

The logical CE does not have to be included along all the patterns on the LHS of the rule. If it is used, however, it must enclose the first CE in the LHS of a rule, and there can be no gaps between CEs enclosed by the logical CE. For example, logical CEs could not be placed around the second and fourth CEs of a rule or even around the first and third CEs of a rule, since this would leave gaps. This restriction on the logical CE is the result of its underlying implementation. It's also possible to make facts dependent on the nonexistence of facts by using the not CE within the logical CE. Even more complex conditions using the exists and forall CEs or other combinations of CEs can be used within the logical CE. Other than creating dependencies between groups of facts, the logical CE acts in all other respects like an and CE.

In order to modify the noxious-fumes-present rule to make the use-oxygen-masks fact dependent on only the noxious-fumes-present fact it would be necessary to reorder the patterns as shown:

```
(defrule noxious-fumes-present
    (logical (noxious-fumes-present))
    (emergency (type fire))
    =>
    (assert (use-oxygen-masks)))
```

With the rule modified as shown, the use-oxygen-masks fact won't be retracted automatically if the emergency fact is retracted (which is a safer approach since there may still be noxious fumes even if the fire is extinguished).

Normally, asserting a fact that's already in the fact list has no effect. However, a logically dependent fact that is derived from more than one source is not automatically retracted until the logical support from all of its sources is removed. For example, suppose another rule is added to indicate that oxygen masks should be used if gas extinguishers are in use:

```
(defrule gas-extinguishers-in-use
    (logical (gas-extinguishers-in-use))
    (emergency (type fire))
    =>
    (assert (use-oxygen-masks)))
```

Running the system now causes two separate rules to assert the same fact based on different reasons:

```
CLIPS> (unwatch all)
CLIPS> (reset)
CLIPS> (watch facts)
CLIPS> (watch rules)
CLIPS> (assert (emergency (type fire))
               (noxious-fumes-present)
               (gas-extinguishers-in-use))
==> f-1 (emergency (type fire))
==> f-2 (noxious-fumes-present)
==> f-3 (gas-extinguishers-in-use)
<Fact-3>
CLIPS> (run)
FIRE 1 gas-extinguishers-in-use: f-3,f-1
==> f-4 (use-oxygen-masks)
FIRE 2 noxious-fumes-present: f-1,f-2
CLIPS>
```

Retracting the noxious-fumes-present fact isn't sufficient to cause the automatic retraction of the use-oxygen-masks fact since there is other logical support for the oxygen masks to be used. The gas-extinguishers-in-use fact must also be retracted before the use-oxygen-masks fact will be retracted:

```
CLIPS> (retract 2)
<== f-2 (noxious-fumes-present)
CLIPS> (retract 3)
<== f-3 (gas-extinguishers-in-use)
<== f-4 (use-oxygen-masks)
CLIPS>
```

A fact that is asserted from the top-level prompt or from the RHS of a rule that does not have any logical CEs in its LHS is unconditionally supported. A fact that is unconditionally supported will never be automatically retracted by the retraction of another fact. Any previous logical support for a fact is discarded once it receives unconditional support.

CLIPS provides two commands for viewing the dependents and the dependencies associated with a fact. The syntax for these commands is:

```
(dependents <fact-index-or-address>)
(dependencies <fact-index-or-address>)
```

For the last example, before the noxious-fumes-present and gas-extinguishers-in-use facts were retracted, these commands would have produced the following output:

```
CLIPS> (facts)
f-0 (initial-fact)
f-1                   (emergency (type fire))
f-2                   (noxious-fumes-present)
f-3                   (gas-extinguishers-in-use)
f-4                   (use-oxygen-masks)
For a total of 5 facts.
CLIPS> (dependents 1)
None
CLIPS> (dependents 2)
f-4
CLIPS> (dependents 3)
f-4
CLIPS> (dependents 4)
None
CLIPS> (dependencies 1)
None
CLIPS> (dependencies 2)
None
CLIPS> (dependencies 3)
None
CLIPS> (dependencies 4)
f-2
f-3
CLIPS>
```

## 8.19 SUMMARY

This chapter introduced the concept of field constraints, which allow the negation and combination of more than one constraint for a given field. The not field constraint is used to prevent matching against certain values. The and field constraint is used to guarantee that all of a series of matching conditions are true. The or field constraint is used to guarantee that at least one of a series of matching conditions is true.

Functions are entered into the CLIPS top-level command loop or are used on the LHS or RHS of a rule. Many functions, such as some of the arithmetic functions, can have a variable number of arguments. Function calls can be nested within other function calls. The bind command allows variables to be bound on the RHS of a rule.

CLIPS provides several I/O functions. The open and close functions can be used to open and close files. Opened files are associated with a logical name. Logical names can be used in most functions that perform input and output to more than one type of physical device. Both printout and read functions use logical names. The printout function can output to the terminal and files. The read function can input from the keyboard and files. The format and readline functions also accept logical names. The format function allows more control over the appearance of output. The readline function can be used to read an entire line of data. The explode$ function converts a string to a multifield value.

Various concepts for controlling the flow of execution are available. The read function was used to demonstrate how a simple control loop for input could be created using control facts that are retracted and then asserted again. Test CEs along with predicate functions can be used on the LHS of a rule to provide more powerful pattern-matching capabilities. In addition, test CEs can be used to maintain a control loop. The predicate field constraint allows predicate tests to be placed directly within a pattern. The equality field constraint is used to compare a field to a value returned by a function. The Sticks program demonstrates several of these control techniques.

There are several other CEs besides the test CE. The or CE is used to express several rules as a single rule. The not CE allows pattern matching against the absence of a fact in the fact list. The and CE is used to group CEs together and, in conjunction with the or and not CEs, can be arbitrarily nested to express complex conditions needed to satisfy a rule. The exists CE is used to determine the existence of at least one group of facts that satisfies a CE or a combination of CEs. The forall CE is used to determine that a set of CEs is satisfied for every occurrence of another CE. The logical CE provides a truth maintenance mechanism. The existence of facts can be made dependent on the existence or nonexistence of other facts.

## PROBLEMS

8.1 Given the following deftemplates for facts describing a family tree.

```
(deftemplate father-of (slot father) (slot child))
(deftemplate mother-of (slot mother) (slot child))
(deftemplate male (slot person))
(deftemplate female (slot person))
(deftemplate wife-of (slot wife) (slot husband))
(deftemplate husband-of (slot husband) (slot wife))
```

write rules that will infer the following relations. Describe the deftemplates you use to solve the problem.

- (a) Uncle, aunt
- (b) Cousin
- (c) Grandparent
- (d) Grandfather, grandmother
- (e) Sister, brother
- (f) Ancestor

8.2 An industrial plant has ten sensors with ID numbers 1 through 10. Each sensor has either “good” or “bad” status. Build a deftemplate for representing the sensors and write one or more rules that will print a warning message if three or more sensors have bad status. Test your rules with sensors 3 and 5 bad; sensors 2, 8, and 9 bad; and sensors 1, 3, 5, and 10 bad. What must be done to prevent the warning message from being displayed multiple times?

8.3 Build a CLIPS program based on the IF-THEN rules developed for Problem 3.5 on page 158. The program should ask for the traveler’s payment method and travel interests and should output potential trips based on these two inputs.
