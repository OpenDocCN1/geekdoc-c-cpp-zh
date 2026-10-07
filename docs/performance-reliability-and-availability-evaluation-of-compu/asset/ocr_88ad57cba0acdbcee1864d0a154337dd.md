# 286 Performance, Reliability, Availability Evaluation of Computational Systems

The probability that the system is available and safe (hidden failure) is

```
$AS = P\{#COK > 0)AND(#HF = 0)\}$
```

The downtime in a period $T$ is

```
$DT = P\{#COK = 0\ \times T$,
```

and the time the system stays in an unsafe state (hidden failure) in a period $T$ is

```
$UST = P\{#HF = 1\ \times T$.
```

The reliability model is depicted in Figure 22.10.b. It is somewhat similar to the availability model but with essential adjustments. This SPN must have an absorbing marking, which creates a state when both servers are available. Two changes were made in the SPN of Figure 22.10.a in order to obtain an SPN that allows calculating the reliability. First, when both servers are available, system repair is not allowed. This condition denotes the service stopped; the system ceased to provide its functions. This feature was obtained by including a dependent arc between place CFS and transition R. The expression is $IF(#COK = 0) : (3)ELSE(1)$. Thus, when $COK = 0$ (both servers fail), the arc weight is set to three. Since $CFS$ will never reach three times, this marking is absorbing. The second change was the assignment of a guard expression to transition D, $G(D) = \#COK = 0 \rightarrow \{T,F\}$; thus, when no is in place $COK$, transition D becomes disabled. The system reliability is calculated using

```
$R(t) = P\{#COK > 0\}$,
```

and the probability of it being reliable and safe (hidden failure) is

```
$RS(t) = P\{#COK > 0)AND(#HF = 0)\}$.
```

**Example 22.4.1.** Suppose we have the system depicted in Figure 22.7a but with perfect coverage. Consider the probability that $c=0.95$, and the $TTF, TTR$, and $DT$ are exponentially distributed with $MTTF=810h$, $MTTR=20h$, and $MDT=5$. Table 22.2 shows the results of the steady-state metrics presented above.

Figure 22.11 shows the availability (a), the availability without hidden failure (b), the yearly downtime (c), a period hidden failure is present in a year (d), and the probability of having a hidden failure (e) for $c \in (0.5, 0.95)$. Figure 22.12 presents the availability (a), the availability without hidden failure (b), the yearly downtime (c), a period hidden failure is present in a year (d), and the probability of having a hidden failure (e) for $c \in (0.58, 0.99)$. Figure 22.13 presents the reliability (a) and the reliability without hidden failure ($R(t)$ and Safe) in the interval $(0, 70000)$. The mean time to failure calculated is $MTTF=17596.53h$. The reliability at $t=1000h$ is $R(1000h)=0.9462788$. The probability of being operational (reliable) and not having a hidden failure at $1000h$ is $R(1000h)$ and Safe is $0.9462232.

![](bbox=[0.863, 0.883, 0.879, 0.893])