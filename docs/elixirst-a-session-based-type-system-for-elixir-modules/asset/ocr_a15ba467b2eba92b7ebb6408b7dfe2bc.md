[TCASE] From the rule, we know that for some type U,

t = case e do (p_i -> t_i)_{i \in I} (x_{nil} -> t_{all}) end \quad (B.23a)
\Delta \cdot (x_{nil} : U) \vdash^w S > t_{all} : T < S' \quad (B.23b)
\emptyset \vdash_{exp} e : U \quad (B.23c)
\vdash^w_{par} p_i : U > \Gamma'_i \quad \text{for all } i \in I \quad (B.23d)
\Delta \cdot \Gamma''_i \vdash^w S > T_i : T < S' \quad \text{for all } i \in I \quad (B.23e)

By eq. (B.23a), term reduction, t \mapsto t', can be derived using two rules, so we consider two sub-cases:

+   1. [RCASE_1] From the rule, we know that t' = case e' do (p_i -> t_i)_{i \in I} (x_{nil} -> t_{all}) end. From the premise we know that

e \to e' \quad (B.23f)

By eqs. (B.23c) and (B.23f) and the Preservation (Expressions) Lemma, we get

\emptyset \vdash_{exp} e' : U \quad (B.23g)

Using eqs. (B.23b), (B.23d), (B.23e), (B.23g), and [TCASE], we get

\Delta \cdot \vdash^w S > case e' do (p_i -> t_i)_{i \in I} (x_{nil} -> t_{all}) end : T < S'

which holds as expected given after(S, \tau) = S and after(\Delta, S) = \Delta.

+   2. [RCASE_2] From the rule, we know that t = case v do (p_i -> t_i)_{i \in I} (x_{nil} -> t_{all}) end and e = v. For convenience, we include the catch-all pattern in t with the remaining patterns, so t = case v do (p_i -> t_i)_{i \in I} end. So, for some j \in I',

\text{match}(p_j, v) = \sigma \text{ where } \sigma = [\tau :: \dots \backslash v_k / \dots \backslash \kappa] \quad (B.23h)

t' = t_j \sigma \quad (B.23i)

By eqs. (B.24c), (B.23d) and (B.23h) and Lemma 13, we know that \Gamma''_j = x_1 : T_1, \dots, x_n : T_n and

\emptyset \vdash_{exp} v_k : T_k \text{ for all } k 1..n \quad (B.23j)

Then, by repeatedly applying the Substitution Lemma to eq. (B.23j), (B.23e for i = j), we get

\Delta \cdot \vdash^w S > \sigma : T < S'

This holds since after(S, \tau) = S and after(\Delta, S) = \Delta. \square

[TEXPRESSION] From the rule, we know that

t = e \quad (B.24a)

\emptyset \vdash_{exp} e : T \quad (B.24b)

From the structure of t (eq. (B.24a)), term transition (t \mapsto t') can only be derived using [RExpression], resulting in an internal transition (i.e., \alpha = \tau)

e \to e' \quad (B.24c)

By Lemma 15 and eqs. (B.24b) and (B.24c), we know that

\emptyset \vdash_{exp} e' : T \quad (B.24d)

Thus, case holds since [RExpression] and eq. (B.24d).