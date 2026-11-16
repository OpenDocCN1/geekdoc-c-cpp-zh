+   • weighted combinations using the likelihood ratios, LS, and necessity ratios, LN. The posterior odds are calculated from:

O(H | E) = LS O(H)

when the evidence E is known true and:

O(H | E') = LN O(H)

when E is known to be false. If E is not known for certain, then P(H | E) can be calculated by linear interpolation, as discussed in the previous section.

The term weighted combination arises because of the general case in which multiple pieces of evidence contribute to a hypothesis. As shown in the previous section:

O(H | E1 n E2 n ... n En) = [ \prod_{i=1}^{N} LS_i ] O(H)

The log of this is:

log O(H | E1 n E2 n ... n En) = log O(H) + \prod_{i=1}^{N} log LS_i

which can be interpreted as each LSi casting log LSi "votes" for the hypothesis. Each log LS is a weight that affects the hypothesis.

Although PROSPECTOR is sometimes called a rule-based system because weighted combinations correspond to rules such as:

```
IF E1 AND E2 AND ... En THEN H
```

it is not as flexible as a true production system based on rules. One limitation is lack of a full mechanism to bind variables. PROSPECTOR is a custom-designed system that emphasizes efficiency and control for geological applications rather than the generality of a production system.

The weighted combinations are also an example of plausible relations. The term plausible means that there is some evidence for belief. PROSPECTOR is an example of a system that uses plausible inference for or against a hypothesis. The plausible inferences of PROSPECTOR are based on Bayesian probabilities with the LS and LN values supplied by human experts.

Plausible and other different degrees of belief are illustrated in the fuzzy graph of Figure 4.20. The terms have the following general meanings as shown in Table 4.13.

The graph of Figure 4.20 is purposely drawn fuzzy to illustrate the vague nature of these terms and the vagueness in progression from one to another. In