The ability to formally verify theorems involving classified Markovian models and the proof script only consists of about 400 lines code in HOL. The short script clearly indicates the usefulness of the formalization, presented in the earlier chapters of this manuscript, as without them the reasoning could not have been done in such a straightforward manner.

# 7.4.2 Birth-Death Process

The Birth-Death process (Trivedi, 2002) is an important sub-class of Markov chains as it involves a state space with non-negative integers. Its remarkable feature is that all one-step transitions lead only to the nearest neighbor state. The discrete-time Birth-Death Processes are mainly used in analyzing software stability, for example, verifying if a data structure will have overflow problems.

The discrete-time Birth-Death Process can be described as a state diagram depicted in Figure 3.

In the above diagram, the states 0, 1, ..., i, ... are associated with the population. The transition probabilities b_i represents the probability of a birth when the population is i,d_i denotes the probability of a death when the population becomes i, and a_i refers to the population in the state i.

Considering 0 <= a_i <= 1 < b_i < 1 and 0 < d_i < 1 (for all i, 1 <= i <= n), the Birth-Death process described here is not a pure birth or pure death process as the population is finite. Thus, the Birth-Death process can be modeled as an aperiodic and irreducible DTMC.

In this DTMC model, the amount of population, usually considered, is greater than 1. Also, a_i, b_i, and d_i should satisfy the additivity of probability axiom. Then, the discrete-time Birth-Death process can be formalized as:

```
Definition 7.12
|- \/ X p a b c d n p_o.
DB_MODEL X p a b d n p_o =
Aperiodic_MC X p ([ 0, n ], POW [ 0, n ]) p_o (DBLt a b d) \/
Irreducible_MC X p ([ 0, n ], POW [ 0, n ]) p_o (DBLt a b d) \/
1 < n /\ (a_0 + b_0 = 1) /\
\/ j. 0 < j /\ j < n => (a_j + b_j + d_j = 1) /\
\/ j. j < n => 0 < b_j /\ b_j < 1 /\ 0 < d_j /\ d_j < 1
```

# Figure 3. State diagram of discrete-time birth-death process

![](bbox=[0.14, 0.81, 0.86, 0.9])