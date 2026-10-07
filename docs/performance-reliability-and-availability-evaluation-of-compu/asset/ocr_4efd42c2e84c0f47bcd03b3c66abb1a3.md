# 586 Performance, Reliability, and Availability Evaluation of Computational Systems

# Exponential Distribution

Now let us assume a independent set of measures, a sample, $\{t_1, t_2, ..., t_n\}$, was collected from an exponentially distributed population with true but unknown parameter $\lambda$.

```
$f(t) = \lambda e^{-\lambda t}, \quad t \ge 0$.
```

The likelihood function considered to estimate the distribution parameter is represented by joint distribution with a $\hat{\lambda}$ that maximizes likelihood function for the sample $\{t_1, t_2, ..., t_n\}$. Therefore, as the set of measures of the sample are i.i.d., then

```
$L(\\lambda | t_1, t_2, ..., t_n) = f(t_1) \times f(t_2) \times ... \times f(t_n)$.
```

```
$L(\\lambda | t_1, t_2, ..., t_n) = \lambda e^{-\lambda t_1} \times \lambda e^{-\lambda t_2} \times ... \times \lambda e^{-\lambda t_n}$.
```

```
$L(\\lambda | t_1, t_2, ..., t_n) = \prod_{i=1}^{n} \lambda e^{-\lambda t_i}$.
```

```
$L(\\lambda | t_1, t_2, ..., t_n) = \lambda^n e^{-\lambda \sum_{i=1}^{n} t_i}; \quad (25.3.25)
```

Now let us take the $ln(\lambda | t_1, t_2, ..., t_n)$, then

```
$ln(\\lambda | t_1, t_2, ..., t_n)) = \ln(\lambda^n e^{-\lambda \sum_{i=1}^{n} t_i})$.
```

```
$ln(\\lambda | t_1, t_2, ..., t_n)) = \ln\lambda^n + \lambda \sum_{i=1}^{n} t_i$.
```

```
$ln(\\lambda | t_1, t_2, ..., t_n)) = n \ln\lambda - \lambda \sum_{i=1}^{n} t_i$.
```

```
$ln(\\lambda | t_1, t_2, ..., t_n)) = n \ln\lambda - \lambda \sum_{i=1}^{n} t_i; \quad (25.3.26)
```

Now, take the derivative of $ln(\lambda | t_1, t_2, ..., t_n))$ with respect to $\lambda$:

```
$\frac{\partial}{\partial\lambda}ln(\\lambda | t_1, t_2, ..., t_n)) = \frac{\partial (n \ln\lambda - \lambda \sum_{i=1}^{n} t_i)}{\partial\lambda}$,
```

thus

```
$\frac{\partial}{\partial\lambda}ln(\\lambda | t_1, t_2, ..., t_n)) = \frac{\partial n \ln\lambda}{\partial\lambda} - \frac{\partial \lambda \sum_{i=1}^{n} t_i}{\partial\lambda}$,
```

```
$\frac{\partial}{\partial\lambda}ln(\\lambda | t_1, t_2, ..., t_n)) = \frac{n}{\lambda} - \sum_{i=1}^{n} t_i$.
```