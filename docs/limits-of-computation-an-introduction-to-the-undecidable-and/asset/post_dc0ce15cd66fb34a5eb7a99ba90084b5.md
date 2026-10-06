
## Limits of Computation

### 9.2.1 Restriction (Also Called Generalization)

X is a special case of Y, and so every yes or no instance of X is already a yes or no instance of Y. No modifications are necessary. Thus, an identity mapping takes a instance of X to a instance of Y, and takes a no instance of X to a no instance of Y.

We have seen examples of generalization earlier: every third degree polynomial is also a fourth degree polynomial (though not versa). So, if we took X to the language p(x): p is a polynomial of degree $\le$ 3 with an integer root for some integer n, and Y is the generalization of X to include fourth degree polynomials, then a yes or no instance of X is, without modification, or a no instance of Y.

$X = \{p(x): p \text{ is polynomial, degree } \le 3, p(n) = 0 \text{ for some n \}$
$X = \{x^3 + 8, x - 5, x^2 - x - 6, \dots \} \text{(yes instances)}$

$\overline{X} = \{x^2 + 1, x^4 - 16, \dots \} \text{\ (no instances)}$

$Y = \{p(x): p \text{ is polynomial, degree } \le 4, p(n) = 0 \text{ for some n \}$
$Y = \{x^3 + 8, x - 5, x^2 - x - 6, x^4 - 16 \dots \} \text{\ (yes instances)}$

$Y = \{x^2 + 1, \dots \} \text{\ (no instances)}$

Boolean expressions in conjunctive normal form are certainly Boolean expressions, so CNF Boolean expressions are special cases of general Boolean expressions, and GEN-SAT is a generalization of CNF-SAT.

## Theorem 9.1

GEN-SAT (or general first-order Boolean expression satisfiability) is NP-complete.

## Proof

An instance of GEN-SAT is a Boolean expression in variables $x_i, \dots, x_n$, using all the standard connectors $(\neg, \wedge, \vee, \to, =)$, not in any particular form. Again, the certificate is an assignment of truth values to the $x_i, \dots, x_n$ variables, and therefore it is easy to show (so do it!) that this certificate can be used to verify a instance in time bounded polynomially in the length of the expression [E].

Now an expression in conjunctive normal form is certainly a Boolean expression, so that

CNF-SAT $\le_p$ GEN-SAT

This is a proof by generalization—or what Garey and Johnson call restriction. GEN-SAT is a more general case of CNF-SAT, so the polynomial transformation is very easy.

**Note:** Many texts use the abbreviation SAT for conjunctive normal form satisfiability. This is tempting since it is probably the most used NP-complete problem. In this text, the simple term SAT is not used, so that is clear (if any) conditions are placed on the Boolean expressions.

### 9.2.2 Local Replacement

In a proof of this kind, one takes reasonably subparts of the known NP-complete problem, and transforms each subpar into a piece of the new problem. The term *gadget* is often used for the pieces constructed by this transformation.

## Theorem 9.2

3-CNF-SAT (Boolean satisfiability in which each clause in conjunctive normal form has three terms, not necessarily distinct) is **NP-complete**.

## Proof

Using local replacement we can take each clause of a yes or no instance in CNF-SAT, and transform that clause into a group of clauses, each of which has three terms. The original set of clauses is satisfiable if and only if the transformed set of clauses is also satisfiable.

The conversion will depend on the length of k to be converted. For $\le 3$, the method is straightforward.

If k = 1, repeat the term three times; so $(x_i)$ becomes $(x_i \lor x_i \lor x_i)$.

If k = 2, duplicate the second term: so $(x_i \lor \neg x_j)$ becomes $(x_i \lor \neg x_j \lor x_k)$.
If k = 3, no change is needed, as the clause is already in 3-CNF.

If k > 3, the original clause will be of the form $x_{j1}, \dots, x_{jk}$ (where any of the terms might be the negation with $\neg$). The transformation of this clause requires the creation of $r = (k - 3)$ new variables $y_1, \dots, y_r$. The idea is to "pull apart" the original clause into multiple clauses bridged by the $y_i$'s and their negations as follows:

- $(x_{ij} \lor x_{j2} \lor y_1)$ First two terms of the clause
- $(\neg y_1 \lor x_{j3} \lor y_2)$ Third term of the clause
- $(\neg y_2 \lor x_{j4} \lor y_3)$ Fourth term of the clause
- ...
- $(\neg y_r \lor x_{j(k-1)} \lor x_{jk})$ Final two terms of the clause

For example, the clause, $(x_3 \lor \neg x_2 \lor x_1 \lor \neg x_3 \lor \neg x_i)$ becomes:

- $(x_3 \lor \neg x_2 \lor y_1)$
- $(\neg y_1 \lor x_1 \lor y_2)$
- $(\neg y_2 \lor x_1 \lor y_3)$
- $(\neg y_3 \lor x_3 \lor \neg x_i)$

**YES TO YES**

For clauses of length $k \le 3$, the true term that appears in the old clause also appears in the new clause, so the new clause is still true.
For clauses of length $k > 3$, we have a whole new set of clauses, and they must all be true. At least one of $x_{ij}$ from the original clause was true. There will be a way to choose true values for $y_i$, so that the new clauses are true:

- If $x_{ij}$ or $x_j$ was true: Set $y_i$ to false. Set all of the other $y_j$ to true. (Wait, the logic in OCR seems garbled here, but preserving the text's intent structure).
- If $x_{j(k-1)}$ or $x_{jk}$ was true: Set $y_r$ to true. Set all of the other $y_i$ to false.

**NO GOES TO NO (OR, EQUIVALENTLY, COMES FROM YES)**

As is often the case, it will be easier to prove the contrapositive; that is, a yes instance of the transformed clauses must come from a yes instance of the original clause (Remember this, as it will occur often). So, suppose that each of the clauses on the right is satisfiable with some assignment of true values to $y_{i1}, \dots, y_{ik}$ and $y_j, \dots, y_l$. For clauses of length to three, the new clause is nearly identical to the old: if one is true, so is the other. For clauses containing $y_i, \dots, y_p$, the key is that the set of clauses cannot be made just by choosing variables and their negations are threaded through the new clauses.

### 9.2.3 Component Design

Sometimes there is no way to take local properties of one decision problem and make changes to each of them to arrive at a valid transformation that $X \le_p Y$. If this cannot be done, the whole structure of X must be considered. The problem Y may be constructed out of parts of X, with changes, reorganizations, or deletions. This often takes considerable ingenuity, and leads to long, hard-to-read proofs. One proof by component design may look nothing like another; knowing how to do one may be no help in others.

We actually saw a component design transformation in the Cook-Levin theorem. Here, moves and paths in a nondeterministic Turing machine (NDTM) were transformed into Boolean expressions. States, moves, configurations, and the accepting condition become expressed in a large set of nontrivial clauses. Other examples of component design will be somewhat shorter. No other proof will require an entire chapter, although some of them can be complicated. Note that 3-CNF-SAT is more restrictive than CNF-SAT, so that we could use the identity mapping to show that

3-CNF-SAT $\le_p$ CNF-SAT

This says nothing about the NP-hardness of 3-CNF-SAT, though it would prove that 3-CNF-SAT is in NP.

## Theorem 9.3

3-DISTINCT-CNF-SAT (Boolean expressions in CNF in which each clause has three distinct terms) is NP-complete.

## Proof

Exercise.

## 9.3 GRAPH PROBLEMS

So far, we have discussed only problems involving Boolean expressions. These form a large group of important decision problems, but there are many other kinds of problems. Some of the most interesting problems come from graph theory, for example, the classic traveling salesman (woman!) wants to visit $n$ cities, wanting the least distance possible, while making the circuit. However, as noted before, as the Traveling Salesman Problem (TSP) is not a decision problem—but it has a closely related version that is a decision problem.

The first graph problem is not as intuitive or as easy to state as TSP—like other NP-complete graph problems—will require some definitions that you have not met before, but which are not difficult.

Graphs can be undirected or directed, as shown in Figure 9.1.

In this book, unless otherwise specified, a graph denotes an undirected graph. Graphs consist of nodes or vertices $v_1, \dots, v_n$ and edges $\{v_i, v_j\}$ or, for directed graphs, directed edges or “arrows” $(v_i, v_j)$. We will write $G = (V, E)$; that is, G is composed of a set $V$ of vertices $v_1, \dots, v_n$, $|V|=n$, and a set of edges $E$, $|E| \le n^2$. We write directed graphs as $G = (V, A)$ with arrows instead of edges.

Graphs may also be weighted, in which case there is some positive number (weight) associated with each edge. Weighted graphs are often undirected complete graphs. A graph G is complete if there are edges between all pairs of vertices.
