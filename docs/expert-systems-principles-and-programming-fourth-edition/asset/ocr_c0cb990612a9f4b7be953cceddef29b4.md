the result is:

E = max[min(0.9, 0.8, 0.3), min(-0.5, -(-0.4))]
= max[0.3, -0.5]
= 0.3

# The fundamental formula for the CF of a rule:

```
IF E THEN H
```

is given by the formula:

```
(8) CF(H, e) = CF(E, e) CF(H, E)
```

where:

+   - CF(E,e) is the certainty factor of the evidence E making up the antecedent of the rule based on uncertain evidence e.
+   - CF(H,E) is the certainty factor of the hypothesis assuming that the evidence is known with certainty, when CF(E,e) = 1.
+   - CF(H,e) is the certainty factor of the hypothesis based on uncertain evidence e.

Thus, if all the evidence in the antecedent is known with certainty, the formula for the certainty factor of the hypothesis is:

```
CF(H, e) = CF(H, E)
```

since CF(E,e) = 1.

As an example of these certainty factors, consider the CF for the streptococcus rule discussed before.

+   - IF 1) The stain of the organism is gram positive, and
+   - 2) The morphology of the organism is coccus, and
+   - 3) The growth conformation of the organism is chains
+   - THEN There is suggestive evidence (0.7) that the identity of the organism is streptococcus

where the certainty factor of the hypothesis under certain evidence is:

```
CF(H, E) = CF(H, E1 ∩ E2 ∩ E3) = 0.7
```

and is also called the attenuation factor.

The attenuation factor is based on the assumption that all the evidence—E1, E2, and E3—is known with certainty. That is,

```
CF(E1, e) = CF(E2, e) = CF(E3, e) = 1
```