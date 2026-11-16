Given as input facts representing the chassis and any gizmos that have been selected, write a program that generates facts representing the number of gizmos used, the total amount of power required for the gizmo, and the total price of the chassis and all gizmos selected.

+   8.15 Using the gem table from Problem 7.13 on page 363, write rules for identifying the following gems: diamond, corundum, chrysoberyl, spinel, quartz, and tourmaline. Include rules to query the user for the hardness, density, and color of the gem. The user should be prompted until he or she responds with one of the colors listed in the table.

+   8.16 Add rules to the Sticks program that will ask if the human player wants to play again after the game has finished.

+   8.17 Modify the Sticks program to allow two human players to play the game against each other, in addition to the computer playing against a human.

+   8.18 Rewrite the following rules as a single rule using and and or CEs:

```
(defrule rule-1
(fact-a)
(fact-d)
=>)
```

```
(defrule rule-2
(fact-b)
(fact-c)
(fact-e)
(fact-f)
=>)
```

```
(defrule rule-3
(fact-a)
(fact-e)
(fact-f)
=>)
```

```
(defrule rule-4
(fact-b)
(fact-c)
(fact-d)
=>)
```

+   8.19 Write a program using and and or CEs for the AND/OR tree of getting to work shown in Figure 3.10 on page 107. Test it for all branches.

+   8.20 Determine whether the variable x is referenced properly for each of the following rules. Explain your answers.

```
(a) (defrule example-1
(not (fact ?x))
(test (> ?x 4))
=>)
```

```
(b) (defrule example-2
(not (fact ?x (:> ?x 4)))
=>)
```