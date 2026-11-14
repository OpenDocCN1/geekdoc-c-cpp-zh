
### [TCASE]

From the rule, we know that for some type U,

t = case e do (p_i -> t_i)_{i \in I} (x_{nil} -> t_{all}) end \quad (B.23a)
\Delta \cdot (x_{nil} : U) \vdash^w S > t_{all} : T < S' \quad (B.23b)
\emptyset \vdash_{exp} e : U \quad (B.23c)
\vdash^w_{par} p_i : U > \Gamma'_i \quad \text{for all } i \in I \quad (B.23d)
\Delta \cdot \Gamma''_i \vdash^w S > T_i : T < S' \quad \text{for all } i \in I \quad (B.23e)

By eq. (B.23a), term reduction, t \mapsto t', can be derived using two rules, so we consider two sub-cases:

- 1. [RCASE_1] From the rule, we know that t' = case e' do (p_i -> t_i)_{i \in I} (x_{nil} -> t_{all}) end. From the premise we know that

e \to e' \quad (B.23f)

By eqs. (B.23c) and (B.23f) and the Preservation (Expressions) Lemma, we get

\emptyset \vdash_{exp} e' : U \quad (B.23g)

Using eqs. (B.23b), (B.23d), (B.23e), (B.23g), and [TCASE], we get

\Delta \cdot \vdash^w S > case e' do (p_i -> t_i)_{i \in I} (x_{nil} -> t_{all}) end : T < S'

which holds as expected given after(S, \tau) = S and after(\Delta, S) = \Delta.

- 2. [RCASE_2] From the rule, we know that t = case v do (p_i -> t_i)_{i \in I} (x_{nil} -> t_{all}) end and e = v. For convenience, we include the catch-all pattern in t with the remaining patterns, so t = case v do (p_i -> t_i)_{i \in I} end. So, for some j \in I',

\text{match}(p_j, v) = \sigma \text{ where } \sigma = [\tau :: \dots \backslash v_k / \dots \backslash \kappa] \quad (B.23h)

t' = t_j \sigma \quad (B.23i)

By eqs. (B.24c), (B.23d) and (B.23h) and Lemma 13, we know that \Gamma''_j = x_1 : T_1, \dots, x_n : T_n and

\emptyset \vdash_{exp} v_k : T_k \text{ for all } k 1..n \quad (B.23j)

Then, by repeatedly applying the Substitution Lemma to eq. (B.23j), (B.23e for i = j), we get

\Delta \cdot \vdash^w S > \sigma : T < S'

This holds since after(S, \tau) = S and after(\Delta, S) = \Delta. \square

### [TEXPRESSION]

From the rule, we know that

t = e \quad (B.24a)

\emptyset \vdash_{exp} e : T \quad (B.24b)

From the structure of t (eq. (B.24a)), term transition (t \mapsto t') can only be derived using [RExpression], resulting in an internal transition (i.e., \alpha = \tau)

e \to e' \quad (B.24c)

By Lemma 15 and eqs. (B.24b) and (B.24c), we know that

\emptyset \vdash_{exp} e' : T \quad (B.24d)

Thus, case holds since [RExpression] and eq. (B.24d).

## B.3. Proofs for Theorem 4

In this section, we provide the proofs of Proposition 3 which lead to the proofs for progress of expressions (Lemma 16) and terms (Theorem 4).

### Proposition 3.

Any well-typed term $(\Delta \cdot \Gamma \vdash_S^w S \triangleright T : T < S')$ following the branching session type is able to process any valid incoming message, i.e.,

$t = \text{receive do } \{ (l_i; p_i^1, \dots, p_i^n) \rightarrow t_i \}_{i \in I} \text{ end} \qquad S = \&\{l_i(T_i^1, \dots, T_i^n).S_i\}_{i \in I} \implies \text{\textbf{match}}(p_k^j, v^j)_{j \in 1..n} \text{ is defined} \qquad \text{after}(S, ?[l_k, v^1, \dots, v^n]) = S_k \text{ for some } k \in I$

**Proof.** A well-typed term following the branching session type (\&{...}) has to be precisely a receive construct, as shown by term t. Such term can only be typed using the [rBRANCH] rule, from which we infer that

$\text{simplepat}(p_i^j, T_i^j)_{i \in I, j \in 1..n}$

The simplepat statement indicates that all of the patterns used in the branches are simple ones, i.e., $p_i^j$ has the form of a variable ($x_i^j$) or tuple of variables ($x_i^j$). From the third statement, we know that a message is valid if it matches with one of the labels available in t (i.e., $l_k$ for some $k \in I$) and each payload value ($v^1, \dots, v^n$) matches with the payload types dictated by the session type S. Therefore we can apply $x_i^j$ and $v^j$ (for all $j \in 1..n$) to the match function, to obtain a series of variable substitutions, as required.

### Lemma 16 (Progress (Expressions)).

If $\emptyset \vdash_{exp} e : T$, then either $e$ is a value, or else there exists some $e'$ such that $e \rightarrow e'$

**Proof.** By induction on the typing derivation $\emptyset \vdash_{exp} e : T$. We consider the main cases.

### [TTUPLE]

From the rule, we know that $e = \langle e_1, \dots, e_k, \dots, e_n \rangle$ and

$\emptyset \vdash_{exp} e_i : T_i \quad \text{for all } i \in 1..n$ (B.25)

By the inductive hypothesis and eq. (B.25), expression $e_1$ can either be a value or reduce to $e'_1$. We consider both sub-cases:

- 1. If for any $i \in 1..n, e_i \rightarrow e'_i$, then case holds by [rTUPLE], resulting in the reduction $e \rightarrow \langle v_1, \dots, v_{i-1}, e'_i, \dots, e_n \rangle$.
- 2. Otherwise, if for all $i \in 1..n, e_i = v_i$, then case holds since the tuple $\langle v_1, \dots, v_n \rangle$ is a value.

### [TARITHMETIC]

From the rule we know that $e = e_1 \circ e_2$ and

$\emptyset \vdash_{exp} e_1 : \text{number}$ (B.26a)
$\emptyset \vdash_{exp} e_2 : \text{number}$ (B.26b)

By the inductive hypothesis and eq. (B.26a), $e_1$ can either be a value or reduce to $e'_1$. We consider both sub-cases:

- 1. If $e_1 \rightarrow e'_1$, then case holds by [rOPERATION_], resulting in the reduction $e \rightarrow e'_1 \circ e_2$.
- 2. Otherwise, if $e_1 = v_1$, we have to consider the behaviour of $e_2$, which by the inductive hypothesis and eq. (B.26b) results in another two sub-cases:
  - 2a. If $e_2 \rightarrow e'_2$, then case holds by [rOPERATION_], resulting in the reduction $e \rightarrow v_1 \circ e'_2$.
  - 2b. Otherwise, if $e_2$ is a value, then case holds by [rOPERATION_].

Regarding the remaining cases: Cases [rBOOLEAN], [rCOMPARISON], [rLIST] and [rNOT] are analogous to the previous case. Finally, cases [rBASIC], [rELIST] hold immediately since $e$ in these instances is a value.

### Theorem 4 (Progress).

If $\Delta \vdash \emptyset \vdash_S^w S \triangleright T : T < S'$, then either $t$ is a value, or else there exists some term $t'$ and action $\alpha$ such that $t \xrightarrow{\alpha}_T t'$ and $\text{after}(S, \alpha)$ is defined

**Proof.** By induction on the typing derivation $\Delta \vdash \emptyset \vdash_S^w S \triangleright T : T < S'$.

### [TLET]

From the rule, we know that t = (x = t_1; t_2), and

\(\Delta \cdot \emptyset \vdash^w S > t_1 : T' > S''\) (B.27)

By the inductive hypothesis and eq. (B.27), we know that **after**(S, \(\sigma\)) is defined and that the term t_1 can be a value, or else transition to a new term t'_1. We consider both sub-cases:

- 1. If t_1 \Rightarrow t'_1, then case holds by [rLET], resulting in t \Rightarrow t'_1; t_2.
- 2. Otherwise, if t_1 = v_1, then case holds by [rLETv], resulting in the internal transition t \xrightarrow{\tau} t_2 [v_1/x].

In both cases, **after**(S, \(\sigma\)) remains defined from the inductive hypothesis.

### [TBRANCH]

From the rule, we know that

t = receive do (\{1 \downarrow_i \vec{p}_i\} \rightarrow t_i)_{i \in I} end (B.28)
S = &\{1(\vec{T}_i).S_i\}_{i \in I} (B.29)

A receive term (eq. (B.28)) transitions to a new subterm (t_i) when a message (\sigma = ?\{1, v_1, ..., v_n\}) is received. An incoming message is guaranteed to match with one of the available patterns, since (i) we are dealing with a trusted observer which sends valid actions, and (ii) the branches are restricted to simple patterns (using simplepat) so a well structured message will match with one of the branches. An incoming message is matched to a branch using its label :1_j (for j \in I). So by [rBRANCH], we know that t \xrightarrow{?\{1_j, v_1, ..., v_n\}} t_j \sigma, where \sigma is computed using the Pattern Matching Definition (i.e., \sigma = match(\vec{p}_j, v_1, ..., v_n)). By the incoming message action and S from eq. (B.29), after(S, ?\{1_j, \vec{v}\}) is defined, as required.

### [TCHOICE]

From the rule, we know that for some \mu \in I, then

t = send t, (\{1_\mu \triangleright e_1, ..., e_n\})
\theta \vdash exp_j : T'_j for all j \in 1..n (B.30)
S = \oplus\{1_j(\vec{T}_j)\}_{j \in I} (B.31)

By Lemma 16 and eq. (B.30), any expression e_i can be either a value, or else reduce to a new expression, so we consider both sub-cases:

- 1. If, for any i \in 1..n, expression e_i can be reduced (i.e., e_i \Rightarrow e'_i), then case holds by [rCHOICE_e], resulting in the internal transition: t \xrightarrow{\tau} send t, (\{1_\mu \triangleright v_1, ..., v_{i-1}, e'_i, ..., e_n\})

Since this is an internal transition, after(S, \tau) is defined for any S.

- 2. Otherwise, for all i \in 1..n, e_i = v_i, then case holds by [rCHOICE_v], resulting in the transition t \xrightarrow{!(1, v_1, ..., v_n)} (1, v_1, ..., v_n). In this case, a message containing (1, v_1, ..., v_n) is sent to process with pid t. From eq. (B.31), we know that S is an internal choice, thus after(S, !(1, \vec{v})) is defined, as required.

### [TKNOWNCALL]

From the rule, we know that

t = f(t, e_2, ..., e_n)
\theta \vdash exp_i : T_i for all i \in 2..n (B.32)

By Lemma 16 and eq. (B.32), any expression e_i can be either a value, or else reduce to a new expression, so we consider both sub-cases:

- 1. If, for any i \in 2..n, expression e_i can be reduced (i.e., e_i \Rightarrow e'_i), then case holds by [rCALL_e], resulting in the internal transition: t \xrightarrow{\tau} f(v, v_2, ..., v_{i-1}, e'_i, ..., e_n).

- 2. Otherwise, if for all i \in 2..n, e_i = v_i, then case holds by [rCALL_v], resulting in the transition t \xrightarrow{fn} t'[f_j/x_j]_{j=1}^n ... The callee's function body (i.e., t') and the substitution details (e.g. y, x_2) are obtained directly from the function information environment \Sigma using the transition action fn, e.g. \Sigma (fn).body = t'.

For both cases, after(S, \sigma) is defined since after accepts and session type S for internal actions (fn and \tau).

### [TUNKNOWNCALL]

Analogous to previous case.
