# 220 Performance, Reliability, and Availability Evaluation of Computational Systems

The MTTF may also be obtained using the method based on methods described in Section 10.6.1 (see Equation 10.6.4).

```
$MTTF = \frac{(\lambda+\mu)(4\lambda+\mu)}{2\lambda^2(2\lambda+\mu)} \quad (21.2.5)$
```

The reliability calculated using this CTMC is higher than calculated from the RBD as well as the mean time to failure. The reason for this is that the combinatorial models (RBD and FT) do not consider the repair of the first component that fails. It is worth noting that the system continues to provide the specified service in the presence of one failure fault. The equivalent CTMC reliability model to the RBD is shown in Figure 21.7.b. The reliability for the RBD equivalent CTMC is

```
$R(t) = 2e^{-\lambda t} - e^{-2\lambda t}$
```

and the mean time to failure is

```
$MTTF = \frac{3}{2\lambda}$
```

It is worth looking at Equation 18.5.24 and Equation 18.5.25.

**Example 21.2.2.** Let us consider the system depicted in Figure 21.4. Assume the time to failure of each server is independent and identically distributed to an exponential distribution with the rate $\lambda = 5 \times 10^{-4} fph$. The time to repair the servers is exponentially distributed with the equal rate $\mu = 5 \times 10^{-2} rph$. The system reliability at $t = 1000h$ calculated using Equation 18.5.24 is $R(1000h) = 0.8452$ and the mean time to failure is $3000h$. The system reliability at $t = 1000h$ calculated using Equation 21.2.4 or Equation 21.2.5. $R(1000h) = 0.99$. Figure 21.7.c depicts the system reliability calculated for the CTMC for the interval (0, 400000).

**Example 21.2.3.** An application system, composed of two equivalent servers (Main Server - Standby Server - SS), is configured in hot-standby. Figure 21.8.a depicts this system. Each application server is composed of hardware infrastructure (HW), an operating system (OS), and a set of applications (APP). Each server has a hardware infrastructure (Figure 21.8.b), which is composed of a motherboard (MB), a network controller (NC), a video controller (VC), a disk controller (DC), a disk (D), and a power source (S). Each server may be represented by an RBD composed of three blocks (Figure 21.8.b). One block represents the application (App), another represents the operating system (OS), and a third block represents the hardware infrastructure. As the hardware infrastructure is decomposed into the motherboard (MB), network controller (NC), video controller (VC), disk controller (DC), disk (D), and power source,

> ⁵It can be calculated using Equation 18.5.25.