and we recognize as expected

```
$$\zeta_S(S; \varphi) = \frac{2}{\sigma^2} \int_s^{+\infty} \varphi(x)\bar{m}^{s,S}(x)dx.$$
```

The result follows.

We now present a useful result

# **Lemma 15.2.** For any \(z \in domain\) of \(A\), we have the equality

```
$$(15.6.12) \quad \int_s^{+\infty} m(x)z(x)Az(x)dx = \frac{1}{2} \int_s^{+\infty} \sigma^2 m z'^2 dx + \frac{\lambda}{2} \int_s^{+\infty} \int_0^{+\infty} m(x)(z(x) - z(x - \xi))^2 \mu(\xi) dx d\xi .$$
```

PROOF. We consider the quantity on the left hand side. Since we will perform two integration by parts, we have to be careful that \(m'\) is discontinuous in \(S\). On the other hand \(z'\) is continuous in \(S\).

After one integration by parts we can write

```
$$\int_s^{+\infty} m(x)z(x)Az(x)dx = \frac{1}{2} \int_s^S \sigma^2 m z'^2 dx + \int_s^S zz' \left( \frac{\sigma^2}{2} m' + \nu m \right) dx + \lambda \int_s^{+\infty} \int_0^{+\infty} m(x)z(x)(z(x) - z(x - \xi)) \mu(\xi) dx d\xi .$$
```

Noting that

```
$$zz' = \frac{1}{2}(z^2)' ,$$
```

we can perform a second integration by parts which leads to

```
$$\int_s^S zz' \left( \frac{\sigma^2}{2} m' + \nu m \right) dx = -\frac{1}{2} \int_s^{+\infty} z^2 \left( \frac{\sigma^2}{2} m' + \nu m' \right) dx + + \frac{\sigma^2}{4} z^2(S)(m'(S-0) - m'(S+0) - m'(s)) .$$
```

The next step is to consider

```
$$\int_s^{+\infty} \int_0^{+\infty} m(x)z(x)(z(x) - z(x - \xi)) \mu(\xi) dx d\xi = \frac{1}{2} \int_s^{+\infty} \int_0^{+\infty} m(x)(z(x) - z(x - \xi))^2 \mu(\xi) dx d\xi + \frac{1}{2} \int_s^{+\infty} \int_0^{+\infty} m(x)(z^2(x) - z^2(x - \xi)) \mu(\xi) dx d\xi .$$
```

We also use

```
$$\int_s^{+\infty} \int_0^{+\infty} m(x)z^2(x - \xi) \mu(\xi) dx d\xi = \int_s^{+\infty} \int_0^{+\infty} m(x + \xi) z^2(x) \mu(\xi) dx d\xi + z^2(S) \int_s^{+\infty} \int_0^{+\infty} m(x + \xi) \mu(\xi) dx d\xi .$$
```

Collecting results and making use of the equation of the invariant measure, see (15.6.6), (15.6.7) we obtain many simplifications. Eventually we obtain (15.6.14)