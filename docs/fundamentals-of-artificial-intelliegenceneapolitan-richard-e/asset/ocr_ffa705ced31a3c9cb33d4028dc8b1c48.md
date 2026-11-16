A: Mr. Holmes' burglar alarm sounds.

B: Mr. Holmes' residence is burglarized.

E: There is an earthquake.

Using the rule-based approach, we might assign the following certainty factors:

```
IF A THEN B with certainty .8
IF E THEN B with certainty -.4
```

When Mr. Holmes learns that his alarm has sounded, he becomes .8 certain that he has been burglarized. When he later learns of the earthquake, he combines the certainty factor .8 with the certainty factor -.4 as follows:

```
.8 + (-.4)
---------------- = .67.
1 - min(|.8|, |-.4|)
```

So his certainty in having been burglarized is reduce to .67.

A difficulty with this model is that E only decreases the certainty in B when we already know A. That is, if the alarm had not sounded, Mr. Holmes would not conclude that it is extremely unlikely that he has been burglarized today (i.e. more unlikely than on any other day) after he heard there was an earthquake. So we cannot have the rule above concerning earthquakes. Instead, we need rules with multiple premises in the antecedent as follows:

```
IF A ^ E THEN B with certainty .67
IF A ^ -E THEN B with certainty .85
```

Note that when we know A and -E, the certainty is higher than when we know only A because we know for sure the other cause is not present. If we wanted to represent additional causes such as an individual being seen lurking around the house, we would need to consider more combinations of assertions in the antecedent.

Another problem with this rule-based approach is that it only allows us to do inference in one direction. That is, if we wanted to model how Mr. Holmes would reason if he learned that he had been burglarized, we would need the following additional rule:

```
IF B THEN A with certainty .7
```

There is no clear connection between the certainty factor in this rule and the rules that do inference in the other direction.