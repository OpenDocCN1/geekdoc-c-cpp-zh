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