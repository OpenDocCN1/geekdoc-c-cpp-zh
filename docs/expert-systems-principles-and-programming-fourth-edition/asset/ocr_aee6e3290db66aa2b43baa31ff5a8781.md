# Figure 4.23 Simplified Portion of the PROSPECTOR Partitioned Semantic Net for the STIR Rule Using FMGS Evidence

![](bbox=[0.05, 0.11, 0.86, 0.57])

many of the formulas that you have seen. Referring back to Figure 4.19, we will follow the propagation of probabilities from the evidence node “the Region Contains Intrusive Breccias,” with acronym RCIB.

If the user says that intrusive breccias are certainly present, then:

```
P(E | e) = P(RCIB | e) = 1
```

From Figure 4.19, notice that the LN values for the other evidence of SMIR are all 1. That is, if the user makes no comment about evidence for stocks, dikes, and volcanic plugs, these make no contribution to SMIR and so can be ignored in the propagation of probabilities.

The reason all this evidence can be ignored comes from the formula for compound evidence discussed in Section 4.14:

```
O(H | e) = [ \prod_{i=1}^{n} L_i ] O(H)
```