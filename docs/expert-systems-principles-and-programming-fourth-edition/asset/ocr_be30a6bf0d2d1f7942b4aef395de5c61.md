the attribute main-course. Since this attribute is unknown, a goal is created for it, and is represented by fact f-6. Because there are no rules that assign the value of the main-course attribute, the rule ask-attribute-value rule is activated.

Proceeding with execution, the ask-attribute-value rule fires to determine the value of the attribute main-course:

```
CLIPS> (run 1)
FIRE    1 ask-attribute-value: f-6,,
    <<= f-6    (goal (attribute main-course))
    What is the value of main-course? poultry.
    ==> f-7    (attribute (name main-course)
                (value poultry))
CLIPS> (agenda.)
100    remove-rule-no-match: f-1, f-7, f-3
100    remove-rule-no-match: f-1, f-7, f-2
100    modify-rule-match: f-1, f-7, f-5
100    modify-rule-match: f-1, f-7, f-4
For a total of 4 activations.
CLIPS>
```

Since the user is being asked to supply the value of the main-course attribute, the goal for this attribute f-6 is removed. The value supplied by the user is asserted as the attribute fact f-7. The assertion of this fact causes four new activations to be placed on the agenda. The rules represented by facts f-4 and f-5 each require as the first condition that the main-course attribute be poultry. Since the value of the main-course attribute is poultry, both of these rule facts must be modified to represent that the first condition has been satisfied. Thus both facts cause activations of the modify-rule-match rule. The rules represented by facts f-2 and f-3 both require as the first condition that the main-course attribute be something other than poultry. Thus neither of these facts is applicable any longer. The rule remove-rule-no-match is activated to cause both of them to be removed.

Allowing the two remove-rule-no-match activations to fire produces the following output:

```
CLIPS> (run 2)
FIRE    1 remove-rule-no-match: f-1, f-7, f-3
    == f-3    (rule (if main-course is fish)
                (then best-color is white))
FIRE    2 remove-rule-no-match: f-1, f-7, f-2
    == f-2    (rule (if main-course is red-meat)
                (then best-color is red))
CLIPS> (agenda.)
100    modify-rule-match: f-1, f-7, f-5
100    modify-rule-match: f-1, f-7, f-4
For a total of 2 activations.
CLIPS>
```