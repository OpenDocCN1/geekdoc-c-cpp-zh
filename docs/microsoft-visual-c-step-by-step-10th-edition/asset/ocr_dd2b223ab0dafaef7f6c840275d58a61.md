judging criteria for a talent contest. A contestant is assessed on their dancing and singing abilities. A judge awards a value from 0 (no talent whatsoever) to 10 (should be a professional) for each ability. A contestant progresses to the next stage of the contest as long as they score 7 or more for each ability:

Click here to view code image

```
int dancingAbility = ... // Value assigned by judge
singingAbility = ... // Value assigned by judge
bool canMoveToNextStage = (dancingAbility >= 7) && (singingAbility >= 7);
```

![](bbox=[0.125, 0.316, 0.857, 0.45])

The outcome of the || operator is true if either of the Boolean expressions evaluates true. You use the || operator to determine whether one of a combination of Boolean expressions is true. For example, the following statement assigns the value true to eliminateContest if the value of dancingAbility is less than 7 or the value of singingAbility is less than 7:

Click here to view code image

```
bool eliminateContestant = (dancingAbility < 7) || (singingAbility < 7);
```

# Short-circuiting

The && and || operators both exhibit a feature called short-circuiting. Short-circuiting describes the situation when it is not necessary to evaluate both operands when as the result of a conditional logical expression. For example, if the left operand of the && operator evaluates to false, the result of the entire expression must be false, regardless of the value of the right operand. Similarly, if the value of the left operand of the || operator evaluates to true, the result of the entire expression must be true, irrespective of the value of the right