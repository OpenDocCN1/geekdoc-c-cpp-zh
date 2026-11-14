
since by the Variable Substitution Definition, w = w[\gamma]. Therefore, eqs. (B.11c), (B.10g) and (B.10h) can be applied to the premise of [TBRANCH] to obtain eq. (B.10):

```
\(\Delta \cdot \Gamma \vdash^{w[\gamma]} S \Downarrow t [\gamma] : T \Downarrow S'\)
```

which is the required result. In case when w = x, then an additional mapping may be obtained from the pattern type rule which maps the dual pid to type. However, since in this case x could be substituted to a variable, then the extra mapping does not affect the result, obtaining eq. (B.10) as required.

[TCHOICE] From the rule, we know that for some \(\mu \in \iota\), \(T = atom, T'_{\mu}, ..., T'_{\mu}\), \(S = \oplus \{ \oplus_{\mu} (\widetilde{T}_{\mu}), S_{\mu} \}_{\iota \in \iota}\) and

```
\(t = send \{ t_i : \{ \iota_1 . e_1, ..., e_n \} \}\) (B.11a)
\(\Gamma, x : T \vdash^{exp} e_j : T'_{\mu}\) for all \(j \in 1..n\) (B.11b)
\(\Gamma \vdash^{exp} v : T\) (B.11c)
```

Applying eqs. (B.11b) and (B.11c) to item ii of Lemma 11 results in \(\Gamma \vdash^{exp} e_j [\gamma] : T'_{\mu}\) for all \(j \in 1..n\). Applying this result to [TCHOICE] results in

```
\(\Delta \cdot \Gamma \vdash^{w[\gamma]} S \Downarrow t [\gamma] : T \Downarrow S'\)
```

which is the required result, since \(t [\gamma] = send \{ w [\gamma] . \{ \iota_1 . e_1 [\gamma], ..., e_n [\gamma] \} \}\). \(\square\)

Lemma 12 links expression types to the basic values (and vice versa), e.g. the value 5 has type number.

## Lemma 12 (Value Typing).

- i. \(\Gamma \vdash^{exp} v : boolean \text{ iff } v = boolean\)
- ii. \(\Gamma \vdash^{exp} v : number \text{ iff } v = number\)
- iii. \(\Gamma \vdash^{exp} v : atom \text{ iff } v = atom\)
- iv. \(\Gamma \vdash^{exp} v : pid \text{ iff } v = \iota\)
- v. \(\Gamma \vdash^{exp} v : [T] \text{ iff } v = [v_1 | v_2] \text{ or } v = []\)
- vi. \(\Gamma \vdash^{exp} v : \{ \tilde{T} \} \text{ iff } v = \{ \tilde{v} \}\)

Proof. By case analysis on the expression typing rules. \(\square\)

Lemma 13 provides a guarantee that the variables inside the substitutions produced by the match function have the expected types. It also ensures that the variables from the same substitutions, which are stored in \(\Gamma\), are assigned with the same types. Consequently, Corollary 14 provides the same guarantees but for a sequence of patterns and values.

## Lemma 13. For all patterns p and values v.

```
\(\text{match}(p, v) = [v_1 \cdots v_n / x_1 \cdots x_n] \vdash_{pa}^{w} p : T \Downarrow \Gamma \vdash^{exp} v : T \implies \begin{cases} \Gamma = x_1 : T_1, ..., x_n : T_n \\ \vdash^{exp} v_i : T_i ; \text{for } i \in 1..n \end{cases}\)
```

Proof. By induction on the definition match(p, v). We proceed by case analysis:

[p = b, v = b] By the definition, match(b, b) = [], so no substitutions are expected. By \(\vdash_{pa}^{w} b : T \Downarrow \Gamma\) and [TPBASIC], the variable binding environment (i.e., \(\Gamma\)) must be empty, so case holds immediately.

[p = x] By definition, match(x, v) = [v/x], and from the premise we know that

```
\(\emptyset \vdash^{exp} v : T\). (B.12a)
```

From \(\vdash^{w}_{pa} x : T \Downarrow \Gamma\) and [TPVARIABLE], we know that \(\Gamma\) must contain x : T only. Therefore, case holds by eq. (B.12a).

[p = [w1 | w2], v = [v1 | v2]] Using the match definition, match([w1 | w2], [v1 | v2]) = match(w1, v1), match(w2, v2), or equivalently

```
\(\text{match}(w_1, v_1) = [v_1 \dots v_k / x_1 \dots x_k]\) (B.13a)
\(\text{match}(w_2, v_2) = [v_{k+1} \dots v_n / x_{k+1} \dots x_n] \text{ where } k = j + 1\) (B.13b)
```

From the premise, applying [RLIST] to \(\emptyset \vdash^{exp} [v_1 | v_2] : [T]\), results in

```
\(\emptyset \vdash^{exp} v_1 : T \text{ and } \emptyset \vdash^{exp} v_2 : [T]\) (B.13c)
```

Applying also [TPLIST] to \(\vdash_{pa}^{w} [w_1 | w_2] : [T] \Downarrow \Gamma\), results in

```
\(\vdash_{pat} w_1 : T \triangleright \Gamma''\) and \(\vdash_{pat} w_2 : [T] \triangleright \Gamma''\)
```

Applying the inductive hypothesis twice to eqs. (B.13a-d) results in

```
\(\Gamma' = x_1 : T_1, ..., x_j : T_j\) and \(\Gamma'' = x_{k} : T_k, ..., x_n : T_n\)
\(\vdash^{exp} v_i : T_i\) for all \(i \in 1..n\)
```

Therefore, case holds for eqs. (B.13e) and (B.13f), since \(\Gamma = \Gamma', \Gamma''\).

[p = (w1, ..., wm), v = (v1, ..., vn)] Using the match definition, match((w1, ..., wm), (v1, ..., vn)) = match(w1, v1), ..., match(wm, vn) = \(\sigma\), or equivalently, for \(i \in 1..m\),

```
match(w_i, v_i) = \(\sigma_i\) given that \(\sigma = \sigma_1, ..., \sigma_m\)
```

From \(\vdash^{exp} (v_1, ..., v_m) : [T_1, ..., T_m]\), by [TTUPLE], we know that

```
\(\vdash^{exp} v_i : T_i\)
```

Applying also [rtTUPLE] to \(\vdash_{pat} (w_1, ..., w_m) : \{T_1, ..., T_m\} \triangleright \Gamma_1, ..., \Gamma_m\), results in

```
\(\vdash_{pat} w_i : T_i \triangleright \Gamma_i\)
```

Applying the inductive hypothesis m times to eqs. (B.14a-c) results in

```
\(\Gamma = \Gamma_1, ..., \Gamma_m = x_1 : T_1, ..., x_n : T_n\)
\(\vdash^{exp} v_j : T_j\) for all \(j \in 1..n\)
```

as required. \(\square\)

## Corollary 14. For all patterns \(\vec{p} = p^1, ..., p^n\), values \(\vec{v} = v_1, ..., v_n\) and \(\forall j \in 1..n\), then the following implication holds.

```
match(\vec{p}, \vec{v}) = [v_1, ..., v_k, ..., v_n]
\(\vdash_{pat} p^j : T^j \triangleright \Gamma^j\)
\(\theta \vdash^{exp} v_j : T^j\)
\(\Longrightarrow\)
\(\widetilde{\Gamma} = \Gamma^1, ..., \Gamma^j = x_1 : T_1, ..., x_k : T_k\)
\(\theta \vdash^{exp} v_i^j : T_i\) for \(i \in 1..k\)
```

**Proof.** Take j = 1, where we know that match(p1, v1) = \(\sigma_1\), \(\vdash_{pat} p^1 : T^1 \triangleright \Gamma^1\) and \(\vdash^{exp} v_1 : T^1\). Then, applying this information to Lemma 13, we get

```
\(\Gamma^1 = x_1^1 : T_1^1, ..., x_m^1 : T_m^1\)
\(\vdash^{exp} v_1^j : T_i^j\) for \(i \in 1..m\)
```

Generalising for \(j \in 1..n\), then \(\Gamma = \Gamma^1, ..., \Gamma^n\) holds by generalising eq. (B.15a). Also \(\vdash^{exp} v_i^j : T_i\) for \(i \in 1..k\) holds by eq. (B.15b). Thus, Corollary 14 holds by applying Lemma 13 n times. \(\square\)

Lemma 15 shows that the type of expressions remains unchanged (or preserved) after an expression is reduced. This means that expressions have a constant type in all steps of reductions, until the expression cannot be reduced further.

## Lemma 15 (Preservation (Expressions)). If \(\vdash^{exp} e : T\) and \(e \rightarrow e'\), then \(\vdash^{exp} e' : T\)

**Proof.** Follows by induction on \(\vdash^{exp} e : T\). We consider the main cases:

[TTUPLE] From the rule, we know that \(e = (e_1, ..., e_k, ..., e_n)\), \(T = [T_1, ..., T_n]\) and

```
\(\vdash^{exp} e_i : T_i\) for all \(i \in 1..n\)
```

Deriving \(e \rightarrow e'\) using [rtTUPLE] results in \(e' = [v_1, ..., v_{k-1}, e'_k, ..., e_n]\) and

```
\(e_k \rightarrow e'_k\)
```

Applying eqs. (B.16a) and (B.16b) to the inductive hypothesis results in \(\vdash^{exp} e'_k : T_k\). By the latter, eq. (B.16a) and [TTUPLE], we get \(\vdash^{exp} e' : T\), as required.

[TARITHMETIC] From the rule we know that \(e = e_1 \circ e_2\), \(T = \text{number}\) and

```
\(\emptyset \vdash^{exp} e_1 : \text{number}\) (B.17a)
\(\emptyset \vdash^{exp} e_2 : \text{number}\) (B.17b)
```

\(e \to e'\) can be derived using different rules, so we consider three sub-cases:

- [REOPERATION] From this rule we know that \(e' = e'_1 \circ e_2\) and

\(e_1 \to e'_1\) (B.17c)

Applying eqs. (B.17a) and (B.17c) to the inductive hypothesis results in \(\emptyset \vdash^{exp} e'_1 : \text{number}\). Using this information, along with eq. (B.17b) in [TARITHMETIC], results in \(\emptyset \vdash^{exp} e' : \text{number}\), as required.

- [REOPERATION2] Analogous to [REOPERATION].

- [REOPERATION3] From the rule, we know that \(e = v_1 \circ v_2\). Since we know that \(\emptyset \vdash^{exp} e : T\), or \(\emptyset \vdash^{exp} v_1 \circ v_2 : T\), then \(\emptyset \vdash^{exp} e' : T\) follows immediately given that \(e' = v = v_1 \circ v_2\).

Regarding the remaining cases: Cases [TBASIC], [TVARIABLE] and [TLIST] hold trivially, since \(e \to e'\) does not apply. Cases [TCOMPARISON] and [TBOOLEAN] are analogous to [TARITHMETIC]. Cases [TLIST] and [TNOT] take a similar approach to [TTUPLE].

Lemma 10-15 allow us to prove the Session Fidelity Theorem. This is one of the main results of Section 5.

## Theorem 2 (Session Fidelity). If \(\Delta \cdot \emptyset \vdash^w S \triangleright T : T < S'\) and \(t \xrightarrow{\alpha} t'\)

- for \(\alpha = ?\{i.. \overline{i}\}, \overline{v}\rangle\) and some session type \(S' = \text{after}(S, \alpha)\), then there exists some \(\Delta'\), such that \(\Delta' \cdot \emptyset \vdash^w S' \triangleright t' : T < S'\) and \(\text{after}(\Delta, \alpha, S) = \Delta'\)
- for \(\alpha \in \{f, t, \iota, !\{i.. \overline{i}\}, \overline{v}\rangle\}\), then there exists some \(S''\) and \(\Delta'\), such that \(\Delta' \cdot \emptyset \vdash^w S'' \triangleright t' : T < S'\) for \(\text{after}(S, \alpha) = S''\) and \(\text{after}(\Delta, \alpha, S) = \Delta'\)

### Proof.

By induction on the typing derivation \(\Delta \cdot \emptyset \vdash^w S \triangleright t : T < S'\).

### [TLET]

From the rule, we know that \(x \neq w\), and

```
t = (x = t_1; t_2) (B.18a)
\(\Delta \cdot \emptyset \vdash^w S \triangleright t_1 : T' < S''\) (B.18b)
\(\Delta \cdot (x : T') \vdash^w S'' \triangleright t_2 : T < S'\) (B.18c)
```

From the structure of t (eq. (B.18a)), term transitions (\(t \xrightarrow{\alpha} t'\)) can be derived using two rules, so we consider two sub-cases:

- [RLET] From this rule, we know that \(t' = (x = t'_1; t_2)\) and

\(t_1 \xrightarrow{\alpha} t'_1\) (B.18d)

If \(\alpha = ?\{i.. \overline{i}\}\), then by \(\alpha\), eqs. (B.18b) and (B.18d) and the inductive hypothesis we obtain

\(\Delta' \cdot \emptyset \vdash^w S'' \triangleright t'_1 : T' < S''\) (B.18e)

where \(\text{after}(\Delta, \alpha, S) = \Delta'\). In case that \(\alpha \neq ?\{i.. \overline{i}\}, \overline{v}\rangle\), eq. (B.18e) can be obtained as well, however we also require \(\text{after}(S, \alpha) = S''\), which holds immediately. Also, by the After Function Definition, we know that \(\Delta'\) is an extension of \(\Delta\), so we can apply the \(\Delta\)-Weakening Lemma on eq. (B.18c) to get

\(\Delta' \cdot (x : T') \vdash^w S'' \triangleright t_2 : T < S'\) (B.18f)

Using eqs. (B.18e) and (B.18f) as the premise for rule [rTLET], we obtain:

```
[TLET] \frac{\Delta' \cdot \emptyset \vdash^w S \triangleright t_1 : T' < S'' \quad \Delta' \cdot (x : T') \vdash^w S'' \triangleright t_2 : T < S' \quad x \neq w}{\Delta' \cdot \emptyset \vdash^w S \triangleright x = t_1; t_2 : T < S'}
```
