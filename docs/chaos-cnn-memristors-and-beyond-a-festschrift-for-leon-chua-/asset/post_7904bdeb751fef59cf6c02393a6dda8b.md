
Fig. 2. One parameter bifurcation diagrams for (a) control parameter f (period doubling bifurcations) and (b) control parameter ω (inverse period doubling) for Eq. (5).

![](img/039e7d3c23390584a66737067db8b75b_301_0.png)

![](img/039e7d3c23390584a66737067db8b75b_301_1.png)

Fig. 3. Numerically obtained two parameter bifurcation diagram of the MLC circuit in the (f − ω) plane. Color: light yellow, period-1; magenta, period-2; yellow, period-4; light green, period-8; blue, period-3 window; green, period-5 window; violet, period-6 window and red, chaos.

is also presented in Fig. 3, where we identify a rich variety of bifurcations. These include

- i) Period doubling bifurcations and chaos
- ii) Period halving bifurcations
- iii) Antimonotonicity
- iv) Intermittency

and so on. For more details, see [44].

## 3. A Family of MLC Circuits

The family of MLC circuits, consisting of the basic MLC circuit and its different variants are shown in Fig. 4. These circuits exhibit very interesting

dynamical phenomena including bifurcations and chaos. For example, we consider a variant of the MLC circuit [43,44] discussed in Sec. 2. Instead of the series LCR circuit considered in Fig. 4(a), we now use parallel LCR circuit and include the nonlinear resistor, namely the Chua's diode (N_R) in parallel. The variant circuit is shown in Fig. 4(b).

The governing equations of motion of the variant of MLC circuit are

```
C dv_R/dt = 1/R (F sin(Ωt) - v_R) - i_L - h(v_R), (13a)
```

```
L di_L/dt = v_R, (13b)
```

where h(.) is the piecewise linear function given by Eq. (2).

As in the case of the MLC circuit discussed in Section 2, for the present circuit also the presence of a rich variety of bifurcations and different routes to chaos have been reported experimentally, confirmed numerically and proven mathematically [43,44].

Rescaling the circuit equations (13) through the relations x = v/B_p, y = i_L/(G B_p), ω = ΩC/G, G = 1/R and t' = tG/C and then redefining t' as t, we have the dynamical equations

```
ẋ = f sin ωt - x - y - h(x),
ẏ = βx, ' = d/dt, (14)
```

where β = C/(L G²), f = F/B_p.

The piecewise linear function h(x) has again the piecewise behaviour as given by Eq. (6). Equations (14) can also be equivalently written as a single second order linear differential equation with

![](img/039e7d3c23390584a66737067db8b75b_302_0.png)

discontinuities as in the case of the bilinear oscillator [1, 2]. In fact we can rewrite Eq. (14) as

$$\ddot{x}+\dot{x}+\beta x+\omega f\cos\omega t=h'(x)\dot{x}, \tag{15}$$

where

$$h'(x)=\begin{cases} b, & x>1\\ a, & -1<x<1\\ b, & x<-1 \end{cases} \tag{16}$$

We can write down the explicit solutions as in the previous section and match the solutions across the boundaries or carry out a numerical analysis of Eq. (14) or (15). Pspice simulations and experimental verifications have also been carried out in detail. A rich variety of bifurcations and chaos results in. These include the following:

- i) Quasiperiodic and torus breakdown route to chaos
- ii) Period-adding sequences and Farey sequences
- iii) Period doubling and reverse period doubling bifurcations
- iv) Remerging Feigenbaum trees, bubbling, band merging and antimonotonicity
- v) Intermittency route to chaos
- vi) Neimark bifurcation

To provide an idea of the varied kinds of dynamical phenomena admitted by this piecewise linear system (14), we present in Fig. 5 a two parameter bifurcation diagram in the amplitude-frequency $(f-\omega)$ space of the external force, while all the

![](img/039e7d3c23390584a66737067db8b75b_302_1.png)

other parameters are fixed. The diagram covers the transitions in the region of the external forcing frequency, $0.09 \leq f \leq 0.16$ and the forcing amplitude, $0.15 \leq f \leq 0.5$. Here also each coloured region denotes a particular type of steady state behaviour, identical to the phase diagram of the MLC circuit, see Fig. 3. Periodic windows are indicated by the corresponding numbers (such as 5T, 6T etc.). The numerical results indicated in Fig. 5 have also been confirmed with experimental results. More details may be obtained from references [43, 44].

In a similar way, the dynamics of the remaining circuits of the family given in Figs. 4 can be analysed. The details will be published elsewhere.

## 4. Spatiotemporal Dynamics of Coupled MLC Circuits

Coupled nonlinear oscillators in the form of arrays arise in many branches of science. These coupled arrays are often used to model very many spatially extended dynamical systems explaining reaction-diffusion process. One can visualize such an array as an assembly of a number of subsystems coupled to their neighbors, or as coupled nonlinear networks (CNNs) [5, 7]. For the past few years several investigations have been carried out to understand the spatiotemporal behaviours of coupled nonlinear oscillators and systems. The studies on these systems include the traveling wave phenomenon, Turing patterns, spatiotemporal chaos and synchronization [8, 18]. In this section we consider similar arrays of coupled nonlinear electronic circuits consisting of MLC circuit as a basic unit, which is essentially a two variable model.

### 4.1. Arrays of MLC circuits

We will now consider one and two-dimensional arrays of MLC circuits [28], where the intercell couplings are effected by linear resistors. Such resistive couplings are then equivalent to diffusive coupling.

### 4.1.1. One-dimensional array

Figure 6 shows a schematic representation of an one-dimensional chain of resistively coupled MLC circuits. Note that the individual cells correspond to isolated MLC circuits. Using the standard Kirchhoff’s laws, the dynamics of the one-dimensional chain can be easily shown to be governed by the following system of equations, in terms of the rescaled variables,

```
$$\dot{x}_i = y_i - h(x_i) + D(x_{i+1}+x_{i-1}-2x_i), \tag{17a}$$
$$\dot{y}_i = -\sigma y_i - \beta x_i + F\sin\omega t, \quad i=1,2,\ldots,N, \tag{17b}$$
```

where $D$ is the diffusion coefficient, $N$ is the chain length and $h(x)$ is the three segment piecewise linear function representing the current voltage characteristic of the Chua’s diode,

```
$$h(x)=\begin{cases}
\epsilon+m_2x+(m_0-m_1), & x\ge x_2\\
\epsilon+m_0x, & x_1<x<x_2\\
\epsilon+m_1-(m_0-m_1), & x\le x_1
\end{cases} \tag{18}$$
```

where $\epsilon$ is the dc offset included for convenience. Naturally, depending on the choice of the slopes $m_0$, $m_1$ and $m_2$, one can fix the characteristic curve of the Chua’s diode. For typical forms of $h(x)$, the coupled MLC circuit exhibits interesting dynamics such as wave propagation and its failure, Turing patterns, spatio-temporal chaos and so on. In the following discussion, we will fix $N$ at $N=100$.

### 4.1.2. Two-dimensional array

As in the case of the one-dimensional array introduced above, one can also consider a two-dimensional square array with each cell in the array being coupled to four of its nearest neighbours, for example, with linear resistors. The state equations can be now written in dimensionless form as

```
$$\dot{x}_{i,j}=y_{i,j}-h(x_{i,j})+D_1(x_{i+1,j}+x_{i-1,j}+x_{i,j+1}+x_{i,j-1}-4x_{i,j})$$
$$\qquad=f(x_{i,j},y_{i,j}),$$
$$\dot{y}_{i,j}=-\sigma y_{i,j}-\beta x_{i,j}+D_2(y_{i+1,j}+y_{i-1,j}+y_{i,j+1}+y_{i,j-1}-4y_{i,j})+F\sin\omega t$$
$$\qquad=g(x_{i,j},y_{i,j}),\quad i,j=1,2,\ldots,N. \tag{19}$$
```

This two-dimensional array has $N\times N$ cells arranged in a square lattice. In our numerical study we will again take $N=100$.

In this analysis we fix the parameter at $\{\beta,\sigma,m_0,m_1,m_2,\epsilon,F\}=\{1.0,1.0,-2.25,1.5,.25,0,0\}$ so that the system admits bistability which is a necessary condition to observe a wave front. Carrying out

![](img/039e7d3c23390584a66737067db8b75b_303_0.png)

Fig. 6. Circuit realization of a one-dimensional array of coupled MLC circuits.

Fig. 7. Space-time plot (a) showing propagation of wave front in one-dimensional array (100 cells) of MLC circuits for D = 2.0 and (b) propagation failure for D = 0.4.

Fig. 8. The spontaneous formation of Turing patterns in an array of 100 × 100 oscillators for the parameters β = 0.8, σ = 1, m0 = −0.5, m1 = 0.5, m2 = 0.5, ε = 0.1, F = 0.0, ω = 0.75, D1 = 1 and D2 = 10 in Eqs. (19) at various time units (a) T = 50, (b) T = 100, (c) T = 500 and (d) T = 2000.

a numerical integration of equations (17) with N = 100 and with the diffusion coefficients chosen at a higher value, D = 2.0, a motion of the wave front towards right (see Fig. 7) is observed, that is a travelling wave front is found. However, below a critical value of the diffusion coefficient (D = Dc) a failure in the propagation has been observed, which in the present case turns out to be D = Dc = 0.4. This means that the initiated wavefront is unable to move as time progresses and Fig. 7(b) shows the propagation failure for D = 0.4.

Another interesting dynamical phenomenon in the coupled arrays is the formation of Turing patterns. For this purpose, we have fixed the parameters for the two-dimensional model (19) as {β, σ, m0, m1, m2, ε, F} = {0.8, 0.92, 0.1, −0.5, 0.5, 0.5, 0}. The numerical simulations have been carried out using an array of size 100 × 100 and random initial conditions near the steady states have been chosen for the x and y variables. Figures 8(a)–(d) show how the diffusion driven instability leads to stable hexagonal pattern (Fig. 8(d)) after passing through intermediate stages (Figs. 8(a)-8(c)).

## 5. Dynamics of a Hyperchaotic Memristive MLC Circuit

In 1971 Leon Chua, while trying to place on a firm mathematical footing the interconnections between the three basic circuit elements known at that time, namely the resistor, capacitor and inductor, felt the need for a fourth basic circuit element, based on symmetry considerations, and predicted its existence [3]. He even postulated that this element should not only have a resistive property but should also be endowed with a memory nature. In order to justify its dual properties, he named this hypothetical element as memristor. Some three and a half decades later, Strukov and his co-workers at Hewlett-Packard Labs reported the existence of this elusive element in nano-scale devices [41]. Ever since this discovery, much research has been going on to utilise the memristor in constructing nonlinear circuits [15, 16, 29, 48, 51, 52].

As memristance is a fundamental circuit quantity, Chua inferred that no combination of passive devices can reproduce the properties of a memristor. Nevertheless he theorised that, in principle, memristors with almost any φ − q characteristic
