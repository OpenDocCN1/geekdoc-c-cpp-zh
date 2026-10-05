558

Chap. 17 Limits to Computation

**Example 17.2** In this example, we make use of a simple conversion between two graph problems.

**Theorem 17.2** VERTEX COVER is in $NP$-complete.

**Proof:** *Prove that VERTEX COVER is in $NP$.* Simply guess a subset of the graph and determine in polynomial time whether that subset is fact in a vertex cover of size $k$ or less.

*Prove that VERTEX COVER is $NP$-hard.* We will assume that K-CLIQUE is already known to be $NP$-complete. (We will see this proof in the next example. For now, just accept that it is true.)

Given that K-CLIQUE is $NP$-complete, we need to find a polynomial-time transformation from the input to K-CLIQUE to the input to VERTEX COVER, and another polynomial-time transformation from the output for VERTEX COVER to the output for K-CLIQUE. This turns out to be a simple matter, given a graph $G$ and a vertex $S$ on $G$. Denote by $S'$ the set of vertices in $G$ but not in $S$. There can be no edge connecting any vertices in $S'$ because, if the inverse, $S$ would not be a vertex cover. Denote by $G'$ the inverse of $G$, the graph formed from the edges not in $G$. If $S$ is of size $k$, then $S'$ forms a clique of size $n-k$ in graph $G'$. Then we can reduce K-CLIQUE to VERTEX COVER by simply converting $G$ to $G'$, and asking if $G'$ has a VERTEX COVER of size $n-k$ or smaller. If YES, then there is a clique in $G$ of size $k$; if NO there is not. $\square$

**Example 17.3** So far, our $NP$-completeness proofs have involved transformations between inputs of the same "type", such as a Boolean expression or from a graph to a graph. Sometimes $NP$-completeness proves a transformation between types of inputs, as shown next.

**Proof:** K-CLIQUE is in $NP$, because we can just guess a clique of $k$ vertices and test in polynomial time if it is a clique. We show that K-CLIQUE is $NP$-hard by using a reduction from SAT. An instance of SAT is a Boolean expression

```
$B = C_1 \cdot C_2 \cdot \dots \cdot C_m$
```

whose clauses we will describe by the notation

$C_i = y[i, 1] + y[i, 2] + \dots + y[i, k_i]$