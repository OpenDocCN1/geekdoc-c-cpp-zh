We will also make use of the Bramble–Hilbert lemma [69], which estimates how well a function u can be approximated by polynomials in relevant Sobolev norms. It can be established uniformly over convex domains [117, 402] and can be extended to non-convex domains that are “star-shaped with respect to a ball” [70]. We state the convex version here.

# Theorem 2.2 (Bramble–Hilbert). There exists a constant \( C_{\text{BH}} \) depending only upon \( d \) such that for any convex polytope \( P \subset \mathbb{R}^d \) of diameter 1 and any \( u \in H^2(P) \), there exists an affine polynomial \( p_u \) such that,

```
\(\|u - p_u\|_{H^1(P)} \le C_{\text{BH}} |u|_{H^2(P)}.\)
```

We now state five additional estimates that are either helpful or essential in proving (2.3). All of these are stated in terms of the spatial dimension \( d \) for unit diameter domains.

+   - Uniform Sobolev Embedding: \(\sum_{i=1}^n |u(v_i)| \le C_{\text{USE}} \|u\|_{H^2(P)}.\) (2.6)
+   - Bounded Gradients in \( L^\infty \): \(\|\nabla \phi_i\|_{L^\infty(P)} \le C_{\nabla \phi}.\) (2.7)
+   - Bounded Gradients in \( H^1 \): \(\|\phi_i\|_{H^1(P)} \le C_{H^1}.\) (2.8)
+   - Bounded Interpolation: \(\|Iu\|_{H^1(P)} \le C_{\text{BI}} \|u\|_{H^2(P)}.\) (2.9)
+   - Interpolation Error: \(\|u - Iu\|_{H^1(P)} \le C_{\text{IE}} |u|_{H^2(P)}.\) (2.10)

Each estimate is of interest when the associated constant \( C \) can be bounded above uniformly over some class p of polygons or polyhedra. In such cases, we say the estimate “holds over p” and we have the following implications.

# Proposition 2.3. Let p be a class of polygons or polyhedra with unit diameter.

+   - (i) If (2.7) holds over p, then (2.8) holds over p.
+   - (ii) If (2.6) and (2.8) hold over p, then (2.9) holds over p.
+   - (iii) If (2.9) holds over p, then (2.10) holds over p.

Proof. For (i), we have that

```
\(\|\phi_i\|_{H^1(P)}^2 = \int_P |\phi_i|^2 + |\nabla \phi_i|^2 \le (1 + \|\nabla \phi_i\|_{L^\infty(P)}^2)|P| \le (1 + C_{\nabla \phi}^2)|P|,\)
```

where \( |P| \) denotes the measure of \( P \). Since \( |P| \) must be contained inside a \( d \)-ball of unit radius, there is a constant \( C \) such that \( |P| \le C \) and the estimate follows.

For (ii), Theorem 2.1 ensures that any \( u \in H^2(P) \) can be treated as a continuous function on \( \bar{P} \), since \( d = 2 \) or 3. Thus, \( u(v_i) \) is well-defined and we have that

```
\(\|Iu\|_{H^1(P)} \le \sum_{i=1}^n |u(v_i)| \cdot \|\phi_i\|_{H^1(P)} \le C_{H^1} C_{\text{USE}} \|u\|_{H^2(P)}.\)
```