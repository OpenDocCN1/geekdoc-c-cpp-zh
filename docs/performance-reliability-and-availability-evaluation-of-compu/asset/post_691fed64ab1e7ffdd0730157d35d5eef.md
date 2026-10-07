
# Reliability Block Diagram

Now, consider the time to repair each component is also exponentially distributed. If the mean time to repair the hardware is $24h$, the mean time to repair the operating system is $8h$, and the respective times to repair the programs are $4h$, the steady-state availability can be estimated by

```
$A = \prod_{i\in{hw, os, a_1, a_2}} A_i,$
```

where $A_i = \mu_i/(\lambda_i + \mu_i) = MTTF / (MTTF + MTTR_i)$.

The steady-state availability is $A=0.99122$. The annual downtime in hours is $DTyh = (1 - A) \times 8760/h = 76.928h$. The system mean time to restore may be estimated from $A = MTTF / (MTTF + MTTR)$, because

```
$A \times (MTTF + MTTR) = MTTF.$
```

```
$A \times MTTR = MTTF - A \times MTTF.$
```

```
$MTTR = \frac{MTTF \times (1 - A)}{A} TR = \frac{MTTF \times UA}{A}, \quad (18.5.10)
```

where $UA$ is the steady-state unavailability.

Taking the steady-state availability, we have $UA = 1 - 0.99122 = 0.00878$. As $MTTF = 640h$, then $MTTR = (640 \times 0.00878)/(0.99122) = 5.67h$.

Assume the mean time to failure of the program $A_2$ may lay in the interval $(1000h, 2000h)$. The steady-state availability and yearly downtime in hours are depicted in Figure 18.7.

![](img/2d1450514bb14a0cdf0eb5048614afab_91_0.png)

**Example 18.5.2.** A system $S$ of 8 functions serially composed was conceived aiming at reliability not smaller than $0.9 (R(t) \ge 0.9)$ for mission time of $t = 400h$. If the functions' time to failure are independent and identically distributed (i.i.d.) according to an exponential distribution, what is the maximal failure rate allowed for each function?

The system reliability for an eight-component i.i.d. serial system is $R(t) = e^{-8\lambda t}$. Then,

```
$$\lambda = \frac{-Ln(R(t))}{8 \times t}$$
```

# Performance, Reliability, and Availability Evaluation of Computational Systems

![](img/2d1450514bb14a0cdf0eb5048614afab_92_0.png)

**Figure 18.7** Steady-State Availability (a) and Downtime (b) as Function of $MTTF_{a2}$ .

As $R(t) \geq 0.9$, then

$\lambda < \frac{-LnR(t)}{8 \times t}$

Hence

$\lambda < \frac{-Ln0.9}{8 \times 400} = 3.2925 \times 10^{-5} f/h$.

The required system mean time to failure is

$MTTF = \frac{1}{8 \times \lambda} = \frac{1}{2.63401 \times 10^{-4}} = 3796.49h$.

# Parallel Composition

Let us consider a system $S$ composed of $n$ components (see Figure 18.8). If the system is operational if at least one component $b_i$ is operational, the structure function is

$\Phi(X) = 1 - \prod_{i=1}^{n} (1 - x_i)$.

Since $\Phi(X)$ is a Bernoulli random variable, we have

$E(\Phi(X)) = P(\Phi(X)) = 1$.

![](img/2d1450514bb14a0cdf0eb5048614afab_93_0.png)

**Figure 18.8** Parallel Composition.

Hence,

$P(\Phi(\mathbf{X}) = 1) = E(1 - \prod_{i=1}^{n} (1 - x_i))$.

Assuming the components are independent, we have

$P(\Phi(\mathbf{X}) = 1) = 1 - E(\prod_{i=1}^{n} (1 - x_i))$.

$P(\Phi(\mathbf{X}) = 1) = 1 - \prod_{i=1}^{n} E((1 - x_i))$.

$P(\Phi(\mathbf{X}) = 1) = 1 - \prod_{i=1}^{n} (1 - E(x_i))$.

$E(x_i) = R_i(t)$ (component's $b_i$ reliability), then

$R_P(t) = P(\Phi(\mathbf{X}) = 1)$.

Thus, the system reliability is

$R_P(t) = 1 - \prod_{i=1}^{n} (1 - R_i(t)), \quad (18.5.11)$

# 78 Performance, Reliability, and Availability Evaluation of Computational Systems

and the system unreliability

```
$UR_p(t) = \prod_{i=1}^{n} UR_i(t) = \prod_{i=1}^{n} (1 - R_i(t)), \quad (18.5.12)$
```

where $UR_i(t)$ is the component $b_i$ unreliability.

Another way of thinking of the system reliability is through its unreliability. The system composed of $n$ components in parallel fails if every component fails. Hence, the system unreliability, $UR(t)$, is the product of the components' unreliability, $\prod_{i=1}^{n} UR_i(t)$. Therefore, as system reliability $R(t) = 1 - UR(t)$, $R(t) = 1 - \prod_{i=1}^{n} UR_i(t)$.

If $E(x_i) = A_i(t)$ (component's $b_i$ instantaneous availability), then the system instantaneous availability is

$A_p(t) = 1 - \prod_{i=1}^{n} (1 - A_i(t)), \quad (18.5.13)$

and the instantaneous system unreliability is

$UA_p(t) = \prod_{i=1}^{n} UA_i(t) = \prod_{i=1}^{n} (1 - A_i(t)), \quad (18.5.14)$

Likewise, if $E(x_i) = A_i$ (component's $b_i$ steady-state availability), then the system steady-state availability is

$A_p = 1 - \prod_{i=1}^{n} (1 - A_i), \quad (18.5.15)$

and the steady-state unreliability is

$UA_p = \prod_{i=1}^{n} UA_i, \quad (18.5.16)$

If $n$ components are identically distributed, then $A_i = MTTF/(MTTF + MTTR)$ for every component $b_i$, and the system steady-state availability is

$A_p = 1 - \prod_{i=1}^{n} \left( 1 - \frac{MTTF}{MTTF + MTTR} \right) \quad (18.5.17)$

# Reliability Block Diagram

Thus,

$A_p = 1 - \left(\frac{MTTF}{MTTF + MTTR}\right)^n \quad (18.5.18)$

If the time to failure of every component is identically distributed according an exponential distribution with rate $\lambda$, and if the time to repair of every component is also identically distributed and follows an exponential distribution with rate $\mu$, the components' steady-state availability is

$A_i = \frac{\mu}{\lambda + \mu}$

Therefore, the system steady-state availability is

$A = 1 - \left(1 - \frac{\mu}{\lambda + \mu}\right)^n \quad (18.5.19)$

Hence,

$A = 1 - \left(\frac{\lambda}{\lambda + \mu}\right)^n \quad (18.5.20)$

and the system unavailability is

$UA = \left(\frac{\lambda}{\lambda + \mu}\right)^n \quad (18.5.21)$

Consider a system composed of two parallel components with time to fail with rates $\lambda_1$ and $\lambda_2$. The system reliability is

$R(t) = 1 - (1 - e^{-\lambda_1 t})(1 - e^{-\lambda_2 t})$

The MTTF of this system is obtained from

$MTTF = \int_0^{\infty}R(t)dt = \int_0^{\infty}(1 - e^{-\lambda_1 t})(1 - e^{-\lambda_2 t})dt$

$MTTF = \int_0^{\infty}(e^{-\lambda_1 t} + e^{-\lambda_2 t} - e^{-(\lambda_1 + \lambda_2)t})dt.$

$MTTF = \int_0^{\infty}e^{-\lambda_1 t}dt + \int_0^{\infty}e^{-\lambda_2 t}dt - \int_0^{\infty}e^{-(\lambda_1 + \lambda_2)t}dt.$

$MTTF = \frac{1}{\lambda_1} + \frac{1}{\lambda_2} - \frac{1}{\lambda_1 + \lambda_2} \quad (18.5.22)$

# 80 Performance, Reliability, and Availability Evaluation of Computational Systems

Assume a system composed of three parallel components with time to failure exponentially distributed with rates $\lambda_1$, $\lambda_2$, and $\lambda_3$. The system reliability is

$R(t) = 1 - (1 - e^{-\lambda_1 t})(1 - e^{-\lambda_2 t})(1 - e^{-\lambda_3 t}).$

Thus, the system mean time to failure is

$MTFF = \int_{0}^{\infty} R(t) dt.$

$MTFF = \int_{0}^{\infty} (1 - (1 - e^{-\lambda_1 t})(1 - e^{-\lambda_2 t})(1 - e^{-\lambda_3 t})) dt.$

$MTFF = \int_{0}^{\infty} (e^{-\lambda_1 t} + e^{-\lambda_2 t} + e^{-\lambda_3 t} - e^{-(\lambda_1+\lambda_2)t} - e^{-(\lambda_1+\lambda_3)t} - e^{-(\lambda_2+\lambda_3)t} + e^{-(\lambda_1+\lambda_2+\lambda_3)t}) dt.$

$MTFF = \frac{1}{\lambda_1} + \frac{1}{\lambda_2} + \frac{1}{\lambda_3} - \frac{1}{\lambda_1+\lambda_2} - \frac{1}{\lambda_1+\lambda_3} - \frac{1}{\lambda_2+\lambda_3} + \frac{1}{\lambda_1+\lambda_2+\lambda_3}. \quad (18.5.23)$

Likewise, the MTFF of a system with a large number of components should be obtained. If, however, the components are identically distributed, a closed-form expression is available. Consider a system S composed of $n$ blocks with $TTF_i$ identically distributed according to an exponential distribution with rate $\lambda$. The system reliability is

$R(t) = 1 - \prod_{i=1}^{n} (1 - e^{-\lambda t}).$

$R(t) = 1 - (1 - e^{-\lambda t})^n. \quad (18.5.24)$

Thus the mean time to failure is

$MTFF = \int_{0}^{\infty} R(t) dt = \int_{0}^{\infty} (1 - (1 - e^{-\lambda t})^n) dt.$

Let $x = 1 - e^{-\lambda t}$. Hence, when $t=0, x=0$, and when $t \to \infty, x=1$. Differentiating $x$, we get $dx = \lambda e^{-\lambda t} dt$. Therefore,

```
$\int_{0}^{\infty} R(t) dt = \int_{0}^{\infty} (1 - (1 - e^{-\lambda t})^n) dt = \int_{0}^{\infty} \frac{1 - (1 - e^{-\lambda t})^n}{e^{-\lambda t}} \times e^{-\lambda t} \lambda dt,$
```
