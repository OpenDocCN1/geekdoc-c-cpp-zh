# Figure 5.2 Uncertainties in Individual Rules

![](bbox=[0.05, 0.08, 0.88, 0.32])

with the assignment of likelihood values. For probabilistic reasoning, as described in Chapter 4, these uncertainties are with the sufficiency, LS, and necessity, LN, values. Since the LS and LN values are based on estimates from humans, there is uncertainty with them. There is also an uncertainty with the likelihood of the consequent. For probabilistic reasoning, this was written as P(H | E) for certain evidence and P(H | e) for uncertain evidence.

Another source of uncertainty is the combining of the evidence. Should the evidence be combined, as in the following:

```
as E1 AND E2 AND E3
```

```
or as E1 AND E2 OR E3
```

```
or as E1 AND NOT E2 OR E3
```

or some other possible way of logical combination using AND, OR, and NOT?

# Lack of Theory

As mentioned in Chapter 4, the ad hoc introduction of formulas such as fuzzy logic to a probabilistic system introduces a problem. The expert system does not then have a sound theoretical foundation based on classical probability, and so represents an ad hoc method that works for a limited case. The danger of ad hoc methods is that there is no complete theory to guide the application or warn of inappropriate situations.

Another example of an ad hoc method that you have seen is the use of LS and LN factors with inference networks. Theoretically, an inference net with N nodes is a probabilistic system with an event space of N possible events. Thus, there are 2^N possible probabilities. In practice, for real-world situations, few of these probabilities are known. Rather than trying to enumerate all the probabilities, the LS and LN factors are used for significant (we hope) arcs between nodes. Use of LS and LN values for significant arcs greatly reduces the complexity of the net.