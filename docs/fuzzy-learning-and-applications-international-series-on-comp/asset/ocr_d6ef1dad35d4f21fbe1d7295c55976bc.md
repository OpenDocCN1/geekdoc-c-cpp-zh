not common in other feedforward connectionist systems. The semantic phase transition phenomenon gives a lower bound to the FBF network structure: the FBF network must contain a number of rules at least equal to the number of classes to be discriminated. The semantic phase transition observed for the FBF network can be explained by the specialization of each rule in a specific class. Even though it is hard to fully understand how a single rule of the system works, it is very easy to deduce the functional problem solved by each rule. Moreover, we have observed that the set of rules in a system with more than 10 rules can always be partitioned into 10 different subsets, each responsible for the classification of the examples of a specific class. Thus, even if the FBF network is organized as a supervised feedforward network, its behavior is closer to the one of a competitive model showing a strong specialization of the fuzzy rules. A pruning technique was proposed by Casalino et al. [5], in order to automatically remove less relevant fuzzy rules from an oversized system.

# 4.8 The Simplified FBF Network and Its Extension

For pattern recognition applications, from this FBF network a Simplified FBF network (SFBF network) can be obtained by assuming, in accordance with rule specialization [1]:

```
ȳ_ij ≡ δ_ij = { 1 if rule j is associated to class i, 0 otherwise. (4.23)
```

This assumption leads to both a system with as many units as classes and a strong simplification of the learning formulas, which become:

```
Δm_jk = η_m φ_j Υ_ij [x_k − m_jk]/σ²_jk (4.24)
```

```
Δσ_jk = η_o φ_j Υ_ij [x_k − m_jk]²/σ³_jk (4.25)
```

with

```
Υ_ij = { (y_i − 1)² if j = i y_i² − y_i if j ≠ i } (4.26)
```

It is worth noting that, from Eq. 4.23 and the form of the defuzzifier, y ∈ (0,1) follows, and consequently

```
Υ_ij = { ≥ 0 if j = i ≤ 0 if j ≠ i } (4.27)
```

holds.

Therefore, the learning rules of the SFBF network are competitive. During training, the means of the Gaussian membership functions of each rule move towards the patterns of the class associated to that rule, and escape from