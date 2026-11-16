| A | B | A => B | A ^ (A => B) | A ^ (A => B) => B |
|---|---|---|---|---|
| T | T | T | T | T |
| T | F | F | F | T |
| F | T | T | F | T |
| F | F | T | F | T |

Because A ^ (A => B) => B is true in all possible worlds, A ^ (A => B) => B.

# Definition 2.4 Given two propositions A and B, if A <=> B is a tautology, we say that A and B are logically equivalent and we write A == B.

# Example 2.11 The following truth table shows that A => B <=> -A v B:

| A | B | -A | A => B | -A v B | A => B <=> -A v B |
|---|---|---|---|---|---|
| T | T | F | T | T | T |
| T | F | F | F | F | T |
| F | T | T | T | T | T |
| F | F | T | T | T | T |

Because A => B <=> -A v B is a tautology, A => B <=> -A v B.

Notice in the previous example that A => B and -A v B have the same truth value in every possible world. This is a general result concerning logical equivalence, which we state in the following theorem.

# Theorem 2.1 A <=> B if and only if A and B have the same truth value in every possible world.

Proof. The proof is left as an exercise.

Table 2.1 shows some important logical equivalences, called laws. It is left as an exercise to establish them using truth tables. We can often simplify a logical expression using these laws due to the following theorem:

# Theorem 2.2 Suppose we have a proposition A and a sub-proposition B within A. If in A we replace B by any proposition logically equivalent to B, we will obtain a proposition logically equivalent to A.

Proof. The proof is left as an exercise.

# Example 2.12 Suppose we have the following proposition:

¬¬P ∧ (Q ∨ ¬Q)

We can simplify it is follows:

¬¬P ∧ (Q ∨ ¬Q) ≡ P ∧ (Q ∨ ¬Q) due to the double negation law
≡ P ∧ True due to the excluded middle law
≡ P due to the identity laws.