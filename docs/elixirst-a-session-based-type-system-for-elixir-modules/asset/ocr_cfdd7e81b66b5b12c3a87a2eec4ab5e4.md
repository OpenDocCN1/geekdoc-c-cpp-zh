[t = case e do (p_i \rightarrow t_i)_{i \in I} end] Given that current structure of t, which implicitly contains the catch-all pattern, we can derive t \mapsto t' using two cases:

+   1. [RCASE1] From the rule we know that t' = case e' do (p_i \rightarrow t_i)_{i \in I} end, and from the premise we know that e \rightarrow e'
+   
+   e \rightarrow e' (B.6a)
+   
+   Since fv(t) = \emptyset, by the fv definition, we know that
+   
+   fv(t_i) \setminus vars(p_i) = \emptyset \quad \text{for all } i \in I (B.6b)
+   
+   fv(e) = \emptyset (B.6c)
+   
+   Applying Closed Expression Lemma to eqs. (B.6a) and (B.6c), results in fv(e') = \emptyset. Thus, using this information, along with eq. (B.6b) and the fv definition, we get fv(t') = \emptyset as needed.

+   2. [RCASE2] From the rule, we know that t = case v' do (p_i \rightarrow t_i)_{i \in I} end, e = v' and for some j \in I,
+   
+   match(p_j, v') = \sigma \quad \text{where } \sigma = [^{y_1}_{x_1} ... ^{y_n}_{x_n}] (B.6d)
+   
+   t' = t_j \sigma (B.6e)
+   
+   From the premise, we know that fv(t) = \emptyset, so by the fv definition, fv(v') = \emptyset and
+   
+   fv(t_i) \setminus vars(\tilde{p}_i) = \emptyset \quad \text{for all } i \in I (B.6f)
+   
+   From eq. (B.6d), we can apply Lemma 8, to get
+   
+   vars(p_j) = \{x_1, ..., x_k\} (B.6g)
+   
+   Substituting eq. (B.6g) in eq. (B.6f) (for i = j), we get fv(t_j) \setminus \{x_1, ..., x_k\} = \emptyset. By similar reasoning from previous cases, we get fv(t') = \emptyset, as required.

# B.2. Proofs for Theorem 2

Before proving Theorem 2, we consider some other necessary lemmata. The \Delta-Weakening Lemma weakens (i.e., extends) the session typing environment (\Delta) without affecting the overall typing result.

# **Lemma 10** (\Delta-Weakening). If \Delta, \Gamma \vdash^w S > t : T < S', then (\Delta, \Delta'), \Gamma \vdash^w S > t : T < S'

**Proof.** Follows by induction on the derivation of \Delta . \Gamma \vdash^w S > t : T < S'. We analyse the significant cases:

+   [TUNKNOWNCALL] From the rule, we know that
+   
+   (\Delta, f h : S, \Gamma) \vdash^w S > \tilde{e} : T < S' (B.7a)
+   
+   \Gamma \vdash exp_i : T_i \quad \text{for all } i \in 2..n (B.7b)
+   
+   Applying the inductive hypothesis to eq. (B.7a) results in (\Delta, \Delta', f h : S, \Gamma) \vdash^w S > t : T < S', where we assume fv h \in dom(\Delta). So, using the latter result, eq. (B.7b) and [TUNKNOWNCALL] results in (\Delta, \Delta'), \Gamma \vdash^w S > t : T < S', as required.

+   [TKNOWNNCALL] From the rule, we know that
+   
+   \Delta (f h) = S (B.8a)
+   
+   \Gamma \vdash exp_i : T_i \quad \text{for all } i \in 2..n (B.8b)
+   
+   If we extend \Delta by \Delta', then (\Delta, \Delta')(f h) = S remains valid. So, using this information, along with eq. (B.8b) in [TKNOWNNCALL], we get (\Delta, \Delta'), \Gamma \vdash^w S > t : T < end, as required.

Cases [TCHOICE] and [TREXPRESSION] hold immediately since \Delta is unused. The remaining cases hold effortlessly by the inductive hypothesis.

The type system observes the session fidelity property if well-typed terms remain well-typed after transitioning. As terms transition, in particular in the rules [RLETS_], [RCALLs] and [RBRANCH], variables are substituted with values. The Substitution Lemma (Lemma 11) ensures that when free variables inside terms and expressions are substituted with a closed value,