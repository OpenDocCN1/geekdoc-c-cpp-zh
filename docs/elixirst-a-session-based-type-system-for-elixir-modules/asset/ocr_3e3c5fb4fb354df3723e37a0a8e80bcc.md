# B.3. Proofs for Theorem 4

In this section, we provide the proofs of Proposition 3 which lead to the proofs for progress of expressions (Lemma 16) and terms (Theorem 4).

**Proposition 3.** Any well-typed term $(\Delta \cdot \Gamma \vdash_S^w S \triangleright T : T < S')$ following the branching session type is able to process any valid incoming message, i.e.,

$t = \text{receive do } \{ (l_i; p_i^1, \dots, p_i^n) \rightarrow t_i \}_{i \in I} \text{ end} \qquad S = \&\{l_i(T_i^1, \dots, T_i^n).S_i\}_{i \in I} \implies \text{\textbf{match}}(p_k^j, v^j)_{j \in 1..n} \text{ is defined} \qquad \text{after}(S, ?[l_k, v^1, \dots, v^n]) = S_k \text{ for some } k \in I$

**Proof.** A well-typed term following the branching session type (\&{...}) has to be precisely a receive construct, as shown by term t. Such term can only be typed using the [rBRANCH] rule, from which we infer that

$\text{simplepat}(p_i^j, T_i^j)_{i \in I, j \in 1..n}$

The simplepat statement indicates that all of the patterns used in the branches are simple ones, i.e., $p_i^j$ has the form of a variable ($x_i^j$) or tuple of variables ($x_i^j$). From the third statement, we know that a message is valid if it matches with one of the labels available in t (i.e., $l_k$ for some $k \in I$) and each payload value ($v^1, \dots, v^n$) matches with the payload types dictated by the session type S. Therefore we can apply $x_i^j$ and $v^j$ (for all $j \in 1..n$) to the match function, to obtain a series of variable substitutions, as required.

**Lemma 16** (Progress (Expressions)). If $\emptyset \vdash_{exp} e : T$, then either $e$ is a value, or else there exists some $e'$ such that $e \rightarrow e'$

**Proof.** By induction on the typing derivation $\emptyset \vdash_{exp} e : T$. We consider the main cases.

[TTUPLE] From the rule, we know that $e = \langle e_1, \dots, e_k, \dots, e_n \rangle$ and

$\emptyset \vdash_{exp} e_i : T_i \quad \text{for all } i \in 1..n$ (B.25)

By the inductive hypothesis and eq. (B.25), expression $e_1$ can either be a value or reduce to $e'_1$. We consider both sub-cases:

+   1. If for any $i \in 1..n, e_i \rightarrow e'_i$, then case holds by [rTUPLE], resulting in the reduction $e \rightarrow \langle v_1, \dots, v_{i-1}, e'_i, \dots, e_n \rangle$.  
+   2. Otherwise, if for all $i \in 1..n, e_i = v_i$, then case holds since the tuple $\langle v_1, \dots, v_n \rangle$ is a value.

[TARITHMETIC] From the rule we know that $e = e_1 \circ e_2$ and

$\emptyset \vdash_{exp} e_1 : \text{number}$ (B.26a)  
$\emptyset \vdash_{exp} e_2 : \text{number}$ (B.26b)

By the inductive hypothesis and eq. (B.26a), $e_1$ can either be a value or reduce to $e'_1$. We consider both sub-cases:

+   1. If $e_1 \rightarrow e'_1$, then case holds by [rOPERATION_], resulting in the reduction $e \rightarrow e'_1 \circ e_2$.  
+   2. Otherwise, if $e_1 = v_1$, we have to consider the behaviour of $e_2$, which by the inductive hypothesis and eq. (B.26b) results in another two sub-cases:  
+      2a. If $e_2 \rightarrow e'_2$, then case holds by [rOPERATION_], resulting in the reduction $e \rightarrow v_1 \circ e'_2$.  
+      2b. Otherwise, if $e_2$ is a value, then case holds by [rOPERATION_].

Regarding the remaining cases: Cases [rBOOLEAN], [rCOMPARISON], [rLIST] and [rNOT] are analogous to the previous case. Finally, cases [rBASIC], [rELIST] hold immediately since $e$ in these instances is a value.

**Theorem 4** (Progress). If $\Delta \vdash \emptyset \vdash_S^w S \triangleright T : T < S'$, then either $t$ is a value, or else there exists some term $t'$ and action $\alpha$ such that $t \xrightarrow{\alpha}_T t'$ and $\text{after}(S, \alpha)$ is defined

**Proof.** By induction on the typing derivation $\Delta \vdash \emptyset \vdash_S^w S \triangleright T : T < S'$.