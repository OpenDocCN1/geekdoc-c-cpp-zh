```
==> f-1    (person (name "John Hill"))
               (address "25 Mulberry Lane"))
==> f-3    (person (name "John Hill"))
               (address "37 Cherry Lane"))
CLIPS>
```

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
```