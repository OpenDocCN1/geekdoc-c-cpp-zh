Similarly, the other arithmetic operations have also been defined for extended reals and their corresponding operators can be overloaded in HOL4 as follows:

```
val _ = overload_on ("--", Term `external_sub `);
val _ = overload_on ("**", Term `external_mul `);
val _ = overload_on ("//", Term `external_div `);
val _ = overload_on ("<=", Term `external_le `);
val _ = overload_on ("<<", Term `external_lt `);
val _ = overload_on ("^~", Term `external_ainv `);
val _ = overload_on ("numeric_negate", Term `external_ainv `);
val _ = overload_on ("inv", Term `external_inv `);
val _ = overload_on ("abs", Term `external_abs `);
val _ = overload_on ("logr", Term `external_logr `);
val _ = overload_on ("lg", Term `external_lg `);
val _ = overload_on ("exp", Term `external_exp `);
val _ = overload_on ("pow", Term `external_pow `);
val _ = overload_on ("sqrt", Term `external_sqrt `);
```

The order relation, for example, is extended as: \(\forall a \in \mathbb{R}^+, -\infty \le a \le +\infty\).

# Definition 4.2

```
|- ∀ x y. extreal_le (Normal x) (Normal y) = (x ≤ y) ∧
 extreal_le NegInf a = T ∧
 extreal_le b PosInf = T ∧
 extreal_le e NegInf = F ∧
 extreal_le PosInf d = F
```

With the order shown in Definition 4.2, R' is a complete lattice where every subset has a supremum and an infimum.

# 4.1.2 Supremum and Infimum

The supremum or least upper bound of a set \(s \subseteq R'\) is the least element of \(R'\) that is greater than or equal to every element of \(s\). The supremum can be defined in HOL4 as:

# Definition 4.3

```
|- ∀p. extreal_sup p =
 if Vx. (∀y. p y ⇒ y ≤ x) ⇒ (x = PosInf) then PosInf
 else (if ∀x. p x ⇒ (x = NegInf) then NegInf
 else Normal (sup (∀r. p (Normal r))))
```