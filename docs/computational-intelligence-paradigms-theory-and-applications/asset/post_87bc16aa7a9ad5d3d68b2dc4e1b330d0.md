
![](img/d9a4cc12c48f7466f309cbd3c4549c73_383_0.png)

**FIGURE 9.6:** Architecture of NEFCON

## 9.3.4 Neuro-Fuzzy Control (NEFCON)

NEFCON is designed to implement Mamdani type FIS and is illustrated in Figure 9.6. The connections between the layers in NEFCON are weighted with fuzzy sets and rules so-called shared weights. These weighted connections assure the unity of the rule base. Among the three layers in the NEFCON structure, the input units present the linguistic values, and the output unit is the defuzzification interface. The intermediate hidden layer serves as the fuzzy inference. NEFCON model uses a combination of reinforcement and backpropagation learning. NEFCON is capable of learning an initial rule base, if no prior knowledge about the system is available or even to optimize a manually defined rule base. NEFCON has two variants: NEFPROX (for function approximation) and NEFCLASS (for classification tasks).

### NEFCON Learning Algorithm

The NEFCON rule base is learned using incremental rule learning or decremental rule learning. Incremental rule learning is used in cases where the correct output cannot be predicted and where the rules are created based on the estimated output values. As the learning process proceeds, more rules are created. In decremental rule learning, initially rules are created due to fuzzy partitions of process variables and unnecessary rules are eliminated in the course of learning. Incremental rule learning is more efficient than the decremental approach. Assume a process with n state variables, consisting of p_i fuzzy sets, and a control variable with q linguistic terms, at most N linguistic rules are created, where N = q∏_{i=1}^{n} p_i. Therefore the rule base is inconsistent. The rules must be consistent with k rules and the condition k ≤ N/q must be satisfied.

The learning algorithm is performed in stages as follows:

- **First stage**: Here all rule units are deleted which provide an output value with a sign different from optimal output value.
- **Second stage**: In this stage, the subsets of rules with similar antecedents are taken and the rule which matches the current state is chosen to contribute to the NEFCON output. At the end of this stage, from each rule subset only the rule with the smallest error is kept, and all the other rules are deleted from the NEFCON system.

### Decremental Rule Learning

Let R denote the set of all rule units and Ant(R_r) denote the antecedent and Con(R_r) the consequent of a fuzzy rule corresponding to the rule unit R_r. Let S be a process with n state variables ξ_i ∈ X_i (i ∈ {1, ..., n}) which are portioned by p_i fuzzy sets each and one control variable η ∈ Y, portioned by q fuzzy sets. Let there be also initial rules with

`(∀R, R° ∈ R((Ant(R) = Ant(R°) ∧ Con(R) = Con(R°)) ⇒ R = R°))`

- **1.** For each rule unit R_r, a counter C_r (initialized to zero) is defined, r ∈ {1, ..., N}. For a fixed number of iterations m_1 the following steps are carried out:
  - Determine the current NEFCON output O_η using the current state of S.
  - For each rule R_r determine its contribution t_r to the overall output O_η, r ∈ {1, ..., N}.
  - Determine sgn(η_opt) for the current input values.
  - Delete each rule unit R_r with sgn(t_r) ≠ sgn(η_opt) and update the value of N.
  - Increment the counter C_r for all R_r with o_r > 0.
  - Apply O_η to S and determine the new input values.

- **2.** For each rule unit R_r, a counter Z_r (initialized to zero) is defined. For a fixed number of iterations m_2 the following steps are carried out:
  - From all subsets R_r = {R_r | Ant(R_r) = Ant(R_s)} (r, s ∈ {1, …, N}) ⊆ R, one rule unit R_r is selected arbitrarily.
  - Determine the current NEFCON output O_n using only the units selected and the current state of S.
  - Apply O_n to S and determine the new input values.
  - For each rule R_rj determine its contribution t_rj to the overall output O_n, r ∈ {1, …, N}.
  - Determine sgn(η_opt) for the current input values.
  - Add |O_rj| to the counter Z_r of each selected unit R_rj.
  - For all selected rule units R_rj with O_rj > 0, C_rj is incremented.

- **3.** Delete all rule units R_sj for all subsets R_j from the network for which there is a rule unit R_sj ∈ R_j with Z_rj < Z_sj, and delete all rule units R_r with C_r < β · (m_1 + m_2), 0 ≤ β < 1, from the network and update the value of N.

- **4.** Apply appropriate FEBP algorithm to the NEFCON system with k = N remaining rule units.

### Incremental Rule Learning

In this learning process the rule base is developed from scratch by adding rule after rule. The rule base is developed by classifying an input vector initially, i.e., finding the membership function corresponding to each variable that generates the highest membership value for the respective input value, thus forming a rule antecedent. The training algorithm attempts to approximate the output value by deducing it from the present fuzzy error. To commence the algorithm, an initial fuzzy partition must be allotted to each variable.

Let S be a process with n state variables ξ_i ∈ X_i (i ∈ {1, …, n}) which are partitioned by p_i fuzzy sets each and one control variable η ∈ [y_min, y_max] partitioned by q fuzzy sets. Let there also be initial k predefined rule units, where k may be zero. The following steps give the incremental rule-learning algorithm.

- **1.** For a fixed number m_1 of iterations the following steps are carried out.
  - For the current input vector (x_1, ..., x_n) find those fuzzy sets (μ^(1), ..., μ^(n)) for which (∀i, j)(μ^(i)(x_i) ≥ μ^(j)(x_i)) holds.
  - If there is no rule with the antecedent: If ξ_i is μ^(i) and ξ_n is μ^(n), then the fuzzy set v̂ such that (∀j)(v̂(v_0) ≥ v_j(v_0)) holds, where the heuristic output value o is determined by `o = { m + |E| · (y_max − m) if E ≥ 0; m − |E| · (m − y_min) if E < 0 }`, where m = (y_max + y_min)/2.
  - Enter the rule: If ξ_i is μ^(i) and ξ_n is μ^(n), then η is v̂; into the NEFCON system.

- **2.** For a fixed number m_2 iterations the following steps are carried out:
  - Propagate the current input vector through the NEFCON system and estimate for each rule R_r its contribution t_r to the overall output O_n. Compute the desired contribution to the system output value by `t_r* = t_r + σ·o_r·E`, where E is the extended fuzzy error and σ > 0 is the learning rate.
  - For each rule unit R_r, determine the new output membership function v_r such that (∀i)(v_r(t_r*) ≥ v_r(t_r)).
  - Delete all rules that have not been used in more than p % of all propagations.
  - Apply appropriate FEBP algorithm to the NEFCON system.

Rule-learning algorithm is mainly applied to examine the present rules and evaluate them. All the rule units undergo the test process and if they do not pass this test they are eliminated from the network. Here the algorithm has to choose the rule with the lowest error value from each subset that consists of rules with identical antecedents, and delete all other rules of each subset. The entire state space must be learned so that a good rule base is produced. Since the incremental rule learning is a complex process, it is optimal for larger systems, while the decremental rule learning can be applied to smaller systems. In order to reduce the cost of the learning procedure for decremental rule learning two criteria are considered:

- If the consequent corresponding to an antecedent is known, then an equivalent rule unit is put into the NEFCON system, and the rule is not deleted.
- For a few states only a subset of all possible rules are to be considered, in that case only these rules are put into the network.

A similar situation is applicable to incremental rule learning, whereby if prior knowledge is available, then rule learning does not need to start from scratch.

## 9.3.5 Fuzzy Inference and Neural Network in Fuzzy Inference Software (FINEST)

FINEST is capable of two kinds of tuning processes: the tuning of fuzzy predicates, combination functions, and the tuning of an implication function. The generalized Modus Ponens is improved in the following four ways:

- (1) Aggregation operators that have synergy and cancellation nature
- (2) A parameterized implication function
- (3) A combination function that can reduce fuzziness
- (4) Backward chaining based on generalized Modus Ponens

### FINEST Architecture and Training Algorithm

The parameter tuning in FINEST is done by the backpropagation algorithm. Figure 9.7 shows the layered architecture of FINEST and the calculation process of the fuzzy inference. FINEST provides a framework to tune any parameter, which appears in the nodes of the network representing the calculation process of the fuzzy data if the derivative function with respect to the parameters is given.

In Figure 9.7, the input values (x_i) are the facts and the output value (y) is the conclusion of the fuzzy inference.

Consider the following fuzzy rules and facts:

```
Rule i: If x_i is A_i1 and x_n is A_in then y is B_i
Fact j: x_j is A_j° (j = 1,..., n, i = 1,...,m)
```

The calculation procedure in each layer is as follows:

Layer 1: Converse truth value qualification for condition j of rule i,

```
τ_AiJ(a_ij) = sup μ_Aj°(x_j)
μ_AiJ(x_j) = a_ij
```
