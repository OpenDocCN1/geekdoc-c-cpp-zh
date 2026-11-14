**Remark 10.1.** Let \( J_{\alpha, x}(v(\cdot)) \) be the cost functional with discount \(\alpha\) for a controlled Markov chain, with control defined by a feedback \( v(\cdot) \) belonging to \( \mathcal{U}_b \). From Ergodic Theory we can claim that

```
(10.2.34) \( (1 - \alpha) J_{\alpha, x}(v(\cdot)) \to \int l(\xi, v(\xi)) m_{e(\cdot)}(d\xi). \)
```

Therefore we have also

```
(10.2.35) \( \rho = \inf_{v(\cdot) \in \mathcal{U}_b} \lim_{n \to \infty} (1 - \alpha) J_{\alpha, x}(v(\cdot)). \)
```

Let us also give the interpretation of the function \( u(x) \). Let us pick a feedback in \( \mathcal{U}_b \). Let us denote by \( y_n, v_n \) the corresponding trajectory, with

```
\( y_{n+1} = (y_n + v_n - D_n)^+ \quad v_n = v(y_n); \quad y_1 = x. \)
```

# **Lemma 10.2.** We have the property

```
(10.2.36) \( Eu(y_n) \to \int u(x) m_{e(\cdot)}(dx). \)
```

**PROOF.** The integral is well defined because the function \( u(x) \) is continuous and the range of \( m_{e(\cdot)}(dx) \) is \( [0, M] \). In fact (10.2.36) will hold for any continuous function. By taking positive and negative parts of \( u(x) \) we may as well assume that \( u(x) \ge 0 \). Consider the sequence \( u_\epsilon(x) = \frac{u(x)}{1 + \epsilon u(x)} \). We note that \( 0 \le y_n \le \max(x, M) \). So \( Eu(y_n) < \infty \) and we can write

```
(10.2.37) \( Eu(y_n) = Eu(y_n) + \epsilon \frac{u^2(y_n)}{1 + \epsilon u(y_n)}. \)
```

and \( \frac{u^2(y_n)}{1 + \epsilon u(y_n)} \le C = \max_{\xi \in [0, \max(x, M)]} u^2(\xi) \). If the initial inventory \( x > M \), we note that

```
\( \{y_{n+1} > M\} = \{D_1 + \cdots + D_n < x - M\}. \)
```

Therefore

```
\( P(\{y_{n+1} > M\}) = F^{(n)}(x - M) \le F^n(x - M). \)
```

Now

```
\( \limsup_{n \to \infty} Eu_\epsilon(y_n) = \limsup_{n \to \infty} Eu_\epsilon(y_{n+n_0}) \le \frac{1}{\epsilon} P(y_{n_0} > M) + \limsup_{n \to \infty} E I_{\{y_{n_0} \le M\}} u_\epsilon(y_{n+n_0}). \)
```

From Ergodic Theory, using the fact that \( u_\epsilon(x) \) is bounded (by \( \frac{1}{\epsilon} \)) we have

```
\( E I_{\{y_{n_0} \le M\}} u_\epsilon(y_{n+n_0}) \to \int u_\epsilon(x) m_{e(\cdot)}(dx), \quad \text{as } n \to \infty. \)
```

Therefore

```
\( \limsup_{n \to \infty} Eu_\epsilon(y_n) \le \int u_\epsilon(x) m_{e(\cdot)}(dx) + \frac{1}{\epsilon} P(y_{n_0} > M). \)
```

Letting \( n_0 \to \infty \) we obtain

```
\( \limsup_{n \to \infty} Eu_\epsilon(y_n) \le \int u_\epsilon(x) m_{e(\cdot)}(dx). \)
```

On the other hand, we have also

```
\( \liminf_{n \to \infty} Eu_\epsilon(y_n) = \liminf_{n \to \infty} Eu_\epsilon(y_{n+n_0}) \ge \liminf_{n \to \infty} E I_{\{y_{n_0} \le M\}} u_\epsilon(y_{n+n_0}). \)
```