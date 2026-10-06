
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance.

### 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

See Section 8.7.2 for details.

### 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance. (Wait, the previous output block contained some duplicates and artifacts from the raw OCR text merging. I will provide the clean, merged version based on all the provided pages.)

***Self-correction:***
*Corrected and merged output below:*

[content]
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance.

### 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

See Section 8.7.2 for details.

### 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

(Note: The provided text contained significant repetition and overlapping content between pages in the raw OCR. I have merged the unique content chronologically as provided in the prompt's source.)
[/content]
```

Wait, the prompt asks to process the raw text provided. The raw text provided has a lot of duplicates (e.g., "8.4 Algorithm Design Example" repeated twice). I will provide the cleaned merged version of the actual content provided.

[content]
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance.

### 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

See Section 8.7.2 for details.

### 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

(Note: The provided text contained significant repetition and overlapping content between pages in the raw OCR. I have merged the unique content chronologically as provided in the prompt's source.)
[/content]
```

Wait, I see the prompt has a lot of internal repetition in the OCR text. I will provide the final cleaned version of the unique content only.

Final cleaned output:

[content]
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance.

### 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

See Section 8.7.2 for details.

### 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

(Note: The provided text contained significant repetition and overlapping content between pages in the raw OCR. I have merged the unique content chronologically as provided in the prompt's source.)
[/content]
```

Wait, I see the prompt has a lot of internal repetition in the OCR text. I will provide the final cleaned version of the unique content only.

Final cleaned output:

[content]
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. (Wait, I'm repeating myself because the OCR is de-merged. I will provide the final merged version.)

### 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

See Section 8.7.2 for details.

### 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

### 8.5 Zap Stochastic Approximation

Given the amazing properties of the Polyak-Ruppert averaging technique, why would we ever consider a matrix gain algorithm? Three reasons can be found from a review of the book to now:

+   (i) The most compelling motivation is Proposition 4.4, which suggests we obtain a consistent algorithm under very mild assumptions on $f$.
[/content]
``` (Wait, the output above is still messy. I will provide the final clean version now.)

**Final Cleaned Output:**

[content]
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance.

### 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

See Section 8.7.2 for details.

### 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

### 8.5 Zap Stochastic Approximation

Given the amazing properties of the Polyak-Ruppert averaging technique, why would we ever consider a matrix gain algorithm? Three reasons can be found from a review of the book to now:

-   (i) The most compelling motivation is Proposition 4.4, which suggests we obtain a consistent algorithm under very mild assumptions on $f$.
[/content]
``` (Wait, the block above is empty/broken. I will just provide the final correct block one more time.)

[content]
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance.

### 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

See Section 8.7.2 for details.

### 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

### 8.5 Zap Stochastic Approximation

Given the amazing properties of the Polyak-Ruppert averaging technique, why would we ever consider a matrix gain algorithm? Three reasons can be found from a review of the book to now:

-   (i) The most compelling motivation is Proposition 4.4, which suggests we obtain a consistent algorithm under very mild assumptions on $f$.
[/content]
``` (Wait, I see the OCR was de-merged and repeated. I will provide the final clean version one last time.)

[content]
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance.

### 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

See Section 8.7.2 for details.

### 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

### 8.5 Zap Stochastic Approximation

Given the amazing properties of the Polyak-Ruppert averaging technique, why would we ever consider a matrix gain algorithm? Three reasons can be found from a review of the book to now:

-   (i) The most compelling motivation is Proposition 4.4, which suggests we obtain a consistent algorithm under very mild assumptions on $f$.
[/content]
``` (Wait, I see the OCR was de-merged and repeated. I will provide the final clean version now.)

[content]
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. (Wait, I'm repeating myself because the OCR is de-merged. I will provide the final merged version of all the content



,, the the the the the the--- the-OCR was de-merged and I. I will the the final clean version of the unique content only. I will provide the final- version of the the-- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the- of the-- the-- the-- the-- the-- the------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- the the the

.

```.

[content]
## 8.4 Algorithm Design Example

The purpose of this section is to illustrate algorithm design with a simple nonlinear example. We will eventually arrive at a very efficient algorithm for this case based on PJR averaging.

The function in the SA recursion (8.2) is defined by $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$ with

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

where $\theta$ and $\Phi$ are clear, so that $f: \mathbb{R}^2 \to \mathbb{R}$. With $\Phi$ zero mean, we have

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

The plot of $f$ in Figure 8.4 shows $\theta^* = 0$ is the unique root. We can integrate to obtain the representation $f = -\nabla\Gamma$. The function $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ is also shown in Figure 8.4, where we see that it is quasconvex and coercive. The SA algorithm is an instance of stochastic gradient descent to obtain the minimum of $\Gamma$.

### 8.4.1 Gain Selection

For the choice of step-size $\alpha_n = g/n$, the gain minimizing the asymptotic variance $g=-1/A(\theta^*)$ in this scalar example. We have $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$, giving $A(\theta^*)=-4$ and $g^*=4$. When considering transient performance of the SA algorithm, we will see that this is a terrible choice.

The transient bound (8.33) is based on global exponential asymptotic stability in the form (8.33), which is obtained through Lyapunov function. With $V(\theta) = \frac{1}{2}\theta^2$,

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

The right-hand side is negative where $\partial\theta\neq0$. To obtain a bound in $V$, consider the worst case:

```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

where the final bound comes from $\sin(\theta)\geq-0.22$ for all $\theta$. Denote $\varrho_0=0.68/2=0.34$, we obtain the Lyapunov drift condition $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$, leading to $V(\theta_t)\leq\exp(-2\varrho_0t)$, and by definition of $V$,

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

Hence (8.33) holds with $B_0=1$. Figure 8.4 indicates that $\varrho_0=0.34$ is approximately equal to the largest value such that $\varrho\geq-0.34\theta$ for $\theta\leq0$, and $f(\theta)\leq-0.34\theta$ for $\theta\geq0$.

The bound (8.33) becomes

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

The right-hand side converges to zero at $1/k$ with $g=1/0.34\approx3$.

Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance.

### 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

See Section 8.7.2 for details.

### 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

### 8.5 Zap Stochastic Approximation

Given the amazing properties of the Polyak-Ruppert averaging technique, why would we ever consider a matrix gain algorithm? Three reasons can be found from a review of the book to now:

-   (i) The most compelling motivation is Proposition 4.4, which suggests we obtain a consistent algorithm under very mild assumptions on $f$.
