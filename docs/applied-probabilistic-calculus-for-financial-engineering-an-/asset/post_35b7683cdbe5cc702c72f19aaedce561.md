
represented as a function of $S$ and $t$. The $B$ in $dB$ denotes Brownian motion, which will be described in the next section. It is important to note that $\mu$ and $\sigma$ may be estimated for individual stocks using statistical analysis of historical prices. It is important that $\mu$ and $\sigma$ are functions of $S$ and $t$. Combining this information together, one obtains the stochastic differential equation

$$
dS/S = \mu\,dt + \sigma\,dB \tag{3.210}
$$

Notice that if the volatility $\sigma$ is zero the model implies

$$
dS/S = \mu\,dt \tag{3.211}
$$

When $\mu$ is constant this equation can be solved so that

$$
S = S_0 e^{\mu t} \tag{3.212}
$$

where $S$ is the price of the stock at $t$ and $S_0$ is the price of the stock at $t = 0$. This equation shows that when the variance of an asset is zero, the asset grows at a continuously compounded rate of $\mu$ per unit of time.

## Brownian Motion

The term Brownian motion, which was originally used as a model for stock price movements in 1900 by L. Bachelier [Klebaner, 1998], is a stochastic process $B(t)$ characterized by the following three properties:

- **1. Normal Increments:** $B(t) - B(s)$ has a normal distribution with mean 0 and variance $t - s$. Thus, if $s = 0$, $B(t) - B(0)$ has a normal distribution with mean 0 and variance $t - 0 = t$.
- **2. Independence of Increments:** $B(t) - B(s)$ is independent of the past.
- **3. Continuity of Paths:** $B(t)$, $t \ge 0$, are continuous functions of $t$.

These three properties alone define Brownian motion, but they also show why Brownian motion is used to model stock prices. Property (2) shows stock price changes will be independent of past price movements. This was an important assumption made in this stock price model.

An occurrence of Brownian motion from time 0 to T is called a path of the process on the interval $[0, T]$. There are five important properties of Brownian motion paths. The path $B(t)$, $0 \le t \le T$

- **1.** is a continuous function of $t$,
- **2.** is not monotonic on any interval, no matter how small the interval is,
- **3.** is not differentiable at any point,
- **4.** has infinite variation on any interval no matter how small it is,
- **5.** has quadratic variation on $[0,t]$ equal to $t$, for any $t$.

Together, Properties (1) and (3) state that although Brownian motion paths are continuous, the $\Delta B(t)$ over interval $\Delta t$ is much larger than $\Delta t$ as $\Delta t \to 0$. Properties (4) and (5) show the distinction between functions of Brownian motion and normal, smooth functions. The variation of a function over the

Hence, the Ito integral

$$
\int_0^T \varepsilon(t)\,dB(t)
$$

is defined as the sum

$$
\int_0^T \varepsilon(t)\,dB(t) = \sum_{i=0}^{n-1} c_i \{B(t_{i+1}) - B(t_i)\} \tag{3.218}
$$

The Ito integral of simple processes is a random variable with the following four properties:

- **Property 1. Linearity:** If $X(t)$ and $Y(t)$ are simple processes and $\alpha$ and $\beta$ are constants, then

$$
\int_0^T [\alpha X(t) + \beta Y(t)]\,dB(t) = \alpha \int_0^T X(t)\,dB(t) + \beta \int_0^T Y(t)\,dB(t) \tag{3.219}
$$

- **Property 2.** The integral of the indicator function of an interval $I_{[a,b]}(t) = 1$ when $t \in [a,b]$, and zero otherwise, is just $B(b) - B(a)$, $0 < a < b < T$,

$$
\int_0^T I_{[a,b]}(t)\,dB(t) = B(b) - B(a) \tag{3.220}
$$

- **Property 3. Zero mean property:**

$$
E\left[\int_0^T X(t)\,dB(t)\right] = 0 \tag{3.221}
$$

- **Property 4. Isometry property:**

$$
E\left[\left(\int_0^T X(t)\,dB(t)\right)^2\right] = E\left[\int_0^T X^2(t)\,dt\right] \tag{3.222}
$$

The definition of the Ito integral may be extended to processes $X(t)$ that may be approximated by sequences $\varepsilon^n$ of simple processes in the sense that

$$
E\left[\int_0^T (\varepsilon^n(t) - X(t))^2\,dt\right] \to 0 \tag{3.223}
$$

as $n \to \infty$. In that case, one defines

$$
\int_0^T X(t)\,dB(t) = \lim_{n \to \infty} \int_0^T \varepsilon^n(t)\,dB(t) \tag{3.224}
$$

In this definition, the limit does not depend on the approximating sequence. Also, the integral that arises this way satisfies Properties 1–4.

Now that one has defined the Ito integral of simple processes, one may define the Ito integrals of other processes. It may be shown that if a general predictable process satisfies certain conditions, the general process is a limit in probability of simple predictable processes discussed earlier. The Ito integral of general predictable processes is defined as a limit of integrals of simple processes. If $X(t)$ is a predictable process such that

$$
\int_{0}^{T} X^{2}(t)\,dt < \infty \tag{3.225}
$$

then the Ito integral

$$
\int_{0}^{T} X(t)\,dB(t)
$$

is defined and satisfies the above four properties.

For example, to evaluate the integral

$$
\int_{0}^{T} B(t)\,dB(t)
$$

one may let $0 = t_{0} < t_{1} < t_{2} < \cdots < t_{n} = T$ be a partition of $[0, T]$, then

$$
\varepsilon^{n}(t) = \sum_{i=0}^{n-1} B(t_{i}) I_{[t_{i},t_{i+1})}(t) \tag{3.226}
$$

Then, for any $n$, $\varepsilon^{n}(t)$ is a simple process. One may take a sequence of the partitions such that $\max_{i}(t_{i+1} - t_{i}) \to 0$ as $n \to \infty$. The Ito integral of this simple function is given by

$$
\int_{0}^{T} \varepsilon^{n}(t)\,dB(t) = \sum_{i=0}^{n-1} B(t_{i})\big[ B(t_{i+1}) - B(t_{i}) \big] \tag{3.227}
$$

One may show that this sequence of integrals converges in probability and identify the limit. Adding and subtracting $B^{2}(t_{i+1})$, one obtains

$$
B(t_{i})\big[ B(t_{i+1}) - B(t_{i}) \big] = \frac{1}{2}\Big[ B^{2}(t_{i+1}) - B^{2}(t_{i}) - \{ B(t_{i+1}) - B(t_{i}) \}^{2} \Big] \tag{3.228}
$$

and

$$
\int_{0}^{T} \varepsilon^{n}(t)\,dB(t) = \frac{1}{2}\sum_{i=0}^{n-1}\big[ B^{2}(t_{i+1}) - B^{2}(t_{i}) \big] - \frac{1}{2}\sum_{i=0}^{n-1}\big\{ B(t_{i+1}) - B(t_{i}) \big\}^{2} \tag{3.229}
$$

$$
= \frac{1}{2}B^{2}(T) - \frac{1}{2}B^{2}(0) - \frac{1}{2}\sum_{i=0}^{n-1} \{B(t_{i+1}) - B(t_i)\}^2 \tag{3.230}
$$

since the first sum is a telescopic sum. Notice that from property 5 of Brownian motion path, the second sum converges to the limit $T$. Therefore, $\int_{0}^{T} \varepsilon^{n}(t)\,dB(t)$ converges, and the limit is

$$
\int_{0}^{T} B(t)\,dB(t) = \lim_{n\to\infty} \int_{0}^{T} \varepsilon^{n}(t)\,dB(t) = \frac{1}{2}B^{2}(T) - \frac{1}{2}T \tag{3.231}
$$

This example illustrates the difference between deterministic calculus and stochastic calculus. The quadratic variation of continuous functions, $x(t)$, of finite variation in standard calculus is 0. Therefore, if one were calculating the integral of $\int_{0}^{T} x(t)\,dx(t)$ the same way as above, the term $\sum_{i=0}^{n-1} \{x(t_{i+1}) - x(t_i)\}^2$ would tend to the limit 0. Thus, the integral $\int_{0}^{T} x(t)\,dx(t)$ equals $\frac{1}{2}x^{2}(T)$.

Now consider the main tool of stochastic calculus: Ito's formula, which is the stochastic counterpart of the chain rule in Calculus. Recall that Brownian motion has quadratic variation on $[0, t]$ equal to $t$, for any $t$. This also may be expressed as the following:

$$
\int_{0}^{t} \{dB(s)\}^2 = \int_{0}^{t} ds = t \quad \text{or, in differential notation,} \quad \{dB(t)\}^2 = dt \tag{3.232}
$$

Using this property and applying Taylor's formula, Ito's formula states that if $f(x)$ is a twice-differentiable function, then for any $t$

$$
f[B(t)] = f(0) + \int_{0}^{t} f'[B(s)]\,dB(s) + \frac{1}{2}\int_{0}^{t} f''[B(s)]\,ds \tag{3.233}
$$

and Ito's formula in differential notation becomes

$$
d\{f(B(t))\} = f'[B(t)]\,dB(t) + \frac{1}{2}f''[B(t)]\,dt \tag{3.234}
$$

## The Ito Process

Next, one defines an Ito process: Let $Y(t)$ be an Ito integral, defined as

$$
Y(t) = \int_{0}^{t} X(s)\,dB(s) \tag{3.235}
$$

Then, an Ito process is an Ito integral plus an adapted continuous process of finite variation. A process $Y$ is called an Ito Process if for any $0 \le t \le T$ it can be represented as

$$
Y(t) = Y(0) + \int_{0}^{t} \mu(s)\,ds + \int_{0}^{t} \sigma(s)\,dB(s) \tag{3.236}
$$

More generally, if $Y$ is an Ito process represented above, then it has a stochastic differential on $[0, T]$ given by

$$
dY(t) = \mu(t)\,dt + \sigma(t)\,dB(t) \tag{3.237}
$$

for $0 \le t \le T$. The function $\mu$ is often called the drift coefficient and the function $\sigma$ is called the diffusion coefficient—terms inherited from studies in mass and energy transfers in areas within classical physics and engineering.

One last important case to consider is for functions of the form $f(X(t), t)$. If $f(x, t)$ is a twice continuously differentiable function in $x$, as well as continuously differentiable in $t$, and $X(t)$ represents an Ito process, then

$$
df[x(t), t] = \frac{\partial f}{\partial x}(X(t), t)\,dX(t) + \frac{\partial f}{\partial t}(X(t), t)\,dt + \frac{1}{2}\sigma^{2}(X(t), t)\frac{\partial^{2} f}{\partial x^{2}}(X(t), t)\,dt \tag{3.238}
$$

This case of Ito's formula may be used to compute the Black–Scholes partial differential equation in the next section.

## Derivation of the Black–Scholes Equation

Here, the price of a derivative security, $V(S, t)$, will be derived. The model for a stock derived previously satisfies an Ito process defined in (3.237).

$$
dY(t) = \mu(t)\,dt + \sigma(t)\,dB(t) \tag{3.237}
$$

Therefore, one may let the function $V(S, t)$ be twice differentiable in $S$ and differentiable in $t$. Applying (3.238) one has

$$
dV(S, t) = \frac{\partial V}{\partial S}\,dS + \frac{\partial V}{\partial t}\,dt + \frac{1}{2}\sigma^{2}S^{2}\frac{\partial^{2} V}{\partial S^{2}}\,dt \tag{3.239}
$$

Substituting into (3.239) for $dS$ with (3.210), one has

$$
dS/S = \mu\,dt + \sigma\,dB \tag{3.210}
$$

$$
dV(S, t) = \frac{\partial V}{\partial S}(\mu S\,dt + \sigma S\,dB) + \frac{\partial V}{\partial t}\,dt + \frac{1}{2}\sigma^{2}S^{2}\frac{\partial^{2} V}{\partial S^{2}}\,dt \tag{3.240}
$$

This simplifies to

$$
dV(S, t) = \sigma S\,dB\frac{\partial V}{\partial S} + \left\{\mu S\frac{\partial V}{\partial S} + \frac{\partial V}{\partial t} + \frac{1}{2}\sigma^{2}S^{2}\frac{\partial^{2} V}{\partial S^{2}}\right\}dt \tag{3.241}
$$
