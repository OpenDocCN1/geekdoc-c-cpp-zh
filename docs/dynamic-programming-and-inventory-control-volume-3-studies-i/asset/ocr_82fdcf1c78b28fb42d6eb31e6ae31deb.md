hence

```
(15.6.14) \limsup \int_s^{+\infty} m(\varphi_s - \varphi^o)^2 dx \le \int_s^{+\infty} m \varphi^o \varphi dx - \int_s^{+\infty} m(\varphi^o)^2 dx.
```

Noting that \(\sqrt{\epsilon}\varphi_\epsilon\) remains bounded in \(L^2_n(R)\), it follows from the equation of \(\varphi_\epsilon\) that

```
\epsilon \int_s^{+\infty} A \varphi_\epsilon z dx \to 0, \forall z \text{ smooth with compact support in } (s, +\infty),
```

therefore we deduce immediately that \(\varphi^o = \varphi\) and from (15.6.14) the property (15.6.22) is obtained, which completes the proof.

# 15.6.3. ERGODICITY.

The result of Theorem 15.4, although sufficient to study ergodic control and the limit of Bellman equation, as we shall see in the next sections, does not prove full ergodicity. To complete we need to prove the

# Theorem 15.5. We have the property

```
(15.6.15) \( E \varphi(y_s^{x,S}(t)) \to \int_s^{+\infty} E \varphi(\xi) m^{s,S}(d\xi), \text{ as } t \to +\infty, \forall x, \forall \varphi \text{ bounded.} \)
```

PROOF. We shall use the fact that

```
\( z^{s,S}(x,t) = E \varphi(y_s^{x,S}(t)), \)
```

is the solution of the Cauchy problem

```
(15.6.16) \begin{align*} \frac{\partial z}{\partial t} + Az &= 0, \quad x > s \\ z(x,t) &= z(S,t), \quad x \le s, t > 0 \\ z(x,0) &= \varphi(x) \end{align*}
```

We proceed with estimates. We first derive an energy equality. By testing (15.6.16) with \(mz\) and making use of Lemma 15.5.2 we can state

```
(15.6.17) \begin{align*} \frac{1}{2} \frac{d}{dt} \int_s^{+\infty} m(x) z^2(x,t) dx + \frac{1}{2} \int_s^{+\infty} \sigma^2 m \left( \frac{\partial z}{\partial x} \right)^2 dx \\ + \frac{\lambda}{2} \int_s^{+\infty} \int_0^{+\infty} m(x) (z(x) - z(x - \xi))^2 \mu(d\xi) dx d\xi = 0 \end{align*}
```

We deduce the estimates

```
(15.6.18) \int_0^{+\infty} \int_s^{+\infty} \sigma^2 m \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx dt \le \int_s^{+\infty} m(x) \varphi^2(x) dx
```

```
(15.6.19) \lambda \int_0^{+\infty} \int_s^{+\infty} \int_0^{+\infty} m(x) (z(x) - z(x - \xi))^2 \mu(d\xi) dx d\xi dt \le \int_s^{+\infty} m(x) \varphi^2(x) dx.
```

Also

```
(15.6.20) \int_s^{+\infty} m(x) z^2(x,t) dx \le \int_s^{+\infty} m(x) \varphi^2(x) dx, \forall t.
```

This inequality implies that without loss of generality we may assume that \(\varphi\) is in the domain of \(A\). Indeed considering the approximation \(\varphi_\epsilon\) defined in Lemma