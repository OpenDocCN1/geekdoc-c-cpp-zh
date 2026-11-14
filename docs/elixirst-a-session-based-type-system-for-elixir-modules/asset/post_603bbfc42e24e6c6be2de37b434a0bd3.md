
**Definition A.2 (Bound Variables).**

\(\mathbf{bv}(t) \stackrel{\text{def}}{=} \begin{cases} \emptyset & t = e \text{ or } t = \text{send}(w, \{..l, \tilde{e}..\}) \text{ or } t = f(\tilde{e}) \\ \{ x \mid x \in \mathbf{bv}(t_1) \cup \mathbf{bv}(t_2) \} & t = (x = t_1; t_2) \\ \bigcup_{i \in I} \mathbf{bv}(t_i) \cup \mathbf{vars}(\tilde{p}_i) & t = \text{receive do } (\{l_i, \tilde{p}_i \rightarrow t_i\})_{i \in I} \text{end} \\ \bigcup_{i \in I} \mathbf{bv}(t_i) \cup \mathbf{vars}(p_i) & t = \text{case } e \text{ do } (p_i \rightarrow t_i)_{i \in I} \text{end} \end{cases}\)

**Definition A.3 (Variable Substitution).**

\( e \lfloor e' / a \rfloor \stackrel{\text{def}}{=} \begin{cases} e' & e = x \\ y & e = y, y \neq x \\ b & e = b \\ e_1 \lfloor e' / a \rfloor \diamond e_2 \lfloor e' / a \rfloor & e = e_1 \diamond e_2 \\ \text{not } (e' \lfloor e' / a \rfloor) & e = \text{not } e' \\ \{ e_1 \lfloor e' / a \rfloor \diamond e_2 \lfloor e' / a \rfloor \} & e = \{ e_1 \diamond e_2 \} \\ \{ e_1 \lfloor e' / a \rfloor, \dots, e_n \lfloor e' / a \rfloor \} & e = \{ e_1, \dots, e_n \} \end{cases}\)

\( t \lfloor e' / a \rfloor \stackrel{\text{def}}{=} \begin{cases} \text{send}(w \lfloor e' / a \rfloor, \{..l, e_1 \lfloor e' / a \rfloor, \dots, e_n \lfloor e' / a \rfloor \}) & t = \text{send}(w, \{..l, e_1, \dots, e_n\}) \\ \text{receive do } (\{l_i, \tilde{p}_i \rightarrow t_i \lfloor e' / a \rfloor \})_{i \in I} \text{end} & t = \text{receive do } (\{l_i, \tilde{p}_i \rightarrow t_i\})_{i \in I} \text{end} \\ f (e_1 \lfloor e' / a \rfloor, \dots, e_n \lfloor e' / a \rfloor) & t = f (e_1, \dots, e_n) \\ \text{case } e \lfloor e' / a \rfloor \text{ do } (p_i \rightarrow t_i \lfloor e' / a \rfloor)_{i \in I} \text{end} & t = \text{case } e \text{ do } (p_i \rightarrow t_i)_{i \in I} \text{end} \\ y = t_1 \lfloor e' / a \rfloor; t_2 \lfloor e' / a \rfloor & t = (y = t_1; t_2), a \neq y \end{cases}\)

**Definition A.4 (Type).** This partial function defines the types of basic values.

\(\text{type}(\text{boolean}) \stackrel{\text{def}}{=} \text{boolean} \quad \text{type}(\text{number}) \stackrel{\text{def}}{=} \text{number}\)
\(\text{type}(\text{atom}) \stackrel{\text{def}}{=} \text{atom} \quad \text{type}(t) \stackrel{\text{def}}{=} \text{pid}, \text{ where } t \text{ is a pid instance}\)

**Definition A.5 (Variable Patterns).** Computes an ordered set of variables from a given pattern \(p\).

\(\mathbf{vars}(\tilde{p}) \stackrel{\text{def}}{=} \mathbf{vars}(p_1, \dots, p_n) \stackrel{\text{def}}{=} \mathbf{vars}(p_1) \cup \dots \cup \mathbf{vars}(p_n)\)

\(\mathbf{vars}(p) \stackrel{\text{def}}{=} \begin{cases} \emptyset & p = b \\ \{ x \} & p = x \\ \mathbf{vars}(w_1) \cup \mathbf{vars}(w_2) & p = [ w_1 \mid w_2 ] \\ \bigcup_{i \in 1..n} \mathbf{vars}(w_i) & p = [ w_1, \dots, w_n ] \end{cases}\)

**Definition A.6 (Function Details).** We can extract function details (i.e., params, body, param_types, return_type, dual) from a list of functions (\(\tilde{Q}\)) and build a mapping, using set-comprehension, as follows. The list of functions (\(\tilde{Q}\)) may consist of public (\(\tilde{D}\)) and private (\(\tilde{P}\)) functions.

\(\mathbf{details}(\tilde{Q}) \stackrel{\text{def}}{=} \left\{ f/n : \left[ \begin{array}{l} \text{"dual"} = y, \text{params} = \tilde{x}, \\ \text{param\_types} = \tilde{T}, \\ \text{return\_type} = T, \\ \text{body} = t \end{array} \right] \mid \dots \right\} \cup \dots \)

**Definition A.7 (Functions Names and Arity).** This definition takes the set of all public function names and their arity.

\(\mathbf{functions}(\tilde{D}) \stackrel{\text{def}}{=} \left\{ f/n \mid \dots \right\} \in \tilde{D} \)

**Definition A.8 (All Session Types).** The function \(\mathbf{sessions}(\tilde{D})\), returns the session type corresponding to each annotated public function.

```
sessions(D) def = { f/n : S | [ @session "S"; @spec... def f(y, x0, ..., xn) do t end ] D }
```

In case the @dual annotation is used instead of @session, the dual session type is computed automatically.

## Appendix B. Proofs

In this appendix, we present the complete proofs of Proposition 1, Theorems 2 and 4, which were omitted from the main text.

### B.1. Proofs for Proposition 1

Before proving Proposition 1, we must analyse some properties related to closed terms, where we see how they affect variable substitutions (Definition A.3). Lemma 5 states that if a variable x does not exist inside a term t, then, if we initiate x with some value, term t must remain unaffected, i.e., t[γ/τ] = t. Restricting this statement, Corollary 6 states that, if x is not a free variable in t, then the same result should hold. Lemma 7 consists of two statements that compare the free variables in terms (or expressions) with those that include a substitution.

### Lemma 5. x ∉ fv(t) ∧ x ∉ bv(t) implies t[γ/τ] = t

**Proof.** By induction on the structure of t.

### Corollary 6. x ∉ fv(t) implies t[γ/τ] = t

**Proof.** A consequence of Lemma 5.

### Lemma 7.

- i. x ∈ fv(t) implies fv(t{γ/λ}) = fv(t)
- ii. x ∈ fv(e) implies fv(e{γ/λ}) = fv(e)

**Proof.** By induction on the structures of t and e for items i and ii respectively.

### Lemma 8. match(p, v) = [v1 ... vn / x1 ... xn], implies vars(p) = (x1, ..., xn)

**Proof.** By induction on the structure of p.

- [p = b] The function match(b, v) succeeds only when v = b. So, by the match definition, when v = b,

  ```
  match(b, b) = []
  ```

  By the vars definition, vars(b) = ∅, which matches the result from eq. (B.1a) since no variables were substituted.

- [p = x] By the match definition, for any v,

  ```
  match(x, v) = [γ/τ]
  ```

  By the vars definition, vars(x) = (x), which matches the variable in the substitution of eq. (B.1b).

- [p = w1 | w2] By the match definition, for v = v1 | v2.

  ```
  match(p, v) = match(w1, v1).match(w2, v2) = [γ1/τ1][γ2/τ2] where
  ```

  ```
  match(w1, v1) = [γ1/τ1]
  ```

  ```
  match(w2, v2) = [γ2/τ2]
  ```

  By case analysis of w1 and w2 from eqs. (B.1d) and (B.1e), we conclude that

  ```
  vars(w1) = {x1}
  ```

  ```
  vars(w2) = {x2}
  ```

  We need to show that vars(w1 | w2) = {x1, x2}. By the vars definition and eqs. (B.1f) and (B.1g), vars(w1 | w2) = vars(x1) ∪ vars(x2) = {x1} ∪ {x2}. This result matches the variables in the substitutions of eq. (B.1c).

- [p = {w1, ..., wn}] Similar to the previous case.

### Lemma 9 (Closed Expression). fv(e) = ∅ and e → e' implies fv(e') = ∅

**Proof.** By induction on the structure of e.

Lemmata 5-9 allow us to prove Closed Term Proposition (Proposition 1). By this proposition, we can say that a closed term t remains closed, even after t transitions to some new term t', producing an action α. Lemma 9 is analogous; it states that expressions remain closed after reductions.

### Proposition 1 (Closed Term). If fv(t) = ∅ and t →α t', then fv(t') = ∅

**Proof.** By induction on the structure of t.

- [t = e] Holds immediately by the rule [rExpression] and the Expression Lemma.

- [t = (x = t1 ; t2)] Given that current structure of t, we can derive t →α t' using two cases:

  1. [rLET1] From the rule, t' = (x = t1' ; t2) and

     ```
     t1 →α t1' (B.2a)
     ```

     From the premise, fv(t) = ∅, so by the fv definition. fv(t1) ∪ (fv(t2) \ {x}) = ∅, or equivalently

     ```
     fv(t1) = ∅ (B.2b)
     ```

     ```
     fv(t2) \ {x} = ∅ (B.2c)
     ```

     If we apply the inductive hypothesis to eqs. (B.2a) and (B.2b), we get

     ```
     fv(t1') = ∅ (B.2d)
     ```

     So, by eqs. (B.2c) and (B.2d) and the definition of fv, we get fv(x = t1' ; t2) = ∅ as required.

  2. [rLET2] From the rule, t = (x = v ; t2) and t' = t2 [v/x]. Since fv(t) = ∅, by the Free Variables Definition, fv(v) ∪ (fv(t2) \ {x}) = ∅, or equivalently

     ```
     fv(v) = ∅ (B.2e)
     ```

     ```
     fv(t2) \ {x} = ∅ (B.2f)
     ```

     We need to show that fv(t') = ∅, or fv(t2 [v/x]) = ∅, so we consider two sub-cases:

     a. If x ∉ fv(t2), then by Corollary 6, t2 = t2 [v/x]. Substituting this in eq. (B.2f), results in fv(t2 [v/x]) = ∅, as required.

     b. If x ∈ fv(t2), then by Lemma 7, we get fv(t2 [v/x]) = fv(t2) \ {x}. If we substitute this in eq. (B.2f), the case holds.

- [t = send(w, (t1.e1, ..., tn.en))] Given that current structure of t, we can derive t →α t' using two cases:

  1. [rCHOICE1] From this rule, we know that α = τ and

     ```
     t' = send(w, {1 ↓ v1, ..., vk-1, ek', ..., en})
     ```

     ```
     ek → ek' (B.3a)
     ```

     Since fv(t) = ∅, then by the fv definition

     ```
     fv(t) = ∅ (B.3b)
     ```

     ```
     fv(v_i) = ∅ for i ∈ 1..k-1 (B.3c)
     ```

     ```
     fv(e_i) = ∅ for i ∈ k..n (B.3d)
     ```

     Applying the Closed Expression Lemma to eqs. (B.3a) and (B.3d), results in fv(ek) = ∅. Using this information along with eqs. (B.3b-d) and the fv definition, results in fv(t') = ∅ as required.
