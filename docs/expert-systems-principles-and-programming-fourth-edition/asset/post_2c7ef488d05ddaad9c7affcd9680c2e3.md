
The likelihood values LS and LN must be provided by a human expert in order to compute the posterior odds. The form of equations (5) and (8) is simple for people to understand. The LS factor shows how much the prior odds are changed when the evidence is present. The LN factor shows how much the prior odds are changed when the evidence is absent. These forms make it easier for a human expert to then specify the LS and LN factors.

As an example, in the PROSPECTOR expert system, there is a rule which specifies how evidence of a certain mineral supports a hypothesis:

```
IF there are quartz-sulfide veinlets
THEN there is a favorable alteration
for the potassic zone
```

This particular intermediate hypothesis provides support for other hypotheses leading to the top-level hypothesis that copper is present. The LS and LN values for this rule are:

```
LS = 300
LN = 0.2
```

which means that observation of quartz-sulfide veinlets is very favorable while not observing the veinlets is mildly unfavorable. If LN were << 1, then the absence of quartz-sulfide veinlets would strongly suggest the hypothesis is false.

Table 4.10 Relationship Among Likelihood Ratio, Hypothesis, and Evidence

| LS | Effect on Hypothesis |
|---|---|
| 0 | H is false when E is true or E' is necessary for concluding H |
| small (0 < LS << 1) | E is unfavorable for concluding H |
| 1 | E has no effect on belief of H |
| large (1 << LS) | E is favorable for concluding H |
| ∞ | E is logically sufficient for H or Observing E means H must be true |

Table 4.11 Relationship Among Likelihood of Necessity, Hypothesis, and Evidence

| LN | Effect on Hypothesis |
|---|---|
| 0 | H is false when E is absent or E is necessary for H |
| small (0 < LN << 1) | Absence of E is unfavorable for concluding H |
| 1 | Absence of E has no effect on H |
| large (1 << LN) | Absence of E is favorable for H |
| ∞ | Absence of E is logically sufficient for H |

An example is the rule:

```
IF glassy limonite
THEN best mineralization favorability
```

with:

```
LS = 1000000
LN = 0.01
```

## 4.13 UNCERTAINTY IN INFERENCE CHAINS

Uncertainty may be present in rules, evidence used by the rules, or both. In this section, you will see some real-world problems of uncertainty and how probability provides an answer.

### Expert Inconsistency

From equation (4) of the preceding section,

```
if LS > 1 then P(E | H') < P(E | H)
```

Subtracting each side from 1 reverses the inequality:

```
1 - P(E | H') > 1 - P(E | H)
```

Since P(E' | H) = 1 - P(E | H), and P(E' | H') = 1 - P(E | H'), then (7) becomes:

```
LN = \frac{1 - P(E | H)}{1 - P(E | H')} < 1
```

The constraints on the values of LS and LN are summarized as the following:

- Case 1: LS > 1 and LN < 1

From equations (4) and (7), the other cases are:

- Case 2: LS < 1 and LN > 1
- Case 3: LS = LN = 1

Although these three cases are mathematically rigorous constraints on the values of LS and LN, they don't always work out in the real world. For the expert system PROSPECTOR used for mineral exploration, it was not uncommon for experts to specify an LS > 1 and LN = 1, which is not one of these three cases. That is, the expert is saying that the observation of evidence is important but the absence of the evidence is unimportant.

This last case shows that the likelihood theory based on Bayesian probability theory is incomplete for the mineral exploration problem. That is, the Bayesian likelihood theory is only an approximation to a theory that can also deal with the case that LS > 1 and LN = 1. For domains in which experts' opinions satisfy one of the first three cases, the Bayesian likelihood theory is satisfactory.

### Uncertain Evidence

In the real world we are seldom absolutely sure of anything except death and taxes and now with cloning and cryonics we're not even sure about death. Although so far we have concentrated on uncertain hypotheses, the more general and realistic situation is uncertain hypotheses and uncertain evidence.

For the general case, assume that the degree of belief in the complete evidence, E, is dependent on the partial evidence, e, by:

```
P(E | e)
```

The complete evidence is the total evidence which represents all possible evidence and hypotheses which compose E. The partial evidence, e, is the portion of E that we know. If we do know all the evidence, then E = e and:

```
P(E | e) = P(E)
```

where P(E) is the prior likelihood of the evidence E. The likelihood P(E | e) is our belief in E given our imperfect knowledge, e, of the complete evidence E.

For example, suppose that people in your neighborhood who started drilling for oil in their kitchens have become rich. You may consider a hypothesis and evidence:

```
H = I'm going to get rich
E = there is oil under my kitchen
```

as expressed in the rule:

```
IF there is oil under my kitchen
THEN I'm going to get rich       P(H | E) = 1
```

At this initial stage, you do not know for certain that there is oil under your kitchen. Conclusive evidence would be drilling a test well, but this is rather expensive. So you consider the partial evidence, e, in support of E as follows:

- Other people in the neighborhood have struck it rich.
- There is some black substance always seeping up around the kitchen stove (which your spouse has blamed on your cooking and cleaning until now).
- A stranger came to the door and offered $20,000,000 for your house because she said that she liked the view.

Based on this partial evidence, you may decide that the likelihood of oil under your kitchen is rather high, P(E | e) = 0.98.
In a probabilistic or likelihood type of inference chain, if H depends on E and E is based on some partial evidence e, then P(H | e) is the likelihood that H depends on e. By the rule for conditional probability:

```
P(H | e) = \frac{P(H \cap e)}{P(e)}
```

Figure 4.15 illustrates how H can be considered to be made up of E and e. So the above becomes:

Figure 4.15 The Intersection of H and e

![](img/2c460d4de56b7ffaad3834eee20beaa0_246_0.png)

```
P(H | e) = \frac{P(H \cap E \cap e) + P(H \cap E' \cap e)}{P(e)}
```

Using the rule of conditional probability gives:

```
P(H | e) = \frac{P(H \cap E | e)P(e) + P(H \cap E' | e)P(e)}{P(e)}
```

```
(1) P(H | e) = P(H \cap E | e) + P(H \cap E' | e)
```

Another way of expressing (1) follows since:

```
P(H \cap E | e) = \frac{P(H \cap E \cap e)}{P(e)}
```

(2) P(H | E ∩ e) = \frac{P(H | E ∩ e) P(E ∩ e)}{P(e)}

and since:

P(E | e) = \frac{P(E ∩ e)}{P(e)}

then (2) becomes:

P(H | E ∩ e) = P(H | E ∩ e) P(E | e)

Likewise:

P(H | E' | e) = P(H | E' ∩ e) P(E' | e)

and (1) becomes:

(3) P(H | e) = P(H | E ∩ e) P(E | e) + P(H | E' ∩ e) P(E' | e)

Normally, we do not know the probabilities P(H | E ∩ e) and P(H | E' ∩ e). However, if we assume these can be approximated by P(H | E) and P(H | E'), then (3) simplifies to:

(4) P(H | e) = P(H | E) P(E | e) + P(H | E') P(E' | e)

Equation (4) is essentially a linear interpolation of P(H | e) vs. P(E | e). The endpoints are:

- (i) E is true and so P(H | e) = P(H | E).
- (ii) E is false and so P(H | e) = P(H | E').

The problem with equation (4) shows up when P(E | e) equals the prior probability P(E). If the system obeys pure Bayesian probability, then:

(5) P(H | e) = P(H | E) P(E) + P(H | E') P(E')
(6) P(H | e) = P(H)

which is correct.

However, in the real world, experience has shown that human experts give subjective probabilities that are almost certain to be inconsistent. For example, if the expert uses the inconsistent case of LS > 1 and LN = 1, then:

O(H | E') = LN O(H) = O(H)

and since:

```
O = \frac{P}{1 - P}
```

then:

```
(7) P(H | E') = P(H)
```

Using (7) in (5) gives:

```
P(H | e) = P(H | E) P(E) + P(H) P(E')
= P(H | E) P(E) + P(H) (1 - P(E))
```

```
(8) P(H | e) = P(H) + P(H | E) P(E) - P(H) P(E)
```

Now:

```
O(H | E) = LS O(H)
```

If LS = 1, then:

```
O(H | E) = O(H)
P(H | E) = P(H)
```

Since the human expert has specified LS > 1, then P(H | E) > P(H) and so the term:

```
P(H | E) P(E) - P(H) P(E)
```

in equation (8) will be > 0, where 0 is the lower bound when LS = 1. So from (8):

```
P(H | e) > P(H)
```

when LS > 1 and LN = 1. This contradicts the fact that P(H | e) should equal P(H) when P(E | e) = P(E). Since P(H | e) > P(H), the probability is greater than it should be and may become magnified further as the inference from one rule is used by another in an inference chain.

### Correcting Uncertainty

One way of correcting this problem is to assume that P(H | e) is a piece-wise linear function. This is an ad hoc assumption that worked well with PROSPECTOR but is not based on traditional probability theory. The function is chosen linear for simplicity in calculations.
