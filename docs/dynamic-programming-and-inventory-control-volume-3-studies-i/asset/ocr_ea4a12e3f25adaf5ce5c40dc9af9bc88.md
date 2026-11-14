PROOF. Let \(x < y\). From the equation (9.1.11) we can write

$$
\begin{aligned}
u(x) + (c - h)x &= cD + \inf_{\eta \ge \max(x,D)} [K \mathbf{I}_{\eta > x} + z(\eta - D)] \\
\le cD + K + \inf_{\eta \ge \max(y,D)} z(\eta - D) \\
\le K + cD + \inf_{\eta \ge \max(y,D)} [K \mathbf{I}_{\eta > y} + z(\eta - D)] \\
\le K + u(y) + (c - h)y,
\end{aligned}
$$

which implies

$$
u(x) + cx \le K + u(y) + cy.$$

But then

$$
\begin{aligned}
z(x) &= \alpha(u(x) + cx) + cx(1 - \alpha) \\
\le \alpha K + \alpha(u(y) + cy) + cy(1 - \alpha) \\
\le K + z(y),
\end{aligned}
$$

and the result follows. 

We then deduce

# **Proposition 9.1.** The solution \(u(x)\) satisfies the property

```

(9.1.13) 
\(x < D \implies u(x) = (h - c)x + cD + K + \inf_{\eta \ge 0} z(\eta)\)

(9.1.14) 
\(x \ge D \implies u(x) = hx + \alpha(x - D).\)
```

PROOF. For \(x < D\), the equation (9.1.11) writes

$$
u(x) = (h - c)x + cD + \inf_{\eta \ge D} [K \mathbf{I}_{\eta > x} + z(\eta - D)],$$

and thus

$$
u(x) = (h - c)x + cD + K + K + \inf_{\eta \ge D} z(\eta - D),$$

and the property (9.1.13) follows. Next if \(x \ge D\), the equation (9.1.11) becomes

$$
u(x) = (h - c)x + cD + \inf_{\eta \ge K} [K \mathbf{I}_{\eta > x} + z(\eta - D)].$$

But from Lemma 9.2 we have

$$z(x - D) \le K + z(\eta - D), \forall x < \eta,$$

hence

$$
u(x) = (h - c)x + cD + z(x - D),$$

Recalling the definition of \(z(x)\) we deduce (9.1.15). This concludes the proof.

# **Lemma 9.3.** We have the property

```
\(\alpha u(0) \le u(0) \le cD.\)
```

PROOF. We have \(\alpha u(0) = z(0)\). Now from (9.1.13)

$$
u(0) = cD = K + \inf_{\eta \ge 0} z(\eta).$$

But \(\inf_{\eta \ge 0} z(\eta)\) is attained at a point \(\eta^* \ge 0\). But from Lemma 9.2, we have

$$z(0) \le K + z(\eta^*),$$

and the result follows. 

We can now assert the main result