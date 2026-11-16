![](bbox=[0.102, 0.083, 0.891, 0.463])

Figure 14.3 Prior and transition Bayesian networks, in the case where the networks in different time slots are connected only through non-evidence variables, are in (a). The resultant dynamic Bayesian network for T = 2 is in (b).

Let e[t] be the set of values of the evidence variables at time step t, and let f[t] be the set of values of the evidence variables up to and including time step t. Suppose for each value x[t] of X[t] we know

```
P(x[t]|f[t]).
```

We want to now compute P(x[t + 1]|f[t + 1]). First, we have

```
P(x[t + 1]|f[t]) = \sum_{x[t]} P(x[t + 1]|x[t], f[t])P(x[t]|f[t]).
= \sum_{x[t]} P(x[t + 1]|x[t])P(x[t]|f[t]). (14.2)
```

Using Bayes' theorem, we then have

```
P(x[t + 1]|f[t + 1]) = P(x[t + 1]|f[t], e[t + 1])
= \alpha P(e[t + 1]|x[t + 1], f[t])P(x[t + 1]|f[t])
= \alpha P(e[t + 1]|x[t + 1])P(x[t + 1]|f[t]), (14.3)
```