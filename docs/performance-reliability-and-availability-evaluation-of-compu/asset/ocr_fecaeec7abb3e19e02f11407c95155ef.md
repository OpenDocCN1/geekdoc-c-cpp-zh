# Performance, Reliability, and Availability Evaluation of Computational Systems

If $MTTF_i = MTTF$ and $MTTR_i = MTTR$, then

```
$A = 1 - \left(\frac{MTTR_i}{MTTF_i + MTTR_i}ight)^n \quad\quad (19.2.18)
```

If the time to repair of component $i$ is exponentially distributed with rate $\mu_i$, then $A_i = \mu_i / (\lambda_i + \mu_i)$. Hence

```
$A = 1 - \prod_{i=1}^n \frac{\mu_i}{\lambda_i + \mu_i} \quad\quad (19.2.19)
```

If $\lambda_i = \lambda$ and $\mu_i = \mu$, then

```
$A = 1 - \left(\frac{\mu_i}{\lambda_i + \mu_i}\right)^n \quad\quad (19.2.20)
```

The instantaneous availability is similarly obtained.

**Example 19.2.2.** Let us assume that the time to failure of each server $S_i$, $i \in \{1, 2, 3\}$, is exponentially distributed with rate $\lambda = 5 \times 10^{-5} f/h$. The system reliability in the interval $(0, 120000/h)$ is shown in Figure 19.7. The system mean time to failure is $MTTF = 36666.7h$. Figure 19.8 shows the density function of the time to failure when the system is composed of one, two, and three servers. Assuming a server mean time to repair is $2.5h$, the system steady-state availability expressed in number of nines $(\#9s = -log_{10}(1-A)$ - see 16.2.26) is $\#9s = 7.3668$.

![](bbox=[0.215, 0.574, 0.782, 0.816])

**Figure 19.7** Three Servers System - Reliability $	imes$ Time.