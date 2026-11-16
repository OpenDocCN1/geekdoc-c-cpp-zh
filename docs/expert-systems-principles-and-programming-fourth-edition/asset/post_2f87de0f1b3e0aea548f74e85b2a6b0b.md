
need an “A” in this course to bring up your GPA. The following formula may express your belief in the likelihood of graduation:

(4) P(graduating | ‘A’ in this course) = 0.70

Notice that this likelihood is not 100 percent. The reason it’s not 100 percent is that a final audit of your courses and grades will be made by the school. There could be problems due to a number of reasons that would still prevent your graduation, such as the following:

- 1. School catalog changes so that not all your courses counted toward the degree.
- 2. You forgot to take a required course.
- 3. Rejection of transfer courses.
- 4. Rejection of some elective courses you took.
- 5. Tuition and library fines that you owe and were hoping would be forgotten.
- 6. Your GPA was lower than you thought and an “A” still won’t raise it up.
- 7. “They” are out to get you.

Assuming that you agree with (4) (or perhaps your own value for the likelihood) then by equation (1):

(5) P(not graduating | ‘A’ in this course) = 0.30

Although equation (5) is correct from a probabilistic viewpoint, it seems somehow intuitively wrong. It’s just not right that if you really work hard and get an “A” in this course, then there is a 30 percent chance that you won’t graduate. Equation (5) should make you as uneasy as the medical expert who believes:

P(H | E1 ⊂ E2 ⊂ E3) = 0.70

but won’t believe the probabilistic consequence:

P(H’ | E1 ⊂ E2 ⊂ E3) = 0.30

The fundamental problem is that while P(H | E) implies a cause-and-effect relationship between E and H, there may be no cause-and-effect relationship between E and H’. Yet the equation:

P(H | E) = 1 – P(H’ | E)

implies a cause-and-effect relationship between E and H’ if there is a cause-and-effect between E and H.

These problems with the theory of probability led Shortliffe to investigate other ways of representing uncertainty. The method that he used with MYCIN was based on certainty factors derived from Carnap’s theory of confirmation. Carnap distinguished two types of probability. One type of probability is ordinary probability associated with the frequency of reproducible events. The second type is called epistemic probability or the degree of confirmation because it confirms a hypothesis based on some evidence. This second type is another example of the degree of likelihood of a belief.

## Measures of Belief and Disbelief

In MYCIN, the degree of confirmation was originally defined as the certainty factor, which is the difference between belief and disbelief:

```
CF (H, E) = MB (H, E) - MD (H, E)
```

where:

- CF is the certainty factor in the hypothesis H due to evidence E
- MB is the measure of increased belief in H due to E
- MD is the measure of increased disbelief in H due to E

The certainty factor is a way of combining belief and disbelief into a single number.

Combining the measures of belief and disbelief into a single number has two uses. First, the certainty factor can be used to rank hypotheses in order of importance. For example, if a patient has certain symptoms that suggest several possible diseases, then the disease with the highest CF would be the one that is first investigated by ordering tests.

The measures of belief and disbelief were defined in terms of probabilities by:

```
MB (H, E) = {
  1 if P(H) = 1
  (max[P(H | E), P(H)] - P(H)) / (1 - P(H)) otherwise
}
```

```
MD (H, E) = {
  1 if P(H) = 0
  (min[P(H | E), P(H)] - P(H)) / (0 - P(H)) otherwise
}
```

Now max [1,0] is always 1 and min [1,0] is always 0. The reason for writing 1 and 0 in terms of max and min is to show the formal symmetry between MB and MD. The versions for MB and MD differ only in the replacement of max by min and vice versa.

Based on these definitions, some characteristics are shown in Table 5.1.

| Characteristics | Values |
| :--- | :--- |
| Ranges | 0 <= MB <= 1<br>0 <= MD <= 1<br>-1 <= CF <= 1 |
| Certain True Hypothesis<br>P(H | E) = 1 | MB = 1<br>MD = 0<br>CF = 1 |
| Certain False Hypothesis<br>P(H' | E) = 1 | MB = 0<br>MD = 1<br>CF = -1 |
| Lack of Evidence<br>P(H | E) = P(H) | MB = 0<br>MD = 0<br>CF = 0 |

The certainty factor, CF, indicates the net belief in a hypothesis based on some evidence. A positive CF means the evidence supports the hypothesis since MB > MD. A CF = 1 means that the evidence definitely proves the hypothesis. A CF > 0 means one of two possibilities. First, a CF = MB — MD = 0 could mean that both MB and MD are 0. That is, there is no evidence. The second possibility is that MB = MD and both are nonzero. The result is that the belief is cancelled out by the disbelief. Unfortunately the cancellation of strong belief by disbelief leads not to simple ignorance, but worse, to a state of confusion. For example, what is worse, coming to a street and not knowing which way to turn, or a passenger in your car saying "turn right" while pointing left?

A negative CF means that the evidence favors the negation of the hypothesis since MB < MD. Another way of stating this is that there is more reason to disbelieve a hypothesis than to believe it. For example, a CF = -70 percent means that the disbelief is 70 percent greater than the belief. A CF = 70 percent means that the belief is 70 percent greater than the disbelief. Notice that with certainty factors there are no constraints on the individual values of MB and MD. Only the difference is important. For example:

CF = 0.70 = 0.70 - 0
= 0.80 - 0.10

and so forth.

Certainty factors allow an expert to express a belief without committing a value to the disbelief. As shown in Problem 5.2,

CF(H, E) + CF(H', E) = 0

which means that if evidence confirms a hypothesis by some value CF(H | E) the confirmation of the negation of the hypothesis is not 1 - CF(H | E) which would be expected under probability theory. That is,

CF(H, E) + CF(H', E) != 1

The fact that CF(H | E) + CF(H' | E) = 0 means that evidence supporting a hypothesis reduces support to the negation of the hypothesis by an equal amount so that the sum is always 0.

For the example of the student graduating if an “A” is given in the course,

CF(H, E) = 0.70   CF(H', E) = -0.70

which means:

- (6) I am 70 percent certain that I will graduate if I get an ‘A’ in this course.
- (7) I am –70 percent certain that I will not graduate if I get an ‘A’ in this course.

Notice that the –70 percent comes about because certainty factors are defined on the interval:

-1 ≤ CF(H,E) ≤ +1

where 0 means no evidence. So certainty values greater than 0 favor the hypothesis while certainty factors less than 0 favor the negation of the hypothesis. Statements (6) and (7) are equivalent using certainty factors analogous to the fact that “yes” is not “no”.

The above CF values might be elicited by asking:

> How much do you believe that getting an ‘A’ will help you graduate?

if the evidence is to confirm the hypothesis or:

> How much do you disbelieve that getting an ‘A’ will help you graduate?

An answer of 70 percent to each question will set CF(H | E) = 0.70 and CF(H’ | E) = -0.70. In MYCIN, rather than asking certainties on a percentage scale, the experts were asked to give certainty on a scale of 1 to 10, where 10 was definite. The user could ask UNK for unknown evidence corresponding to CF = 0.

## Calculating with Certainty Factors

Although the original definition of CF was:

CF = MB - MD

there were difficulties with this definition because one piece of disconfirming evidence could control the confirmation of many other pieces of evidence. For example, 10 pieces of evidence might produce a MB = 0.999 and one disconfirming piece with MD = 0.799 could then give:

CF = 0.999 - 0.799 = 0.200

In MYCIN, a rule's antecedent CF must be > 0.2 for the antecedent to be considered true and activate the rule. This threshold value of 0.2 was not done as a fundamental axiom of CF theory, but rather as an ad hoc way of minimizing the activation of rules which only weakly suggest a hypothesis. Without a threshold, many rules may be activated of little or no value and greatly reduce the system's efficiency.

The definition of CF was changed in MYCIN in 1977 to be:

CF = (MB - MD) / (1 - min(MB, MD))

to soften the effects of a single piece of disconfirming evidence on many confirming pieces of evidence. Under this definition with MB = 0.999, MD = 0.799:

CF = (0.999 - 0.799) / (1 - min(0.999, 0.799)) = 0.200 / 0.201 = 0.995

which is very different from the previous definition that gave 0.999 - 0.799 = 0.200 and so did not activate a rule since it was not greater than 0.2. Now the 0.995 will cause the rule to be activated.

The MYCIN methods for combining evidence in the antecedent of a rule are shown in Table 5.2. Notice that these are the same as the PROSPECTOR rules based on fuzzy logic.

| Evidence, E | Antecedent Certainty |
| :--- | :--- |
| E, AND E2 | min [CF(H,E1), CF(H,E2)] |
| E, OR E2 | max [CF(H,E1), CF(H,E2)] |
| NOT E | -CF(H,E) |

For example, given a logical expression for combining evidence such as:

```
E = (E1 AND E2 AND E3) OR (E4 AND NOT E5)
```

the evidence E would be computed as:

```
E = max[min(E1, E2, E3), min(E4, -E5)]
```

For values:

E1 = 0.9   E2 = 0.8   E3 = 0.3
E4 = -0.5  E5 = -0.4
