Therefore
\( u^n(x) \ge \inf_{V \in \mathcal{V}} J_x(V) \),
and also
\( \bar{u}(x) \ge \inf_{V \in \mathcal{V}} J_x(V) \).
On the other hand for any control, not necessarily in \(\mathcal{V}\) we can write
\(\bar{u}(x) \le E^{V,x} \sum_{j=1}^{n_0} \alpha^{j-1} l(y_j, v_j) + \alpha^n E^{V,x} \bar{u}(y_{n+1})\)
\(\le J_x(V) + \alpha^n E^{V,x} \bar{u}(y_{n+1})\).
Now if \( V \in \mathcal{V} \) the 2nd term goes to 0 as \( n \to \infty \). Therefore we can assert
\( \bar{u}(x) \le J_x(V) \forall V \in \mathcal{V} \),
and this completes the proof of the Theorem.

**Remark.** We do not claim that the infimum is attained in the right hand side of (4.4.7). Moreover the maximum solution is u.s.c. and not l.s.c.

# 4.5. UNIQUENESS

We consider the problem of uniqueness of solutions of the functional equation (4.3.7), in the interval \((0, w_0)\). A necessary and sufficient condition for uniqueness is that the minimum and the maximum solutions coincide. To prove that the minimum and maximum solutions coincide, it is sufficient to prove that the optimal control \(\bar{V} \in \mathcal{V}\). A different approach is to use contraction properties, when they are available.

# **Theorem 4.6.** Assume \( l(x, v) \) bounded. Then there exists one and only solution of (4.3.7)

**PROOF.** We can use a contraction property. Let us recall that \( B \) denotes the space of bounded functions on \( X = R^d \). We notice that (4.3.7) can be written as a fixed point for the map

```
\( T : B \to B, z = Tw, \)
```

with

```
\( Tw(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v(w)], \)
```

and since \( l \) is bounded we can define \( T \) as a map from \( B \) into \( B \). With \( \alpha < 1 \) it is obvious that \( T \) is a contraction. Hence there exists one and only one fixed point.

**Remark.** Since \( w_0 \) is bounded, the uniqueness follows also immediately from the fact that condition (4.4.6) is always satisfied.

This result can be extended in several ways.

# **Theorem 4.7.** Assume that

```
(4.5.1) \( 0 \le l(x, v) \le h|x| + c|v| + l_0, \)
```

```
(4.5.2) \( \Phi^v(|x|)(x) \le \theta|x| + \lambda|v| + \mu, \)
```

and \( U \) is compact. If \( \alpha\theta < 1 \) the solution of (4.3.7) in the space \( B_1 \) of functions with linear growth exists and is unique.