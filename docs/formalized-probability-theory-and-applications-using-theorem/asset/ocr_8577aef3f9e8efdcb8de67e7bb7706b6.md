Finally, we show that the above mentioned two results are also valuable for the given application for border surveillance through a simple instantiation of the input parameter q by its value. The corresponding HOL4 analysis is given in the following 2 lemmas.

# Lemma 14.15

```
|- ∀ p m s L Ts. (0 < s < 1) ∧ (0 < L) ∧ (0 < Ts) ∧ (∀k. L < & (SUC k) × Ts)
⇒ lim (k→∞) (∀x. Pd_surv p (k × m) k s L Ts (0.28)) =
1 - (1 - s) × e ^ (-⌊L / Ts⌋) × (0.28) × m - s × e ^ (-⌊(L + 1) / Ts⌋) × (0.28) × m.
```

# Lemma 14.16

```
|- ∀ p s L Ts. (0 < s < 1) ∧ (0 < L) ∧ (0 < Ts) ∧ (∀k. L < & (SUC k) × Ts)
⇒ lim (m→∞) (∀m. lim (k→∞) (∀x. Pd_surv p (k × m) k s L Ts (0.28))) = 1.
```

Unlike traditional analysis techniques for the validation of a WSN for border surveillance, using the k-set randomized scheduling algorithm, our approach is much more efficient. Indeed, while paper-and-pencil based analysis or simulation cannot guarantee the correctness of the scheduling performance results, the reported theorems in this chapter are absolutely accurate. This distinguishing feature is due to the inherent soundness of theorem proving and its generic nature, e.g., the detection probability for any given values of n and k can be computed by instantiating Theorem 14.2 with appropriate values. Contrarily, simulation is usually restricted to specific network configurations, while probabilistic model checking is frequently using parameter abstraction in order to cope with the state-space explosion problem (Pruth, 2006). Moreover, for each of the formally verified theorems, the set of required assumptions is clearly stated so there is no doubt about missing a critical assumption. This can never be ensured in simulation and model checking where many assumptions can be taken into account without explicitly mentioning them.

In this work, we provided a completely rigorous method for the performance evaluation of the randomized scheduling algorithm for WSNs through theorem proving. Indeed, the probabilistic feature of the randomized nodes scheduling algorithm makes its analysis challenging for all possible cases. Since the assignment of the sensor nodes to the k sub-networks is randomly done, it may happen that some of the sub-networks are empty. Moreover, due to the random deployment of nodes, the random scheduling can lead to a situation where certain parts of the area