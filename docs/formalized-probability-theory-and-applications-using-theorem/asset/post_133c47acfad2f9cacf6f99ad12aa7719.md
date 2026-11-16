
function (PMF) as Pr (D_t = i) = a_j, where i = 1, 2, ..., n refers to the position of the least recently used page in the stack at time t, and \sum_{j=1}^n a_j = 1. This way the distribution function becomes Pr (D_t \le i) = \sum_{j=1}^i a_j. Now, if a tagged page occupies the i^{th} position in the stack at time t, which is expressed as s_t in Figure 1, then the position of this page in the stack s_{t+1} depends on the next reference x_{s_t} and the position of this page in the stack s_t.

Based on the described updating procedure in the LRU stack, the evaluation of the page-fault rate of the LRU paging algorithm becomes quite simple. If the evaluated program has been allocated i page frames of main memory, then a page fault will occur at time t when D_t > i. Hence, the page fault probability is

F (LRU) = Pr (D_t > i) = 1 - \sum_{j=1}^i a_j \quad (7.2)

The movement of the tagged page through the LRU state is then a random process \{ E_t \}_{t \ge 0}. If the page occupies the i^{th} position in the stack s_t, then E_t = i, for all 1 \le i \le n. Now, we have the following transition probabilities:

p_{1i} = Pr (E_{t+1} = 1 | E_t = i) = Pr (D_{t+1} = i) = a_i, 1 \le i \le n
p_{ii} = Pr (E_{t+1} = i | E_t = i) = Pr (D_{t+1} < i) = \sum_{j=1}^{i-1} a_j, 2 \le i \le n
p_{i, i+1} = Pr (E_{t+1} = i+1 | E_t = i) = Pr (D_{t+1} > i) = 1 - \sum_{j=1}^i a_j, 1 \le i \le n-1
p_{ij} = 0, otherwise.

The LRU stack is then described as an aperiodic and irreducible DTMC by assuming a_i > 0 for all i \in [1, n].

The state diagram of this aperiodic and irreducible DTMC is shown in Figure 2, where the transition probabilities can be expressed as the following higher-order logic function:

### Figure 1. LRU stack updating procedure

![](img/0e284aa46fa831bc38a68343fef110e3_109_0.png)

### Figure 2. State diagram for the LRU stack model

![](img/0e284aa46fa831bc38a68343fef110e3_109_1.png)

### Definition 7.10
\forall a t i j. L t a i j =
If (j = 1) then a i else
If (j - i = 1) then 1 - sum (1, i) (\lambda j. a j) else
If (j = i) then sum (1, i - 1) (\lambda j. a j) else 0

Definition 7.10 can be used to formalize the LRU stack model as:

### Definition 7.11
\forall X p a n p0. LRU_model X p a n p0.
Aperiodic_DTMC X p ({1, n}, POW ({1, n})) p0 (Lt a) \\
Irreducible_DTMC X p ({1, n}, POW ({1, n})) p0 (Lt a) \\
1 \le n \land (\forall j. 0 < j \land j \le n \Rightarrow 0 < a j) \\
(sum (1, n) (\lambda j. a j) = 1)

where the state space is described as a pair ([ 1, n ], POW ([ 1, n ])), in which the first element contains all the states { 1, 2, ... n } and the second one is the sigma algebra of the first element. The condition ( 1 <= n ) is used to avoid the case when the length of the referencing string is zero. The other two conditions represent the specification of the model mentioned above.

Using the formal definition of this LRU stack model, we can now formally reason about its limiting distributions, which are mainly used to describe the stationary behaviors of this model.

In the LRU stack model, there exists lim_{t->infty} p_i^(t_k) for every i in [ 1, n ].

### Theorem 7.7

```
|- forall X p a n p0 P_o i.
LRU_model X p a n p0 P_o /\ i in [ 1, n ]
=> exists u. ( /\ t. prob p ( x | X t x = i ) -> u )
```

The proof of this property is based on Theorem 7.5 and the definition of limit of a real sequence.

In the LRU stack model, lim_{t->infty} p_i^(m) = 1 / n, for every i in [ 1, n ].

### Theorem 7.8

```
|- forall X p a n p0 P_o i.
LRU_model X p a n p0 P_o /\ i in [ 1, n ]
=> ( lim ( /\ t. prob p ( x | X t x = i ) ) = 1 / n )
```

The proof of this property is primarily based on Theorem 7.7 along with Lemma 7.4:

```
|- forall X p a n P_o i j.
LRU_model X p a n P_o /\ i in [ 1, n ] /\ j in [ 1, n ]
=> ( lim ( /\ t. prob p ( x | X t x = i ) ) =
lim ( /\ t. prob p ( x | X t x = j ) ) )
```

The proof of the above lemma is based on DTMC properties along with some arithmetic reasoning.

Theorem 7.8 implies that lim_{t->infty} p_i^(t) (for any tag i) is independent of its initial distribution and the position of the tagged page has an equal probability to be in any stack position. This means that any page is equally likely to be referenced in the long run. As a result, it concludes that this LRU stack specification does not cover the case of non-uniform page referencing behaviors of some programs.

The ability to formally verify theorems involving classified Markovian models and the proof script only consists of about 400 lines of code in HOL. The short script clearly indicates the usefulness of the formalization, presented in the earlier chapters of this manuscript, as without them the reasoning could not have been done in such a straightforward manner.

## 7.4.2 Birth-Death Process

The Birth-Death process (Trivedi, 2002) is an important sub-class of Markov chains as it involves a state space with non-negative integers. Its remarkable feature is that all one-step transitions lead only to the nearest neighbor state. The discrete-time Birth-Death Processes are mainly used in analyzing software stability, for example, verifying if a data structure will have overflow problems.

The discrete-time Birth-Death Process can be described as a state diagram depicted in Figure 3.

In the above diagram, the states 0, 1, ..., i, ... are associated with the population. The transition probabilities b_i represents the probability of a birth when the population is i, d_i denotes the probability of a death when the population becomes i, and a_i refers to the population in the state i.

Considering 0 <= a_i <= 1 < b_i < 1 and 0 < d_i < 1 (for all i, 1 <= i <= n), the Birth-Death process described here is not a pure birth or pure death process as the population is finite. Thus, the Birth-Death process can be modeled as an aperiodic and irreducible DTMC.

In this DTMC model, the amount of population, usually considered, is greater than 1. Also, a_i, b_i, and d_i should satisfy the additivity of probability axiom. Then, the discrete-time Birth-Death process can be formalized as:

### Definition 7.12
```
|- \/ X p a b d n p_o.
DB_MODEL X p a b d n p_o =
Aperiodic_MC X p ([ 0, n ], POW [ 0, n ]) p_o (DBLt a b d) \/
Irreducible_MC X p ([ 0, n ], POW [ 0, n ]) p_o (DBLt a b d) \/
1 < n /\ (a_0 + b_0 = 1) /\
\/ j. 0 < j /\ j < n => (a_j + b_j + d_j = 1) /\
\/ j. j < n => 0 < b_j /\ b_j < 1 /\ 0 < d_j /\ d_j < 1
```

### Figure 3. State diagram of discrete-time birth-death process

![](img/0e284aa46fa831bc38a68343fef110e3_111_0.png)

In this definition, this process is formally described as an aperiodic and irreducible DTMC, in which the state space is expressed as a pair ([0, n], POW [0, n]). The set [ 0, n ] represents the population and POW [ 0, n ] is the sigma algebra of the set [ 0, n ]. Since the aperiodic and irreducible DTMC is independent of the initial distribution, the parameter p₀ in this model is a general function. The other conjunctions shown in Definition 7.12 are the requirements described in the specification of the discrete-time Birth-Death process mentioned above.

Now, it can be verified that this discrete-time Birth-Death process exhibits the limiting probabilities.

### Theorem 7.9

```
|- ∀ X p a b d n p₀.
DB_MODEL X p a b d n p₀ ⇒ (∃ u. prob p { Xt = i } → u)
```

This theorem can be verified by rewriting the goal with Definition 7.12 and then applying Theorem 7.5.

Now, we can prove that the limit probability distributions are the stationary distributions and are independent of the initial probability vector as:

### Theorem 7.10

```
|- ∀ X p a b d n p₀.
DB_MODEL X p a b d n p₀ ⇒ (∃ f. stationary_dist p X f)
```

This theorem is verified by first instantiating f to be the limiting probabilities, lim (λ t. P {X_t = i}), and then by applying Theorem 7.9.

The last two theorems verify that the Birth-Death process holds the steady-state probability vector v_i = lim P { Xt = i }. The computation of the steady-state probability vector v_i is mainly based on the following two equations:

```
v₀ = a v₀ + d v₁ (7.3a)
vᵢ = bᵢ₋₁ vᵢ₋₁ + a vᵢ + dᵢ₊₁ vᵢ₊₁ (7.3b)
```

Now, these two equations can be formally verified by the following two theorems.
