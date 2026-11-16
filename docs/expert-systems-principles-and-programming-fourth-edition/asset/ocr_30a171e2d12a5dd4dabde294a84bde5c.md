```
IF main-course is poultry and
meal-is-turkey is red
THEN best-color is red
```

is modified to the following rule:

```
IF meal-is-turkey is yes
THEN best-color is red
```

which is represented by fact f-9. Similarly, this new fact causes an activation of the attempt-rule rule to replace the activation lost when the fact representing the rule was retracted.

Allowing the first attempt-rule activation to fire produces the following output:

```
CLIPS> (run 1).|
FIRE 1 attempt-rule: f-1,f-9,
==> f-10 (goal (attribute meal-is-turkey))
CLIPS> (agenda).|
0 ask-attribute-value: f-10.,
For a total of 1 activation.
CLIPS>
```

The fact f-10 is asserted representing a goal to determine the value of the meal-is-turkey attribute. Since no rule assigns the value of this attribute, the ask-attribute-value rule is activated to determine the value.

Allowing the ask-attribute-value rule to fire produces the following output:

```
CLIPS> (run 1).|
FIRE 1 ask-attribute-value: f-10.,
==> f-10 (goal (attribute meal-is-turkey))
What is the value of meal-is-turkey? yes|
==> f-11 (attribute name meal-is-turkey)
(value yes))
CLIPS> (agenda).|
100 rule-satisfied: f-1,f-11,f-9
100 remove-rule-no-match: f-1,f-11,f-8
For a total of 2 activations.
CLIPS>
```

An attribute fact representing the value of the meal-is-turkey attribute is asserted as a result of this rule firing. In addition, the goal fact to determine the value of this attribute is removed. The new attribute fact causes two activations. The first activation is for the remove-rule-no-match rule. Since fact f-8's first condition is inconsistent with the value of the new attribute and the rule represented by the fact is no longer applicable, this fact needs to be removed. The second activation is for the rule-satisfied rule. Since fact f-8's remaining condition is satisfied by the new attribute fact, the consequent of this fact can be applied.