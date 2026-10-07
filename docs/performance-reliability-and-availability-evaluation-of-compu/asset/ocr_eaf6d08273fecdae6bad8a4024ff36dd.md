# Reliability Block Diagram

**Example 18.5.1.** Assume a computer system is composed of a physical server (hardware-HW) with an operating system (OS), and two application programs $A_1$ and $A_2$. These components are assumed to be independent. Consider the time to failure of each component (HW, OS, $A_1$, and $A_2$) is exponentially distributed with the respective rates: $\lambda_{HW} = 6.25 	imes 10^{-5}$, $\lambda_{OS} = 3.333 	imes 10^{-4}$, $\lambda_{A_1} = 5.00 	imes 10^{-4}$, and $\lambda_{A_2} = 6.6667 	imes 10^{-4}$. The system is assumed to be operational only if the physical system, and both application programs are operational. Then, the logical function depicting the operational mode is

```
$\Phi(\mathbf{B}) = s_{hw} \wedge s_{os} \wedge s_{a1} \wedge s_{a2},$
```

where $s_{hw}, s_{os}, s_{a1},$ and $s_{a2}$ are the logical variables that describe the components' state. Therefore, the RBD represents this operational mode composes the components in series as depicted in Figure 18.5.b.

The structure function is

```
$\Phi(\mathbf{X}) = x_{hw} \times x_{os} \times x_{a1} \times x_{a2},$
```

where $x_{hw}, x_{os}, x_{a1},$ and $x_{a2}$ are the structure variables that describe the components' reliability $R(t) = E(\Phi(\mathbf{X}))$, then

```
$R(t) = E(x_{hw} \times x_{os} \times x_{a1} \times x_{a2}).$
```

```
$R(t) = E(x_{hw}) \times E(x_{os}) \times E(x_{a1}) \times E(x_{a2}).$
```

```
$R(t) = R_{hw}(t) \times R_{os}(t) \times R_{a1}(t) \times R_{a2}(t).$
```

```
$R(t) = e^{-\lambda_{hw}t} \times e^{-\lambda_{os}t} \times e^{-\lambda_{a1}t} \times e^{-\lambda_{a2}t}.$
```

```
$R(t) = e^{-(\lambda_{hw} + \lambda_{os} + \lambda_{a1} + \lambda_{a2})t}.$
```

```
$R(720h) = 0.3247.$
```

As $R(t) = e^{-\lambda_{eq}t},$ the MTTF = $1/\lambda_{eq}$ and as $\lambda_{eq} = $(\lambda_{hw} + \lambda_{os} + \lambda_{a1} + \lambda_{a2})$, then the system time to failure is MTTF = 640 h.

Figure 18.6 shows the system reliability in the interval $(0, 720h).