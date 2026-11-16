
The above definition can be formalized in HOL4 as follows:

```
⊢ ∀ p1 p2 X B Y. conditional_belief_vulnerability p1 p2 X B Y =
Σ y Σ b joint distribution p1 B Y (( b ) , { y }) * 1 / Γ b,y *
Σ z:T_a . belief_conditional_distribution p1 X Y B (( x ) , { y } , { b })
```

Now, we can apply the converse logarithm to get the conditional Belief Min-Entropy.

H∞ (X | Y : B) = – log ( V (X | Y : B))

Based on the previous measures, we define the information leakage that determines how much information has been leaked from the input to the output.

information leakage = initial uncertainty - remaining uncertainty

Next, we will use the definitions, presented in this section, to formally reason about their classical properties, which in turn allow us to conduct formal information flow analysis with the HOL4 theorem prover.

## 10.3 FORMAL ANALYSIS OF INFORMATION FLOW

The main focus of this chapter is on the analysis of the threat model of guessing the critical information in one try, which is usually considered as the worst case scenario and cannot be handled by the Shannon entropy as we mentioned earlier. In this section, we formally verify that the definitions, presented in the previous section, can handle this particular model.

In regards to information flow model, Min-Entropy (Mhamdi, Hasan & Tahar, 2011) allows us to measure uncertainties. The following theorem provides a lower bound to the initial uncertainty.

### Theorem 10.1

```
|- ∀ X p b. FINITE (Ω) ∧ Ω ≠ ∅ ∧ random_variable X p Borel ∧
(∀ x. x ∈ X (Ω) ∧ (distribution p X { x }) ≤ 1/2^p )) ∧
(∀ x. x ∈ Ω ⇒ (x) ∈ events p) ∧
X (Ω) ∈ subsets Borel) ⇒
b ≤ (min entropy X p)
```

where Ω = p_space P. If this initial uncertainty is uniformly distributed over the input set X, then the initial uncertainty is equal to | X |:

### Theorem 10.2

```
|- ∀ X p. FINITE (Ω) ∧
random_variable X p Borel ∧
∀ x. x ∈ X (Ω) ⇒ distribution p X { x } = 1 / | X (Ω) |
⇒ min_entropy X p = log | X (Ω) |
```

The first assumption, in the above theorems, is required because the maximum of a set is well-defined for finite sets only.

Another useful aspect related to information leakage is the remaining uncertainty that represents the model of the aposteriori behavior. If a program is deterministic and the initial distribution is uniformly distributed, then its information leakage depends on the output set only. This result can be formally verified as the following theorem:

### Theorem 10.3

```
|- ∀ X Y p c. (∀x. x ∈ X (Ω) ⇒ distribution p X { x } = 1 / |X(Ω)| ∧
Deterministic_cond Y c ⇒
Information_leakage p X Y = log ( | Y (Ω) | )
```

where the assumptions model the determinism condition and the uniform distribution. Next, we analyze the information flow considering the attacker's belief. For this purpose, we include another random variable B that models the adversary's extra knowledge about the high input. Under the condition of a total inaccurate belief, the following theorem holds:

### Theorem 10.4

```
|- ∀ B sp ev p1 p2. FINITE (p_space (sp, ev, p2)) ∧
FINITE (p_space (sp, ev, p1)) ∧
∀a b. (a, b) ∈ totally_inaccurate_belief_set sp ev p1 p2 A B ⇒
Belief_min_entropy sp ev p1 p2 A B = +∞
```

According to the above theorem, when the attacker has no information about the secret input, the initial vulnerability of the system tends to zero. The proof of this result is based on the Bayes' rule and our definition of the Belief Min-Entropy.

The following theorem verifies that the conditional Min-Entropy is always less than or equal to the Belief Min-Entropy.

### Theorem 10.5

```
|- ∀ X B sp ev p1 p2.
∀ x b. (b ∈ B (Q)) ∧
(belief_set (sp, ev, p1) (sp, ev, p2) X B b ≠ ∅) ∧
(x ∈ (belief_set (sp, ev, p1) (sp, ev, p2) X B b)) ∧
conditional_distribution (sp, ev, p1) B X (( b ), ( x )) ≤ 1 / |B(Q)| ⇒
min_entropy X (sp, ev, p1) ≤ belief_min_entropy sp ev p1 p2 X B
```

The interpretation of the previous result is that the vulnerability of a system is greater in the presence of the extra knowledge. Similarly, the following theorem provides the belief initial uncertainty in the deterministic case.

### Theorem 10.6

```
|- ∀ X B sp ev p1 p2 c.
∀ x b. x ∈ belief_set (sp, ev, p1) (sp, ev, p2) X B b ∧
b ∈ B (Q) ∧
∀ x. (x ∈ belief_set (sp, ev, p1) (sp, ev, p2) X B b) ∧
distribution (sp, ev, p1) X (x) = 1 / |X(Q)| ∧
events (sp, ev, p1) = POW (Q) ∧
deterministic_cond B c ⇒
log |X(Q)| / |B(Q)| ≤ belief_min_entropy sp ev p1 p2 X B
```

Next, just like in the case of Min-Entropy, we verify that the remaining belief uncertainty is lower bounded by conditional Min-Entropy joint to the adversary's belief, i.e. H∞(A | O, B) ≤ H∞(A | O : B), which can be expressed as the following HOL4 theorem:

### Theorem 10.7

```
|- ∀ X B Y p1 p2. FINITE (Q) ∧ random_variable X p1 Borel ∧
Random_variable B p1 Borel ∧ random_variable Y p1 Borel ∧
∀ x. x ∈ (Q) ⇒ { x } ∈ events p1
⇒ conditional_joint_min_entropy p1 X B Y ≤
Conditional_belief_min_entropy p1 p2 X B Y
```

Thus, the belief remaining uncertainty under the deterministic conditions is bounded by log (|X|/|Q|). Now we can formally verify the following result in HOL4:

### Theorem 10.8

```
|- ∀ X Y B p q c c'. FINITE Q ∧ Q ≠ {} ∧
∀ x b y. x ∈ belief_conditioned_set p q X B Y b y ∧
∀ b. b ∈ B (Q) ∧ ∀ y. y ∈ Y (Q) ∧
∀ x. x ∈ Q ⇒ { x } ∈ events p ∧
∀ x. x ∈ X (Q) ⇒ distribution p X { x } = 1 / |X(Q)| ∧
Deterministic_cond Y c ∧ deterministic_cond B c' ⇒
log |X(Q)| / |Y(Q)| / |B(Q)| ≤ conditional_belief_min_entropy p q X B Y
```

where belief_conditioned_set p q X B Y b y = Γb.y denotes the set of possible adversary's choices according to her belief and low observation.

The proof of the above theorem is primarily based on the Min-Entropy properties under deterministic conditions. Finally, Theorems 10.6 and 10.8 can be used to reason about the belief information leakage for deterministic programs.

```
log | Y | ≤ I_L(X; (Y: B)) (10.2)
```

From the above result, we conclude that the belief behavior helps the adversary in choosing more reliable initial knowledge based on the observations. The above mentioned properties have been verified before but the main novelty of our work was to re-verify these results using an interactive theorem prover. Based on the soundness of theorem proving, the formally verified theorems are guaranteed to be accurate and contain all the required assumptions. Moreover, these formally verified results can be built upon to reason about information flow analysis of various applications within the sound core of a theorem prover. For illustration purposes, the information leakage of cascade of channels is formally analyzed in the next section. These added advantages have been attained at the cost of human effort in formalizing and interactively verifying the above-mentioned results. The proof script is composed of 3400 lines of code and took about 1000 man-hours of development time.

## 10.4 APPLICATION: CHANNELS IN CASCADE

A channel is a triplet (A, B, CAB), where A is a finite set of the critical inputs, B is the observable output and CAB is the channel matrix representing the transitional probabilities from the input to the output of the channel. The channels are frequently connected in a cascade manner such that the outputs of the previous stage act as the input to the next one. In cascaded channels, the final output is produced in n steps, where n represents the number of cascaded channels.

The major goal of this section is to formally reason about the information flow of channels in cascade and analyze the information leakage in such systems. We will first formalize the notions of channels and cascade of channels in higher-order logic. These definitions, along with our formally verified results of the previous section, will then be used to formally reason about the measure of quantity of information and the information leakage of a two cascaded channel model.

### 10.4.1 Formalization of Channels and Cascade of Channels

A channel can be formalized in HOL4 using the following function:

### Definition 10.5

```
∀ X Y p f. channel p X Y f =
Random_variable X p Borel ∧
Random_variable Y p Borel ∧
∀ x y. x ∈ X (Ω) ∧
y ∈ Y (Ω) ∧
f (x, y) = conditional_distribution p Y X ({y}, { x })
```

The predicate channel accepts a probability space p, the random variables X and Y representing the finite sets of the critical inputs and the observable outputs, respectively, and a function f that models the channel matrix CAB in terms of the conditional probabilities of obtaining the output b such that the input is a.

Now the behavior of a cascade of two channels, i.e., (X, Z, CXZ) and (Z, Y, CZY), is equivalent to the channel (X, Y, CXZ * CZY). This definition of a cascade of two channels can be formalized in HOL4 as follows:
