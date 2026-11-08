
![](img/55ff3770fcfe64effe3c90a4d4692fa6_484_0.png)

*Fig. 2. A toroidal arrangement: when one goes off the top, one comes in at the corresponding position on the bottom, and when one goes off the left, one comes in on the right.*

When one deals with finite sets a basic property that holds is the following: a function from a finite set into itself is injective if and only if the function is surjective. This property is partially true for cellular automata. In fact, an injective cellular automaton is always surjective, but the converse does not hold. When we consider finite configurations the behaviour is more analogous to finite sets. Theorem 3.9, a combination of two results proved by Moore (43) and by Myhill (44) respectively, shows exactly this fact.

**Definition 3.8.** *A pattern α is a function α : P → S, where P ⊆ ℤ^d is a finite set. Pattern α agrees with a configuration c if and only if c(x) = α(x) for all x ∈ P.*

**Theorem 3.9 (Moore (43), Myhill (44)).** *Let A be a cellular automaton. Then G_A^F is injective if and only if G_A has the property that for any given pattern α there exists a configuration c in the range of G_A^F such that α agrees with c.*

**Theorem 3.10 (Richardson (54)).** *Let A be a cellular automaton. Let G_A be its global function and G_A^F be G_A restricted to the finite configurations. Then the following implications hold:*

1. If G_A is one-to-one then G_A^F is onto.
2. If G_A^F is onto then G_A^F is one-to-one.
3. G_A^F is one-to-one if and only if G_A is onto.

**Definition 3.11.** *A cellular automaton A with global function G_A is invertible if there exists a cellular automaton B with global function G_B, such that G_B ∘ G_A = id, where id is the identity function on C.*

It is decidable whether two given cellular automata A and B are inverses of each other. This is a consequence of the effectiveness of the decomposition and the decidability of the equivalence. In 1972 Richardson proved the following important theorem about cellular automata:¹⁹

**Theorem 3.12** (Richardson (54)). *Let A be an injective cellular automaton. Then A is bijective and the inverse of G_A, G_A⁻¹, is the global function of a cellular automaton.*

The same year as Richardson’s result, Amoroso and Patt proved the following theorem:

**Theorem 3.13** (Amoroso and Patt (1)). *Let d = 1. Then there exists an algorithm that determines, given a cellular automaton A = (1, S, N, f), if A is invertible or not.*

In the same paper they also provided an algorithm in order to determine if a given cellular automaton is surjective.²⁰ In higher spaces the problem of showing if a given cellular automaton is surjective or not has been shown undecidable by Kari (34). Kari also proved that the reversibility of cellular automata is undecidable.

**Theorem 3.14** (Kari (34)). *Let d > 1. Then there is no algorithm that determines, given A = (d, S, N, f), if A is invertible or not.*

The proof of Theorem 3.14 is based on the transformation of the tiling problem shown to be undecidable by Berger (8), into the invertibility problem on a suitable class of cellular automata.

## 3.2 A new proof of the Richardson theorem based on propositional logic

Theorem 3.12 was proven using a topological argument in combination with the Garden of Eden theorem. Richardson’s proof was non-constructive (it used compactness of a certain topological space) and the new proof is formally non-constructive too (because of the use of compactness of propositional logic). One should notice that this non-constructivity is unavoidable because of the undecidability theorem proved by Kari: see Theorem 3.14. The new proof given in (14) offers a technical simplification: only basic logic is involved requiring straightforward formalism, and it allows us to apply an interpolation theorem. It is important to point out that the proof can be made fully constructive, if we consider periodic configurations; considering d = 2 the working space becomes a torus.²¹ The proof uses dimension d = 2 and the binary alphabet. This simplifies the notation but displays the idea of the proof in full generality, which works for d > 2 and extended alphabets as well. We report below the statement of Richardson’s theorem and the proof in some detail. The reader can see (14) for the complete one.

**Theorem 3.15.** *Let A be a cellular automaton over $\mathbb{Z}^2$ (with 0, 1 alphabet) whose global function $G_A$ is injective. Then there is a cellular automaton B (with 0, 1 alphabet) with global function $G_B$ such that $G_B \circ G_A = id$.*

The method given by the present author in (14) goes as follows. For an $n$-tuple of $\mathbb{Z}^2$-points $N = ((u_1, v_1), \ldots, (u_n, v_n))$ defining the neighborhood of $A$, denote by $(i,j) + N$ the $n$-tuple $(i + u_1, j + v_1), \ldots, (i + u_n, j + v_n)$. Then we define a suitable embedding into propositional logic as follows: For each $i,j$ let $p_{i,j}$ be a propositional variable. Denote by $P_{(i,j)+N}$ the $n$-tuple of variables

$$p_{i+u_1,j+v_1}, \ldots, p_{i+u_n,j+v_n}.$$

This embedding has the consequence of characterizing the transformation function of the cellular automaton as a Boolean function of $n$ variables

$$p^{t+1}_{(i,j)} = f(p^t_{(i,j)+N})$$

where the superscripts $t$ and $t + 1$ denote the discrete time. An array

$$(r_{(i,j)})_{(i,j)\in\mathbb{Z}^2}$$

(we shall skip the indices and write simply $r$) of 0 and 1 describes the configuration obtained by $G_A$ from an array

$$(p_{(i,j)})_{(i,j)\in\mathbb{Z}^2}$$

if and only if conditions

$$r_{(i,j)} = f(p_{(i,j)+N}),$$

for all $(i,j)$ are satisfied.

Denote the infinite set of all these conditions $T_A(\bar{p}, \bar{r})$.

Then the next step is to define $f$ by a CNF (or DNF) formula. In this manner we can think of $T_A(\bar{p}, \bar{r})$ as a propositional theory consisting of clauses.

A basic observation is that the injectivity of $G_A$ is equivalent to the fact that the theory

$$T(\bar{p}, \bar{q}) \cup T(\bar{q}, \bar{r})$$

(where $\bar{p}$, $\bar{q}$ and $\bar{r}$ are disjoint arrays of variables) logically implies all equivalences of the form:

$$p_{(i,j)} \equiv q_{(i,j)}$$

for all $(i,j) \in \mathbb{Z}^2$. Since the theory is unaltered if we replace all indices $(i,j)$ by $(i,j) + (i_0,j_0)$ (any fixed $(i_0,j_0) \in \mathbb{Z}^2$), this is equivalent to the fact that

$$T(\bar{p}, \bar{q}) \cup T(\bar{q}, \bar{r})$$

implies that

$$p_{(0,0)} \equiv q_{(0,0)}.$$

This can be reformulated in the following manner:

$$T(\bar{p}, \bar{r}) \cup \{p_{(0,0)}\} \cup T(\bar{q}, \bar{r}) \cup \{\neg q_{(0,0)}\}$$

is unsatisfiable.

By applying the compactness theorem for propositional logic, we deduce that there are finite theories

$$T_0(\bar{p}, \bar{r}) \subseteq T(\bar{p}, \bar{r})$$

and

$$T_0(\bar{q}, \bar{r}) \subseteq T(\bar{q}, \bar{r})$$

such that

$$T_0(\vec{p},\vec{r}) \cup \{p_{(0,0)}\} \cup T_0(\vec{q},\vec{r}) \cup \{\neg q_{(0,0)}\}$$

is unsatisfiable. At this point in the proof we can use the Craig interpolation theorem. This result guarantees the existence of a formula $I(\vec{r})$, such that:

$$T_0(\vec{p},\vec{r}) + p_{(0,0)} \vdash I(\vec{r})$$

and

$$I(\vec{r}) \vdash T_0(\vec{q},\vec{r}) \to q_{(0,0)}.$$

Although we write the whole array $\vec{r}$ in $I(\vec{r})$, the formula obviously contains only finitely many $r$ variables.

Thus by application of the deduction theorem we have that:

$$T_0(\vec{p},\vec{r}) \vdash p_{(0,0)} \to I(\vec{r})$$

and

$$T_0(\vec{q},\vec{r}) \vdash I(\vec{r}) \to q_{(0,0)}.$$

Then after suitably renaming the propositional variables we see that the second implication gives:

$$T_0(\vec{p},\vec{r}) \vdash I(\vec{r}) \to p_{(0,0)}$$

i.e. together

$$T_0(\vec{p},\vec{r}) \vdash I(\vec{r}) \equiv p_{(0,0)}.$$

The interpolant $I(\vec{r})$ computes the symbol of cell $(0,0)$ in the configuration prior to $\vec{r}$. This defines the inverse of $A$. Let $M \subseteq \mathbb{Z}^2$ be the finite set of $(s,t) \in \mathbb{Z}^2$ such that $r_{(s,t)}$ appears in $I(\vec{r})$. Finally define the inverse cellular automaton $B$ as follows:

1. Alphabet is 0, 1;
2. The neighborhood is $M$;
3. The transition function is given by $I(\vec{r})$.

This concludes the proof.

We conclude this part about the Richardson theorem with a few remarks about the proof sketched above.

1. The construction of the inverse cellular automaton carried out in the proof given in (14) has two key moments. First the application of the compactness theorem after a suitable embedding into propositional logic. In a second moment the interpolation theorem is applied leading to some kind of effectiveness. Of course, the application of compactness leads to a non-recursive procedure but as we previously noticed this fact is unavoidable because of Theorem 3.14.

2. The construction guarantees that

$$G_B(G_A(\vec{p})) = \vec{p}$$

but it does not — a priori — imply that also

$$G_A(G_B(\vec{r})) = \vec{r}.$$
