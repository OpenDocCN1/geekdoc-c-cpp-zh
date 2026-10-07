
## 210 Performance, Reliability, and Availability Evaluation of Computational Systems

The minimal cuts are

``````
$MC_1^3 \Rightarrow b_6 \wedge \overline{b_{10}} \wedge \overline{b_{14}},$
```

```
$MC_2^3 \Rightarrow b_6 \wedge \overline{b_{15}},$
```

```
$MC_3^3 \Rightarrow b_6 \wedge b_{11} \wedge \overline{b_{12}} \wedge \overline{b_{14}},$
```

```
$MC_4^3 \Rightarrow b_6 \wedge \overline{b_{11}} \wedge b_{12} \wedge \overline{b_{15}},$
```

```
$MC_5^3 \Rightarrow \overline{b_7} \wedge b_8 \wedge \overline{b_{10}} \wedge \overline{b_{14}},$
```

```
$MC_6^3 \Rightarrow \overline{b_7} \wedge \overline{b_8} \wedge b_{10} \wedge b_{15}},$
```

```
$MC_7^3 \Rightarrow b_7 \wedge \overline{b_8} \wedge b_{11} \wedge b_{12} \wedge b_{13} \wedge b_{14},$
```

```
$MC_8^3 \Rightarrow b_7 \wedge \overline{b_8} \wedge b_{11} \wedge b_{12} \wedge \overline{b_{15}},$
```

```
$MC_9^3 \Rightarrow b_9 \wedge \overline{b_{10}} \wedge \overline{b_{13}},$
```

```
$MC_{10}^3 \Rightarrow \overline{b_9} \wedge b_{10} \wedge \overline{b_{15}},$
```

```
$MC_{11}^3 \Rightarrow \overline{b_9} \wedge b_{11} \wedge b_{12} \wedge b_{13} \wedge \overline{b_{14}},$
```

```
$MC_{12}^3 \Rightarrow \overline{b_9} \wedge b_{11} \wedge b_{12} \wedge \overline{b_{15}},$
```

and

Now we use the Esary-Prochan method to calculate the probability bounds. Hence, $\rho_1^3=p_6p_7, \rho_2^3=p_6p_8, \rho_3^3=p_{10}p_{11}, \rho_4^3=p_{10}p_{12}, \rho_5^3=p_{13}p_{15}, \rho_6^3=p_{14}p_{15}, \gamma_1^3=(1-p_6) (1-p_{10}) (1-p_{13}), \gamma_2^3=(1-p_6) (1-p_{10}) (1-p_{15}), \gamma_3^3=(1-p_6) (1-p_{11}) (1-p_{12}) (1-p_{14}), \gamma_4^3=(1-p_6) (1-p_{11}), \gamma_5^3=(1-p_{12}) (1-p_{15}), \gamma_6^3=(1-p_7) (1-p_8) (1-p_{10}) (1-p_{13}) (1-p_{14}), \gamma_7^3=(1-p_7) (1-p_{10}) (1-p_{11}) (1-p_{12}), \gamma_8^3=(1-p_7) (1-p_8) (1-p_{11}) (1-p_{12}) (1-p_{13}) (1-p_{15}), \gamma_9^3=(1-p_9) (1-p_{10}) (1-p_{13}) (1-p_{14}), \gamma_{10}^3=(1-p_9) (1-p_{10}) (1-p_{15}), \gamma_{11}^3=(1-p_9) (1-p_{11}) (1-p_{12}) (1-p_{13}) (1-p_{14}), \gamma_{12}^3=(1-p_9) (1-p_{11}) (1-p_{15})$. Therefore, the upper and lower probability bounds for the system $S_3$ are:

```
$L_3=(1-\gamma_1^3) \times (1-\gamma_2^3) \times (1-\gamma_3^3) \times (1-\gamma_4^3) \times (1-\gamma_3^2) \times (1-\gamma_6^3) \times (1-\gamma_7^2) \times (1-\gamma_8^3)$
```

```
$$(1-\gamma_9^3) \times (1-\gamma_{10}^3) \times (1-\gamma_{11}^2) \times (1-\gamma_{12}^2)$
```

and

$U_3 = 1-(1-\rho_1^2) \times (1-\rho_2^3) \times (1-\rho_3^3) \times (1-\rho_4^3) \times (1-\rho_5^3) \times (1-\rho_6^3)$

For $p_1 = p_2 = p_3 = p_4 = p_5 = 0.95$, we obtain $L_3 = 0.999718$ and $U_3 = 0.999998$.

Now, reduce the RDB shown in Figure 20.13.a to the RDB presented in Figure 20.13.b. The subsystems are represented by respective component. The reduced model (rm) has one minimal path, $MP_1^{rm} \Rightarrow s_1 \wedge s_2 \wedge s_3$, and three minimal cuts, $MC_1^{rm} \Rightarrow s_1, MC_2^{rm} \Rightarrow s_2$ and $MC_3^{rm} \Rightarrow s_3$.

$\rho_1^{rm} = U_1U_2U_3$,
$\gamma_1^{rm} = (1-L_1)$, $\gamma_2^{rm} = (1-L_2)$,

and

$\gamma_3^{rm} = (1-L_3)$,

Thus

$L = (1-\gamma_1^{rm}) \times (1-\gamma_2^{rm}) \times (1-\gamma_3^{rm}) = 0.989498$

and

$U = 1-(1-\rho_1^{rm}) = 0.998981$.

## EXERCISES

- **Exercise 1.** Consider a RAID 50 with eight disks, each with time to fail exponentially distributed with rate $\lambda = 5.5 \times 10^{-5}$. Propose an RBD and calculate the reliability at $t=7500h$ using the structure-function method.

- **Exercise 2.** Assume a RAID 60 with ten disks, each with time to fail exponentially distributed with rate $\lambda = 5.5 \times 10^{-5}$. Propose an RBD and calculate the reliability at $t=7500h$.

- **Exercise 3.** A system of two servers ($S_1$ and $S_2$), each with its network-attached device ($NAS_1$ and $NAS_2$). The system is operational if both servers and their respective storage device are operational. $A_i = MTTF_i/(MTTF_i+TTR_i)$.

## 212 Performance, Reliability, and Availability Evaluation of Computational Systems

- **Exercise 4.** Consider a RAID 5 with five disks, each with time to fail exponentially distributed with rate $\lambda = 5.5 \times 10^{-5}$. Propose an RBD and calculate the reliability at $t=2000h$.

- **Exercise 5.** Calculate the reliability at $t=3000h$ of the system represented by Figure 20.14 using pivoting.

- **Exercise 6.** Calculate the reliability at $t=3000h$ of the system represented by Figure 20.14 using inclusion-exclusion.

- **Exercise 7.** Calculate the steady-state availability of the system represented by Figure 20.13.

- **Exercise 8.** Calculate the reliability at $t=3000h$ of the system represented by Figure 20.13 using sum of products.

- **Exercise 9.** Calculate the reliability at $t=2000h$ of the system represented by Figure 20.13 using sum of products.

- **Exercise 10.** Calculate the reliability at $t=3000h$ of the system represented by Figure 20.13 using decomposition.

- **Exercise 11.** Calculate the reliability of the system represented by Figure 20.13 using decomposition and exclusion.

- **Exercise 12.** Calculate the reliability bounds of the system represented by Figure 20.13 using min-max method.

- **Exercise 13.** Compute the reliability bounds at $t=2000h$ of Example 19.3 using Esary-Prochan method.
