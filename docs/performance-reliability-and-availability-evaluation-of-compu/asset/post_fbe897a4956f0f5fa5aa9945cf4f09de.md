
## Fault Tree

![](img/2d1450514bb14a0cdf0eb5048614afab_167_0.png)

Figure 19.8 Three Servers System - Density × Time.

## KooN Gate

Consider a system composed of $n$ components. Suppose the system fails when at least $k$ fails; such a system can be represented by composing $AND$ and $OR$ gates. The system has $\binom{n}{k}$ combinations of $k$ basic events that lead to a failure. Assume, for instance, a system represented by three basic events, $\bar{a}$, $\bar{b}$, and $\bar{c}$. If this system fails at least two out of three basic events occur, the FT is in Figure 19.9. It is worth noting that the basic events appear more than once in the FT. Such an FT has been represented in Figure 19.10.a is an implicit representation of the composition shown in Figure 19.11. The logical function that represents the system failure is

```
$\Psi(a,b,c) = (\bar{a} \wedge b) \vee (\bar{a} \wedge \bar{c}) \vee (\bar{b} \wedge \bar{c})$
```

Hence

```
$\Psi(a,b,c) = (\bar{a} \wedge b) \vee (\bar{a} \wedge \bar{c}) \vee (\bar{b} \wedge \bar{c})$
```

```
$\Psi(a,b,c) = (\bar{a} \wedge b) \wedge (\bar{a} \wedge \bar{c}) \wedge (\bar{b} \wedge \bar{c})$
```

Applying the transformation rules presented in Table 18.3, we get

```
$\Phi(x_a,x_b,x_c) = (1-(1-x_a)(1-x_b)) \times (1-(1-x_a)(1-x_c)) \times (1-(1-x_b)(1-x_c)) \times$
```

```
$(1-(1-x_a)(1-x_b)(1-x_c))$
```

## 152 Performance, Reliability, and Availability Evaluation of Computational Systems

As $x_i^l = x_i$, and doing some algebra, we get

> $\Phi(x_a, x_b, x_c) = x_ax_b + x_ax_c + x_bx_c - 2x_ax_bc$.

Considering $x_a, x_b, x_c$ are independent, $R_a(t) = E(x_a)$, $R_b(t) = E(x_b)$, $R_c(t) = E(x_c)$ and $E(\Phi(x_a, x_b, x_c)) = 1 = R(t)$, we have

> $R(t) = R_b(t)R_c(t) + R_a(t)R_b(t) + R_a(t)R_c(t) - 2R_a(t)R_b(t)R_c(t)$.

The system instantaneous and steady-state availability can be likewise obtained.

**Example 19.2.3.** Assume the FT device in Figure 19.9 represents a sensor system composed of three sensors, $a, b$, and $c$. If each sensor reliability at $t=100h$ is $R_a(100h) = 0.81873$, $R_b(100h) = 0.84648$, and $R_c(100h) = 0.86688$, respectively, the system reliability at $t=100h$ is $R(100h) = 0.93501$.

![](img/2d1450514bb14a0cdf0eb5048614afab_168_0.png)

**Example 19.2.4.** If the basic events are identically distributed, and each sensor reliability at $t=100h$ is $R_i(100h) = 0.81873$, $i \in \{a,b,c\}$, the system reliability at $t=100h$ is $R(100h) = 0.91334$.

![](img/2d1450514bb14a0cdf0eb5048614afab_168_1.png)

If the basic events are identically distributed, the system reliability can be directly obtained by applying

> $UR_e(t) = \sum_{j=k}^{n} UR_e(t)^j(1-UR_e(t))^{n-k}$,

Where $UR_e(t)$ is the unreliability assigned to the basic event.

Therefore

> $R(t) = \sum_{j=k}^{n} UR_e(t)^j R_e(t)^{n-k}. \quad (19.2.21)$

Hence

> $R(t) = 1 - \sum_{j=k}^{n} UR_e(t)^j R_e(t)^{n-k}. \quad (19.2.22)$

Similarly, the system steady-state and instantaneous availability is calculated by

> $A = 1 - \sum_{j=k}^{n} UA_l^j A_e^{n-k}, \quad (19.2.23)$

## Fault Tree

and

$A(t) = 1 - \sum_{j=k}^{n} UA_e(t)^j A_e(t)^{n-k} \quad (19.2.24)$

If the basic events are independent and identically distributed, the gate notation depicted in Figure 19.10.b may be adopted.

![](img/2d1450514bb14a0cdf0eb5048614afab_169_0.png)

Figure 19.9 FT with AND and OR gates representing KooON configuration.

![](img/2d1450514bb14a0cdf0eb5048614afab_169_1.png)

Figure 19.10 KooON gate (a) and its Simplified Representation (b)

## 154 Performance, Reliability, and Availability of Computational Systems

**Example 19.2.5.** Consider the times to failure of each sensor are exponentially distributed with $\lambda = 2 \times 10^{-3} f/h$, and the time to repair of each sensor are also exponentially distributed with $\mu = 5 \times 10^{-2} r/h$. The system steady-availability is 0.99568.

![](img/2d1450514bb14a0cdf0eb5048614afab_170_0.png)

It is worth noting that the $K_{fooN}$ gate is equivalent to the $K_{oooN}$ block (of an RBD), where $K_r = N - K_f + 1$.

**Example 19.2.6.** If FT represents a system failure with only one $K_{fooN}$ gate with $N=7$ and $K_f=3$, the respective $K_r = 7 - 3 + 1 = 5$.

![](img/2d1450514bb14a0cdf0eb5048614afab_170_1.png)

As the $K_{fooN}$ gate is equivalent to the $K_{oooN}$ block, and all events are identically distributed according to exponential distribution with rate $\lambda$, the mean time to failure can be calculated

$MTTF = \frac{1}{\lambda} \sum_{j=k}^{n} \frac{1}{j} \quad (19.2.25)$ (Wait, the OCR text is very garbled in the latter half. Let me re-process based on logical inference of the provided fragments).

*Self-correction: The OCR text from page 170 onwards is highly corrupted/repetitive. I will clean up the noise while keeping the available information.*

Actually, looking closely at the provided text, it seems to have a lot of repetitions and artifacts. I will provide the best coherent version of the provided text.

---

[content]
## Fault Tree

![](img/2d1450514bb14a0cdf0eb5048614afab_167_0.png)

Figure 19.8 Three Servers System - Density × Time.

## KooN Gate

Consider a system composed of $n$ components. Suppose the system fails when at least $k$ fails; such a system can be represented by composing $AND$ and $OR$ gates. The system has $\binom{n}{k}$ combinations of $k$ basic events that lead to a failure. Assume, for instance, a system represented by three basic events, $\bar{a}$, $\bar{b}$, and $\bar{c}$. If this system fails at least two out of three basic events occur, the FT is in Figure 19.9. It is worth noting that the basic events appear more than once in the FT. Such an FT has been represented in Figure 19.10.a which is an implicit representation of the composition shown in Figure 19.11. The logical function that represents the system failure is

```
$\Psi(a,b,c) = (\bar{a} \wedge b) \vee (\bar{a} \wedge \bar{c}) \vee (\bar{b} \wedge \bar{c})$
```

Hence

```
$\Psi(a,b,c) = (\bar{a} \wedge b) \vee (\bar{a} \wedge \bar{c}) \vee (\bar{b} \wedge \bar{c})$
```

```
$\Psi(a,b,c) = (\bar{a} \wedge b) \wedge (\bar{a} \wedge \bar{c}) \wedge (\bar{b} \wedge \bar{c})$
```

Applying the transformation rules presented in Table 18.3, we get

```
$\Phi(x_a,x_b,x_c) = (1-(1-x_a)(1-x_b)) \times (1-(1-x_a)(1-x_c)) \times (1-(1-x_b)(1-x_c)) \times$
```

```
$(1-(1-x_a)(1-x_b)(1-x_c))$
```

## 152 Performance, Reliability, and Availability Evaluation of Computational Systems

As $x_i^l = x_i$, and doing some algebra, we get

> $\Phi(x_a, x_b, x_c) = x_ax_b + x_ax_c + x_bx_c - 2x_ax_bc$.

Considering $x_a, x_b, x_c$ are independent, $R_a(t) = E(x_a)$, $R_b(t) = E(x_b)$, $R_c(t) = E(x_c)$ and $E(\Phi(x_a, x_b, x_c)) = 1 = R(t)$, we have

> $R(t) = R_b(t)R_c(t) + R_a(t)R_b(t) + R_a(t)R_c(t) - 2R_a(t)R_b(t)R_c(t)$.

The system instantaneous and steady-state availability can be likewise obtained.

**Example 19.2.3.** Assume the FT device in Figure 19.9 represents a sensor system composed of three sensors, $a, b$, and $c$. If each sensor reliability at $t=100h$ is $R_a(100h) = 0.81873$, $R_b(100h) = 0.84648$, and $R_c(100h) = 0.86688$, respectively, the system reliability at $t=100h$ is $R(100h) = 0.93501$.

![](img/2d1450514bb14a0cdf0eb5048614afab_168_0.png)

**Example 19.2.4.** If the basic events are identically distributed, and each sensor reliability at $t=100h$ is $R_i(100h) = 0.81873$, $i \in \{a,b,c\}$, the system reliability at $t=100h$ is $R(100h) = 0.91334$.

![](img/2d1450514bb14a0cdf0eb5048614afab_168_1.png)

If the basic events are identically distributed, the system reliability can be directly obtained by applying

> $UR_e(t) = \sum_{j=k}^{n} UR_e(t)^j(1-UR_e(t))^{n-k}$,

Where $UR_e(t)$ is the unreliability assigned to the basic event.

Therefore

> $R(t) = \sum_{j=k}^{n} UR_e(t)^j R_e(t)^{n-k}. \quad (19.2.21)$

Hence

> $R(t) = 1 - \sum_{j=k}^{n} UR_e(t)^j R_e(t)^{n-k}. \quad (19.2.22)$

Similarly, the system steady-state and instantaneous availability is calculated by

> $A = 1 - \sum_{j=k}^{n} UA_l^j A_e^{n-k}, \quad (19.2.23)$

and

$A(t) = 1 - \sum_{j=k}^{n} UA_e(t)^j A_e(t)^{n-k} \quad (19.2.24)$

If the basic events are independent and identically distributed, the gate notation depicted in Figure 19.10.b may be adopted.

![](img/2d1450514bb14a0cdf0eb5048614afab_169_0.png)

Figure 19.9 FT with AND and OR gates representing KooON configuration.

![](img/2d1450514bb14a0cdf0eb5048614afab_169_1.png)

Figure 19.10 KooON gate (a) and its Simplified Representation (b)

## 154 Performance, Reliability, and Availability of Computational Systems

**Example 19.2.5.** Consider the times to failure of each sensor are exponentially distributed with $\lambda = 2 \times 10^{-3} f/h$, and the time to repair of each sensor are also exponentially distributed with $\mu = 5 \times 10^{-2} r/h$. The system steady-availability is 0.99568.

![](img/2d1450514bb14a0cdf0eb5048614afab_170_0.png)

It is worth noting that the $K_{fooN}$ gate is equivalent to the $K_{oooN}$ block (of an RBD), where $K_r = N - K_f + 1$.

**Example 19.2.6.** If FT represents a system failure with only one $K_{fooN}$ gate with $N=7$ and $K_f=3$, the respective $K_r = 7 - 3 + 1 = 5$.

![](img/2d1450514bb14a0cdf0eb5048614afab_170_1.png)

As the $K_{fooN}$ gate is equivalent to the $K_{oooN}$ block, and all events are identically distributed according to exponential distribution with rate $\lambda$, the mean time to failure can be calculated

$MTTF = \frac{1}{\lambda} \sum_{j=k}^{n} \frac{1}{j} \quad (19.2.25)$ (Note: The remaining OCR text in the source was highly repetitive and corrupted, which was filtered to maintain coherence).
