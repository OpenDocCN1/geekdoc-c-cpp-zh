# **Theorem 10.1**

```
|- ∀ X p b. FINITE (Ω) ∧ Ω ≠ ∅ ∧ random variable X p Borel ∧
(∀ x. x ∈ X (Ω) ∧ (distribution p X { x }) ≤ 1/2^p )) ∧
(∀ x. x ∈ Ω ⇒ ( x }∈ events p) ∧
X (Ω) ∈ subsets Borel) ⇒
b ≤ (min entropy X p)
```

where Ω = p\_space P. If this initial uncertainty is uniformly distributed over the input set X, then the initial uncertainty is equal to | X |:

# **Theorem 10.2**

```
|- ∀ X p. FINITE (Ω) ∧
random\_variable X p Borel ∧
∀ x. x ∈ X (Ω) ⇒ distribution p X { x } = 1 / | X (Ω) |
⇒ min\_entropy X p = log | X (Ω) |
```

The first assumption, in the above theorems, is required because the maximum of a set is well-defined for finite sets only.

Another useful aspect related to information leakage is the remaining uncertainty that represents the model of the aposteriori behavior. If a program is deterministic and the initial distribution is uniformly distributed, then its information leakage depends on the output set only. This result can be formally verified as the following theorem:

# **Theorem 10.3**

```
|- ∀ X Y p c. (∀x. x ∈ X (Ω) ⇒ distribution p X { x } = 1 / |X(Ω)| ∧
Deterministic\_cond Y c ⇒
Information\_leakage p X Y = log ( | Y (Ω) | )
```

where the assumptions model the determinism condition and the uniform distribution. Next, we analyze the information flow considering the attacker's belief. For this purpose, we include another random variable B that models the adversary's extra knowledge about the high input. Under the condition of a total inaccurate belief, the following theorem holds:

# **Theorem 10.4**

```
|- ∀ B sp ev p1 p2. FINITE (p\_space (sp, ev, p2)) ∧
FINITE (p\_space (sp, ev, p1)) ∧
∀a b. (a, b) ∈ totally\_inaccurate\_belief\_set sp ev p1 p2 A B ⇒
Belief\_min\_entropy sp ev p1 p2 A B = +∞
```