As an example of representing rules using this format, consider the decision tree in Figure 12.2. This tree can easily be converted to rules using AV pairs, as described previously. The pseudocode for the converted rules is:

```
IF main-course is red-meat
THEN best-color is red

IF main-course is poultry and
meal-is-turkey is yes
THEN best-color is red

IF main-course is poultry and
meal-is-turkey is no
THEN best-color is white

IF main-course is fish
THEN best-color is white
```

The attributes used in the rules are main-course, meal-is-turkey, and best-color. The main-course attribute corresponds to the answer determined by the decision tree question “What is the main course?” The meal-is-turkey attribute corresponds to the answer determined by the question “Is the main course turkey?” Notice that the branch of the decision tree that determines that the best color is unknown is not represented as a rule, since one of the limitations of our backward chainer is that unknown values are not represented. If the main course is not one of these that produce an answer, in this case the user will be asked the value of the best-color attribute.

The following defects show how the wine rules can be represented using the backward-chaining rule format. Since these rule facts are not an intrinsic part of the backward-chaining mechanism, they’ll be placed in the MAIN module (recall that the MAIN module imports from all other modules, so the rule deftemplate will be visible to it):

```
(deffacts MAIN::wine-rules
  (rule (if main-course is red-meat)
        (then best-color is red))

  (rule (if main-course is fish)
        (then best-color is white))

  (rule (if main-course is poultry and
        meal-is-turkey is yes)
        (then best-color is red))

  (rule (if main-course is poultry and
        meal-is-turkey is no)
        (then best-color is white))))
```