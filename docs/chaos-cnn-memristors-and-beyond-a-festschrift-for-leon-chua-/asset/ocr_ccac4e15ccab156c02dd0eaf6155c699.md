ing area of study in nonlinear dynamics. Of particular interest in this connection is the effect of time delay in such systems. In this section, we will present some details on coupled piecewise linear time-delay systems and synchronizations exhibited by them.

# 8.1. *Synchronization transitions in coupled time-delay electronic circuits*

Now let us consider the following set of unidirectionally coupled first-order delay differential equations,

$$\frac{dx}{dt}=-a_1x(t)+b_1F[x(t-\tau_1)],$$

$$\frac{dy}{dt}=-a_2y(t)+b_2F[y(t-\tau_1)]+b_3F[x(t-\tau_2)],$$

(34a)                                      (34b)

where $a_1=a_2>0$ are positive constants, $b_1\ne b_2$ contributes to the parameter mismatch resulting in coupled non-identical systems, $b_3$ is the coupling strength, $\tau_1$ is the feedback delay and $\tau_2$ is the coupling delay [40]. The nonlinear function $F(x)$ is of the same form as in Eq. (32).

Now to analog simulate the coupled time-delay systems (Eqs. (34)) and to demonstrate experimentally the existence of different types of synchronizations, a unidirectionally coupled time-delay electronic circuit is constructed as shown in the block diagram of Fig. 20. One of the electronic oscillator circuits is used as the drive system, while the other structurally identical circuit is used as the response system with some parameter mismatches. The drive voltage ($U_1(t)$) after the delay line in the drive system is fed back to the nonlinear part ($ND_1$) of the drive system and a fixed $R_1C_1$ filter with time delay to generate chaotic/hyperchaotic oscillations.

Similarly, the response circuit with a nonlinear part ($ND_2$), a delay line and a fixed $R_2C_2$ filter is capable of generating chaotic/hyperchaotic oscillations. The signal after the nonlinear function of drive is used as the transmission signal, which is unidirectionally transmitted through the lowpass filter ($R_3C_3$), delay line and nonlinear part to the response circuit.

Experimental observations reveal transitions from anticipatory to lag synchronization via complete synchronization, when excitatory couplings are a function of the coupling delay (time $\tau_2$) (see Fig. 21). Next, when we use an inhibitory coupling, $-b_3f[x(t-\tau_2)]$, in Eq. (34b) instead of the excitatory coupling $+b_3f[x(t-\tau_2)]$, we find the transition from inverse anticipatory to inverse lag synchronization via an inverse complete synchronization as a function of the coupling delay $\tau_2$ (see Fig. 22).

# 8.2. *Experimental confirmation of chaotic phase synchronization*

We now consider the possibility of chaotic phase synchronization exhibited by coupled time delay systems. For this purpose, we consider the normalized evolution equation of the coupled time-delay electronic circuits with error coupling,

$$\dot{x}=-ax(t)+b_1F[x(t-\tau)],$$

$$\dot{y}=-ay(t)+b_2F[y(t-\tau)]+\varepsilon(x(t)-y(t)),$$

(35)

![](bbox=[0.255, 0.712, 0.751, 0.879])

Fig. 20. Circuit block diagram of the coupled delayed feedback oscillator. Two delay oscillators are coupled through a nonlinear activation function ($ND$) but with a different time delay $T_{3d}$ in the coupling with a low pass first-order $R_3C_3$ filter. $U_1(t)$ and $U_2(t)$ are the voltages across the capacitances $C_1$ and $C_2$, respectively. $U(t-T_{1d})=U(t-T_{2d})$ are the voltages across the delay units of both the coupled oscillators.