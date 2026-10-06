# 4.5 Quasistochastic Approximation

The probing signal is deterministic in the QSA developed in this chapter. Two canonical choices with $\Omega \subset \mathbb{R}^m$ are the $m$-dimensional mixtures of periodic functions:

```
$\Xi_d = \sum_{i=1}^K v^i[\phi_i + \omega_i t]_{(\text{mod } 1)} \quad (4.46a)$
```

```
$\Xi_d = \sum_{i=1}^K v^i\sin(2\pi[\phi_i + \omega_i t]) \quad (4.46b)$
```

for fixed $K \geq 1$, vectors $\{v^i\ \subset \mathbb{R}^m$, phases $\{\phi_i\\}$, and frequencies $\{\omega_i\}$. Such signals have well-defined steady-state mean and covariances. Consider example (4.46b) in the special case

```
$\Xi_d(i) = \sqrt{2}\sin(\omega_i t), \quad 1 \leq i \leq m \quad (4.47)$
```

with $\omega_i \neq \omega_j$ for all $i \neq j$. The steady-state mean and covariance then satisfy

```
$\lim_{T\to\infty} \frac{1}{T} \int_0^T \Xi_d \ dt = 0, \quad (4.48a)$
```

```
$\lim_{T\to\infty} \frac{1}{T} \int_0^T \Xi_d^2 \ dt = 1, \quad (4.48b)$
```

where $1$ is the identity matrix.\nFor a function $g: \mathbb{R}^K \to \mathbb{R}$, we can expect the following asymptotic independence, provided the frequencies $\{\omega_i\}$ are distinct:

```
$\lim_{T\to\infty} \frac{1}{T} \int_0^T g(2\pi[\phi_1 + \omega_1 t]), \dots,sin(2\pi[\phi_K + \omega_K t]) \ dt =\n= \int_0^1 \dots\int_0^1 g(2\pi[\phi_1 + \omega_1 t_1]), \dots,sin(2\pi[\phi_K + \omega_K t_K]) \ dt_1 \dots dt_K. \quad (4.49)$
```

See Lemma 4.37 for a precise statement about another general class of probing signals.\nThe following subsections contain examples to illustrate theory of QSA, and also a glimpse at applications

# 4.5.1 Quasi Monte-Carlo

Consider the problem of integrating over the interval $[0, 1]$ of a function $y: \mathbb{R} \to \mathbb{R}$. In a standard Monte-Carlo approach we would draw independent random variables $\{\Phi(k)\}$, with distribution uniform on the interval $[0,1]$, and then:

```
$\theta_n = \frac{1}{n} \sum_{k=0}^{n-1} y(\Phi(k)). \quad (4.50)$
```

In a QSA approach, the probing signal is the one-dimensional sawtooth function, $\Xi_d \equiv t$ (modulo 1), and estimates are defined by the average

```
$\Theta_t = \frac{1}{t} \int_0^t y(\Xi_r) dr. \quad (4.51)$
```