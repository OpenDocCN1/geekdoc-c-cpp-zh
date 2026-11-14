# **Proposition 13.3.** We assume

```
(13.3.25) \(\alpha^L((1-\alpha)c - \alpha^L p)(L-1)D + K(1-\alpha) \ge 0,\)
```

then the property (13.3.24) is satisfied.

PROOF. We note that this result includes the case L = 1 in which the condition is automatically satisfied. The proof is similar to that of the case L = 1.

We recall that

```
(13.3.26) \(H_s(x) - \alpha E H_s(x - D) = g_s(x), \forall x.\)
```

We then find a similar equation for \(\Phi_s(x)\). This is where it is important to consider \(\Phi_s(x)\) and not \(\Psi_s(x)\), since we write the equation for any x and not just for x > s. It is easy to verify that \(\Phi_s(x)\) is the solution of

```
(13.3.27) \(\Phi_s(x) - \alpha E \Phi_s(x - D) = g_s(x) + \alpha E(g(x - D) - g(s)) \mathbb{I}_{s-D < s} - \alpha^L E(g(x - D^{(L)}) - g(s)) \mathbb{I}_{s-D^{(L)} < s},\)
```

and again we check that this equation coincides with (13.3.26) when L = 1. Going back to (13.3.24) we recall that

```
\(K + \inf_{\eta \ge x} \Phi_s(\eta) \ge K + \inf_{\eta > s} \Phi_s(\eta) = 0, \forall x > s.\)
```

So it is sufficient to prove (13.3.24) for \(x > x_0 > s\), the first value larger than s such that \(H_s(x) \ge 0\). We necessarily have \(H_s(x_0) = 0\). We have \(s < \xi < x_0\). Let us fix \(\xi > 0\). We consider the domain \(x \ge x_0 - \xi\). We can write

```
(13.3.28) \(H_s(x) - \alpha E H_s(x - D) \mathbb{I}_{x-D \ge x_0 - \xi} \le g_s(x), \forall x,\)
```

using the fact that

```
\(E H_s(x - D) \mathbb{I}_{x-D < x_0 - \xi} \le 0.\)
```

Define next

```
\(M_s(x) = \Phi_s(x + \xi) + K.\)
```

We note that \(M_s(x) > 0, \forall x\).

```
\(M_s(x) - \alpha E M_s(x - D) = g_s(x + \xi) + \alpha E(g(x + \xi - D) - g(s)) \mathbb{I}_{\xi + \xi - D < s} - \alpha^L E(g(x + \xi - D^{(L)}) - g(s)) \mathbb{I}_{\xi + \xi - D^{(L)} < s} + K(1 - \alpha)\)
```

and using the positivity of M we can assert that

```
(13.3.29) \(M_s(x) - \alpha E M_s(x - D) \mathbb{I}_{x-D \ge x_0 - \xi} \ge g_s(x + \xi) + \alpha E(g(x + \xi - D) - g(s)) \mathbb{I}_{\xi + \xi - D < s} - \alpha^L E(g(x + \xi - D^{(L)}) - g(s)) \mathbb{I}_{\xi + \xi - D^{(L)} < s} + K(1 - \alpha)\)
```

We now consider the difference \(Y_s(x) = H_s(x) - M_s(x)\), in the domain \(x \ge x_0 - \xi\).

We have

```
(13.3.30) \(Y_s(x) - \alpha E Y_s(x - D) \mathbb{I}_{x-D \ge x_0 - \xi} \le g_s(x) - g_s(x + \xi) - \alpha E(g(x + \xi - D) - g(s)) \mathbb{I}_{\xi + \xi - D < s} + \alpha^L E(g(x + \xi - D^{(L)}) - g(s)) \mathbb{I}_{\xi + \xi - D^{(L)} < s} - K(1 - \alpha)\)
```

We have seen from the case L = 1, Theorem 9.11, that

```
\(g_s(x + \xi) - g_s(x) \ge 0, \forall x \ge x_0 - \xi.\)
```

Consider next the function

```
\(\chi_s(y) = \alpha E(g(y - D) - g(s)) \mathbb{I}_{y-D < s} - \alpha^L E(g(y - D^{(L)}) - g(s)) \mathbb{I}_{y-D^{(L)} < s},\)
```