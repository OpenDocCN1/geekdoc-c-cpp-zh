else than a Lorenz-like attractor (compare Fig. 24 to Fig. 18(e)). The dimensionless form (12) can be also used. In this case, parameter values for producing Fig. 24 are $\alpha=\frac{0.590}{0.120}$, $\beta=\frac{0.590}{0.162}$, $a=1.5$, and $b=-0.07$.

One year later, Chua and co-workers designed a simple piecewise-linear circuit to reproduce Lorenz-like attractor [92]. Using $x=-I_L$, $y=V_{C_1}$, and $z=V_{C_2}$, the governing equations are [93]

```
$$\begin{cases}
\dot{x}=\dfrac{y-Rx}{L}\\[4pt]
\dot{y}=\dfrac{g_1(y-z)-g_2(y+z)-\gamma_2y-x}{C_1}\\[4pt]
\dot{z}=\dfrac{g_1(y-z)+g_2(y+z)+\gamma_3(z-E)}{C_2}
\end{cases} \tag{18}$$
```

where $g_i$’s are two piecewise-linear functions readings as

```
$$\begin{cases}
g_1(u)=\dfrac{(m_0-m_1)|u|+(m_0+m_1)u}{2}\\[6pt]
g_2(u)=\dfrac{(m_0-m_1)|u|-(m_0+m_1)u}{2}
\end{cases} \tag{19}$$
```

This system is equivariant under an order-2 rotation symmetry $R_z(\pi)$. It has three fixed points, one designated by $p^0$ and located at $(x_0,y_0,z_0)=(0,0,\frac{\gamma_3}{\gamma_3-2m_0})$, and two symmetry-related fixed points, $p^{\pm}$, around which the two scrolls take place as in the Lorenz system. A typical Lorenz-like attractor is shown in Fig. 25.

Chua and co-workers proved that

+   (i) there is a value of $\frac{1}{L}\in[0.0165;0.048]$ for which there is a heteroclinic orbit (Fig. 26) connecting $p^{+}$ and $p^{-}$;
+   
+   (ii) the Jacobian matrix at $p^{\pm}$ has eigenvalues $(-\lambda^s,\lambda^u\pm i\omega)$ where $\lambda^s>\lambda^u>0$;
+   
+   (iii) a Horseshoe is embedded in a neighborhood of the heteroclinic point.

As shown in Fig. 26, the heteroclinic orbit is unknotted as required by the Ghrist & Holmes theorem. Unfortunately, the eigenvalues at $p^{\pm}$ are not as required for applying this theorem and it cannot be proved that all possible knots are realized as periodic orbits solution to this Lorenz-like piecewise-linear circuit. Nevertheless, the chaotic nature of its attractor is proved in the sense of Shil’nikov theorem [93]. As shown by Ghrist [70], Lorenz-like systems cannot produce attractors containing every types of knots.

![](bbox=[0.512, 0.096, 0.896, 0.443])

![](bbox=[0.512, 0.465, 0.896, 0.659])

![](bbox=[0.512, 0.693, 0.896, 0.817])

# 6. A Symmetric Piecewise-linear Rössler Circuit

The $R$-$C$-oscillator circuit, consisting of a three-section $R$-$C$-ladder quadrupole and an inverting amplifier in the feedback path (Fig. 27), is one of