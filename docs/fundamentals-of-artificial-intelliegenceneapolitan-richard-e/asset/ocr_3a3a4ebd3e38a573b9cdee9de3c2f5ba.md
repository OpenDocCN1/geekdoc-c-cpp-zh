```
Procedure Conjunctive_Normal_form(var Proposition);
remove all "↔" symbols using the if and only if elimination law;
remove all "→" symbols using the implication elimination law;
repeat
    if there are any double negations
        remove them using the double negation law;
    if there are any negations of non-atomic propositions
        remove them using DeMorgan's laws;
until the only negations are single negations of atomic propositions;
repeat
    if there are any disjunctions in which one or more terms is a conjunction
        remove them using these laws:
    A ∨ (B ∧ C) ≡ (A ∨ B) ∧ (A ∨ C)   (2.1)
    (A ∧ B) ∨ C ≡ (A ∨ C) ∧ (B ∨ C);   (2.2)
until Proposition is in conjunctive normal form;
```

Equivalence 2.1 is the Distributivity law in Table 2.1 and Equivalence 2.2 can be derived from the Commutivity and Distributivity laws.

# Example 2.22 We use Algorithm 2.1 to convert ¬((P ⇒ Q) ∧ ¬R) to conjunctive normal form:

+   ¬((P ⇒ Q) ∧ ¬R) ≡ ¬((¬P ∨ Q) ∧ ¬R) implication elimination
+   ≡ ¬(¬P ∨ Q) ∨ ¬¬R DeMorgan's laws
+   ≡ ¬(¬P ∨ Q) ∨ R double negation
+   ≡ (¬¬P ∧ ¬Q) ∨ R DeMorgan's laws
+   ≡ (P ∧ ¬Q) ∨ R double negation
+   ≡ (P ∨ R) ∧ (¬Q ∨ R) Equiv. 2.2

# Example 2.23 We use Algorithm 2.1 to convert (P ∧ Q) ∨ (R ∧ S) to conjunctive normal form:

+   (P ∧ Q) ∨ (R ∧ S) ≡ ((P ∧ Q) ∨ R) ∧ ((P ∧ Q) ∨ S) Equiv. 2.1
+   ≡ (P ∨ R) ∧ (Q ∨ R) ∧ ((P ∧ Q) ∨ S) Equiv. 2.2
+   ≡ (P ∨ R) ∧ (Q ∨ R) ∧ (P ∨ S) ∧ (Q ∨ S) Equiv. 2.2