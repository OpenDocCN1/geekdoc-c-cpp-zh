

==> f-1    (person (name "John Hill"))
               (address "25 Mulberry Lane"))
==> f-3    (person (name "John Hill"))
               (address "37 Cherry Lane"))
CLIPS>

Two deftemplates are used in this example. The `person` deftemplate is used to store information about a person, in this case just the name of the person and the person's address. Other information, such as age or eye color, could also be stored. The `moved` deftemplate is used to indicate that a person's address has changed. The new address is given in the `address` slot.

The first pattern in the `process-moved-information` rule determines whether an address change needs to be processed, and the second pattern finds the `person` fact for which the address information will need to be changed. The fact address of the `moved` fact is bound to the variable `?f1` so that this fact can be retracted once the change is processed. The fact address of the `person` fact is bound to the variable `?f2`, which is later used on the RHS of the rule to modify the value of the `address` slot.

Note that variables bound to values within a fact and variables bound to the fact address of a fact can both be used. In addition, the value of the `?address` variable can still be used on the RHS after the fact from which it received its value has been retracted.

Retracting the `moved` fact on the RHS of the `process-moved-information` rule is important for the rule to work correctly. Notice what happens when the `retract` command is removed:

```
CLIPS>
(defrule process-moved-information
   (moved (name ?name) (address ?address))
   ?f2 <- (person (name ?name))
   =>
   (modify ?f2 (address ?address)))
CLIPS> (unwatch facts)
CLIPS> (unwatch rules)
CLIPS> (reset)
CLIPS> (watch facts)
CLIPS> (watch rules)
CLIPS> (watch activations)
CLIPS> (watch activations)
CLIPS> (run 3)
FIRE    1 process-moved-information: f-2,f-1
==> f-1    (person (name "John Hill"))
           (address "25 Mulberry Lane"))
==> f-3    (person (name "John Hill"))
           (address "37 Cherry Lane"))
==> Activation 0 process-moved-information: f-2,f-3
FIRE    2 process-moved-information: f-2,f-3
<== f-3     (person (name "John Hill"))
             (address "37 Cherry Lane"))
==> f-4     (person (name "John Hill"))
             (address "37 Cherry Lane"))
==> Activation 0 process-moved-information: f-2,f-4
FIRE 3 process-moved-information: f-2,f-4
<== f-4     (person (name "John Hill"))
             (address "37 Cherry Lane"))
==> f-5     (person (name "John Hill"))
            (address "37 Cherry Lane"))
==> Activation 0 process-moved-information: f-2,f-5
CLIPS>
```

The program executes an infinite loop since it asserts a new person fact after modifying the fact bound to ?f2, thus reactivating the process-moved-information rule. Remember that a modify command is treated as a retract command followed by an assert command. Since the run command was told to fire only three rules, that is when the program stopped. If no limit argument had been given to the run command, the program would have looped endlessly. The only way to stop an infinite loop like this is by interrupting CLIPS using Control-C, or another appropriate interrupt command for the computer on which CLIPS is running.

## 7.22 SINGLE-FIELD WILDCARDS

Sometimes it is useful to test for the existence of a field within a slot without actually assigning a value to a variable. This is particularly useful for multifield slots. For example, suppose we want to print the social security number of every person with a specified last name. The following shows the deftemplate used to describe each person, a deffacts with some predefined people, and a rule to print the social security numbers of every person with a specified last name:

```
(deftemplate person
   (multislot name)
   (slot social-security-number))
(deffacts some-people
   (person (name John Q. Public)
           (social-security-number 483-98-9083))
   (person (name Jack R. Public)
           (social-security-number 483-98-9084)))
(defrule print-social-security-numbers
   (print-ss-numbers-for ?last-name)
   (person (name ?first-name ?middle-name
             ?last-name)
           (social-security-number ?ss-number))
=>
   (printout t ?ss-number crlf))
```

The print-social-security-numbers rule binds the first and middle names of the person to the variables ?first-name and ?middle-name, respectively. These variables, however, are not referred to by actions on the RHS or other pattern or slots on the LHS of the rule. Instead of using a variable, a single-field wildcard can be used when a field is required, but the value is not important. A single-field wildcard is represented by a question mark. Using single-field wildcards, the print-social-security-numbers rule can be rewritten as follows:

```
(defrule print-social-security-numbers
  (print-slot-numbers-for ?last-name)
  (person (name ? ? ?last-name)
    (social-security-number ?ss-number))
=>
  (printout t ?ss-number crlf))
```

Note that the name slot of a person fact must contain exactly three fields for the print-social-security-numbers rule to be activated. For example, the fact:

```
(person (name Joe Public)
  (social-security-number 345-89-3039))
```

would not satisfy the print-social-security-numbers rule.

Notice the importance of not including a space between the question mark and the symbolic name of a variable. The pattern:

```
(person (name ?first ?last))
```

expects two fields for the name slot, but the pattern:

```
(person (name ?first ? last))
```

expects three fields for the name slot, and the last field must be the symbol last.

When a single-field slot is left unspecified in a pattern, CLIPS automatically treats it as if there is a single-field wildcard check for that slot. For example, the pattern:

```
(person (name ?first ?last))
```

is equivalent to:

```
(person (name ?first ?last)
  (social-security-number ?))
```

## 7.23 BLOCKS WORLD

To demonstrate variable bindings, we will build a program to move blocks in a simple blocks world. This type of program is analogous to the classic blocks world program in which the knowledge domain is restricted to blocks (Firebaugh 88). This is a good example of planning and might be applied to automated manufacturing, where a robot arm manipulates parts.

The only things of interest in a blocks world are blocks. A single block may be stacked on another block. The goal of a complex blocks world program is to rearrange the stacks of blocks into a goal configuration with the minimum number of moves. For this example, a number of simplifying restrictions will be made. The first of these restrictions is that only one initial goal is allowed, and this goal can only be to move one block on top of another. With this restriction it is rather trivial to determine the optimal moves to achieve the goal. If the goal is to move block x on top of block y, then move all blocks (if any) on top of block x to the floor and all blocks (if any) on top of block y to the floor and then move block x on top of block y.

The second restriction will be that any goal must not already have been achieved. That is, the goal cannot be to move block x on top of block y if block x is already on top of block y. This is a rather simple condition to check; however, the appropriate syntax to test for this condition will not introduced until Chapter 8.

To begin to solve this problem, it will be useful to set up a configuration of blocks that can be used for testing the program. Figure 7.2 shows the configuration that will be used. There are two stacks in this configuration. The first stack has block A on top of block B on top of block C. The second stack has block D on top of block E on top of block F.

Figure 7.2 Blocks World Initial Configuration

![](img/2c460d4de56b7ffaad3834eee20beaa0_441_0.png)

To determine which type of rules would be effective in solving the problem, a step-by-step completion of a blocks world goal is useful. What steps must be taken to move block C on top of block E? The easiest solution for this problem would be to directly move block C on top of block E. However, this rule could only be applied if both block C and block E had no blocks on top of them. The pseudocode for this rule would be:

