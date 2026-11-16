# Definition 10.6

```
⊢ ∀ p X Z Y p f g. cascade_channel p X Z Y f g =
    channel p Z Z f ∧
    channel p Z Y g ∧
    ∀ x y. joint_distribution p X Y ({x }, {y }) =
        ∑ x joint_distribution p X Z ({x }, { z }) *
            conditional_distribution p Y Z ({y }, { z })
```

# 10.4.2 Information Flow Analysis of Channels in Cascade

In order to analyze the information flow for the worst case scenario, i.e., when A recovers the critical information in one guess, we model the apriori distribution as a function of the maximum input distribution and the aposteriori behavior is expressed as a function of the maximum over X of the distribution of guessing a while observing b.

```
leakage = Min-Entropy (X) - conditional Min-Entropy (X | Y)
```

```
IL∞ (X, Y) = H∞ (X) - ∞ (X | Y) (10.3)
```

Now, the leakage in a cascade of channels can be evaluated using Min-Entropy and the corresponding proof goal can be expressed in HOL4 as follows:

# Theorem 10.9

Let (X, Y, CX) be the cascade of (X, Z, CXZ) and (Z, Y, CYZ). Then we have IL∞ (X, Y) ≤ IL∞ (X, Z)

This theorem can be expressed in HOL4 as

```
⊢ ∀ p X Z Y f g.
    cascade_channel p X Z Y f g ∧
    FINITE (Q) ∧
    Q ≠ ∅ ∧
    events p = POW (Q) ∧
    ∀ x. 0 < distribution p Y ({ x }) ∧
    ∀ x. 0 < distribution p Z ({ x }) ∧
    (∀ x. x ∈ Q ⇒ ({ x } ∈ events p) ∧
    Information_leakage p X Y ≤ information_leakage p X Z
```