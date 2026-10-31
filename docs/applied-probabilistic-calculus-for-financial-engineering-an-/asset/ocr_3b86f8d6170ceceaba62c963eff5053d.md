Hence, the Ito integral $\int_0^T \varepsilon(t) dB(t)$ is defined as the sum

$\int_0^T \varepsilon(t) dB(t) = \sum_{i=0}^{n-1} c_i \{B(t_{i+1}) - B(t_i)\}$
(3.218)

The Ito integral of simple processes is a random variable with the following four properties:

# Property 1. Linearity:

If $X(t)$ and $Y(t)$ are simple processes and $\alpha$ and $\beta$ are constants, then

$\int_0^T [\alpha X(t) + \beta Y(t)] dB(t) = \alpha \int_0^T X(t) dB(t) + \beta \int_0^T Y(t) dB(t)$
(3.219)

# Property 2.

The integral of the indicator function of an interval $I_{[a,b]}(t)=1$ when $t \in [a,b]$, and zero otherwise, is just $B(b) - B(a)$, $0<a<b<T$,

$\int_0^T I_{[a,b]}(t) dB(t) = B(b) - B(a)$
(3.220)

# Property 3. Zero mean property:

$E\left[\int_0^T X(t) dB(t)\right] = 0$
(3.221)

# Property 4. Isometry property:

$E\left[\int_0^T X(t) dB(t)\right]^2 = E\left[\int_0^T X^2(t) dt\right]$
(3.222)

The definition of the Ito integral may be extended to processes $X(t)$ that may be approximated by sequences $\varepsilon^n$ of simple processes in the sense that

$E\left[\int_0^T (\varepsilon^n(t) - X(t))^2 dt\right] \to 0$
(3.223)

as $n \to \infty$. In that case, one defines

$\int_0^T X(t) dB = \lim_{n \to \infty} \int_0^T \varepsilon^n t dB$
(3.224)

In this definition, the limit does not depend on the approximating sequence. Also, the integral that arises this way satisfies Properties 1–4.