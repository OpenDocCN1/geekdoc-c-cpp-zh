are resolved to infer:

```
¬B ∨ ¬S ∨ F
```

which is then resolved with:

```
¬F ∨ ¬G ∨ R
```

to infer:

```
¬B ∨ ¬S ∨ ¬G ∨ R
```

and so forth. For simplicity in drawing, the last resolvents are implied, rather than drawing in every single one.

Since the root of the tree is nil, this is a contradiction. By refutation, the original conclusion:

```
B ∧ S ∧ G ∧ A ∧ T → C
```

is a theorem since its negation leads to a contradiction. Thus rule (1) does logically follow from rules (2) – (5).

# 3.13 RESOLUTION AND FIRST-ORDER PREDICATE LOGIC

The resolution method is also used with the first-order predicate logic. In fact, it is the primary inference mechanism of PROLOG. However, before resolution can be applied, a wff must be put in clausal form. As an example,

> Some programmers hate all failures
> No programmer hates any success
> :. No failure is a success

Define the following predicates:

+   P(x) = x is a programmer
+   F(x) = x is a failure
+   S(x) = x is a success
+   H(x,y) = x hates y

The premisses and negated conclusion are written as:

+   (1) (∃ x) [P(x) ∧ (∀ y) (F(y) → H(x,y))]
+   (2) (∀ x) [P(x) → (∀ y) (S(y) → ¬H(x,y))]
+   (3) ¬(∀ y) (F(y) → ¬S(y))

where the conclusion has been negated in preparation for resolution.