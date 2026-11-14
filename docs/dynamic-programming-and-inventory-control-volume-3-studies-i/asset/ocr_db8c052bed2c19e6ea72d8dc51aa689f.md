The intermediary results (15.6.43), (15.6.26), (15.6.27), (15.6.28) will be proved later. We now assume \(\varphi(x)\) continuous and bounded. We want to prove that

```
(15.6.29) 
\(z(x, t) \to \int_s^{+\infty} m(x)\varphi(x)dx \text{ as } t \to +\infty, \forall x.\)
```

It is sufficient to assume \(x > s\). So let us pick \(x_0 > s\). Using \(z(x, t) = E\varphi(y_x(t))\) we can write

```
\(E\varphi(y_{x_0}(t)) - \int m\varphi dx = E\varphi(y_{x_0}(t)) - E\varphi_\epsilon(y_{x_0}(t)) + E\varphi_\epsilon(y_{x_0}(t)) - \int m\varphi_\epsilon dx + \int m\varphi_\epsilon dx - \int m\varphi dx.\)
```

Now for \(R > x_0\) we have

```
\(|E\varphi(y_{x_0}(t)) - E\varphi_\epsilon(y_{x_0}(t))| \le 2||\varphi|| E\mathbf{I}_{y_x(t) \ge R} + \sup_{s \le x \le R} |\varphi_\epsilon(x) - \varphi(x)|,\)
```

hence

```
\(\left| E\varphi(y_{x_0}(t)) - \int m\varphi dx \right| \le 2||\varphi|| E\mathbf{I}_{y_x(t) \ge R} + \sup_{s \le x \le R} |\varphi_\epsilon(x) - \varphi(x)| + \left| E\varphi_\epsilon(y_{x_0}(t)) - \int m\varphi_\epsilon dx \right| + \left| \int m\varphi_\epsilon dx - \int m\varphi dx \right|.\)
```

Since \(\varphi\), belongs to the domain of \(A\), fixing \(\epsilon\) and \(R\), we can let \(t \to +\infty\) and deduce

```
\(\limsup_{t \to +\infty} \left| E\varphi(y_{x_0}(t)) - \int m\varphi dx \right| \le 2||\varphi|| \sup_{t \ge \delta} E\mathbf{I}_{y_x(t) \ge R} + \sup_{s \le x \le R} |\varphi_\epsilon(x) - \varphi(x)| + \left| \int m\varphi_\epsilon dx - \int m\varphi dx \right|.\)
```

But then letting \(\epsilon \to 0\), then \(R \to +\infty\) and making use of properties (15.6.26), (15.6.28) the right hand side tends to 0. So the property (15.6.15) is fully proven.

# PROOF OF INTERMEDIARY RESULTS:

# PROOF OF REGULARITY:

We know that

```
(15.6.30) \(|z(x, t)| \le ||\varphi||, \int_0^{+\infty} \int_s^{+\infty} m(x) \left( \frac{\partial z}{\partial x} \right)^2 (x, t) dx dt \le \frac{1}{\sigma^2} ||\varphi||^2 \int_0^{+\infty} \int_s^{+\infty} \int_0^{+\infty} m(x)(z(x) - z(x - \xi))^2 \mu(\xi) d\xi dx dt \le \frac{1}{\lambda} ||\varphi||^2\)
```