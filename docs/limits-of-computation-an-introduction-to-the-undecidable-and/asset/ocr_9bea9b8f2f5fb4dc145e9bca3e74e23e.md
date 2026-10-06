# 6 Limits of Computation

# Example

{a, b} \times {c, d} = \{(a, c), (a, d), (b, c), (b, d)\}

{1, 2, 3} \times {1, 2} = \{(1, 1), (1, 2), (2, 1), (2, 2), (3, 1), (3, 2)\}

{a, b, c} \times \varnothing = \varnothing

# 1.2 FUNCTIONS

Again, functions are a concept quite familiar to computer science.

# Definition 1.14

A **function** or **mapping** from set A to set B (written $f: A \to B$) is a subset of $A \times B$ such that each $x \in A$ is associated with a *unique* $y \in B$.

For $f: A \to B$:

+   * A is called the **domain** of $f$.
* B is called the **codomain** of $f$.

+   If $f(x) = y$:
* $y$ is called the **image** of $x$ under $y$
* $x$ is the **preimage** of $y$ under $f$.

Thus, the mapping from a person to his or her mother is a function (assuming exactly one mother per person), but the mapping from a person to his her child is not. The mapping (person x, mother of X) has a domain of all people—every person has a mother, and a codomain of the set of women who have children.

# Definition 1.15

A function $f$ from a set A to set B is an **injection** if no two values from A are mapped to the same element of $B$ ($f(x) = f(y)$ implies $x = y$). It is a **surjection** if it is onto $B$ (for every $b \in B$, there is an $x \in A$ such that $f(x) = b$). It is a **bijection** or **one-to-one correspondence** if it is both an injection and a surjection (one-to-one and onto).