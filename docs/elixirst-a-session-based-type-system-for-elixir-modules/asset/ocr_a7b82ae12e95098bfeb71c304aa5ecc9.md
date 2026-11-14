```
$\vdash \vdash_{pat} w_1 : T \triangleright \Gamma''$ and $\vdash \vdash_{pat} w_2 : [T] \triangleright \Gamma''$
```

Applying the inductive hypothesis twice to eqs. (B.13a-d) results in

```
$\Gamma' = x_1 : T_1, ..., x_j : T_j$ and $\Gamma'' = x_k : T_k, ..., x_n : T_n$ 
$\vdash \vdash_{exp} v_j^i : T_j$ for all $i \in 1..n$
```

Therefore, case holds for eqs. (B.13e) and (B.13f), since $\Gamma = \Gamma', \Gamma''$.

[p = (w1, ..., wm), v = (v1, ..., vn)] Using the match definition, match({w1, ..., wm}, {v1, ..., vn}) = match(w1, v1), ..., match(wm, vn) = $\sigma$, or equivalently, for i $\in$ 1..m,

```
match(wi, vi) = $\sigma_i$ given that $\sigma = \sigma_1, ..., \sigma_m$
```

From $\vdash \vdash_{exp} v_1 : T_1 ... v_2 : [T_1, ..., T_m]$, by [TTUPLE], we know that

```
$\vdash \vdash_{exp} v_i : T_i$
```

Applying also [rtTUPLE] to $\vdash \vdash_{pat} (w_1, ..., w_m) : \{T_1, ..., T_m\} \triangleright \Gamma_1, ..., \Gamma_m$, results in

```
$\vdash \vdash_{pat} w_i : T_i \triangleright \Gamma_i$
```

Applying the inductive hypothesis m times to eqs. (B.14a-c) results in

```
$\Gamma = \Gamma_1, ..., \Gamma_m = x_1 : T_1, ..., x_n : T_n$ 
$\vdash \vdash_{exp} v_j : T_j$ for all $j \in 1..n$
```

as required. $\square$

# **Corollary 14.** For all patterns $\vec{p} = p^1, ..., p^n$, values $\vec{v} = v_1, ..., v_n$ and $\forall j \in 1..n$, then the following implication holds.

```
**match($\vec{p}$, $\vec{v}$)** = [v1 : ... vk ... vn] 
$\vdash \vdash_{pat} p^j : T^j \triangleright \Gamma^j$ 
$\theta \vdash \vdash_{exp} v_j : T^j$ 
$\Longrightarrow$ 
{ $\widetilde{\Gamma} = \Gamma^1, ..., \Gamma^j = x_1 : T_1, ..., x_k : T_k$ 
$\{\theta \vdash \vdash_{exp} v_i^j : T_i$ for $i \in 1..k$
```

**Proof.** Take j = 1, where we know that match(p1, v1) = $\sigma_1$, $\vdash \vdash_{pat} p^1 : T^1 \triangleright \Gamma^1$ and $\vdash \vdash_{exp} v_1 : T^1$. Then, applying this information to Lemma 13, we get

```
$\Gamma^1 = x_1^1 : T_1^1, ..., x_m^1 : T_m^1$ 
$\vdash \vdash_{exp} v_1^j : T_i^j$ for $i \in 1..m$
```

Generalising for $j \in 1..n$, then $\vdash \vdash = \Gamma^1, ..., \Gamma^n$ holds by generalising eq. (B.15a). Also $\vdash \vdash_{exp} v_i^j : T_i$ for $i \in 1..k$ holds by eq. (B.15b). Thus, Corollary 14 holds by applying Lemma 13 n times. $\square$

Lemma 15 shows that the type of expressions remains unchanged (or preserved) after an expression is reduced. This means that expressions have a constant type in all steps of reductions, until the expression cannot be reduced further.

# **Lemma 15 (Preservation (Expressions)).** If $\vdash \vdash_{exp} e : T$ and $e \rightarrow e'$, then $\vdash \vdash_{exp} e' : T$

**Proof.** Follows by induction on $\vdash \vdash_{exp} e : T$. We consider the main cases:

[TTUPLE] From the rule, we know that $e = (e_1, ..., e_k, ..., e_n)$, $T = [T_1, ..., T_n]$ and

```
$\vdash \vdash_{exp} e_i : T_i$ for all $i \in 1..n$
```

Deriving $e \rightarrow e'$ using [rtTUPLE] results in $e' = [v_1, ..., v_{k-1}, e'_k, ..., e_n]$ and

```
$e_k \rightarrow e'_k$
```

Applying eqs. (B.16a) and (B.16b) to the inductive hypothesis results in $\vdash \vdash_{exp} e'_k : T_k$. By the latter, eq. (B.16a) and [TTUPLE], we get $\vdash \vdash_{exp} e' : T$, as required.