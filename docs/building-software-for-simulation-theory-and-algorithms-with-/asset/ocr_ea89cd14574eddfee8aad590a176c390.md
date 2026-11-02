This problem can be solved by using a more sophisticated numerical integration scheme or by devising a simpler model. The former is an advisable solution, and to implement it requires only that a new _ode_solver_ be built and supplied to the _Hybrid_ class. Suitable methods can be found in any textbook on numerical analysis.

Nonetheless, it is not uncommon for a model to have dynamics that cannot be simulated in detail, either for lack of information or for want of computing capabilities. The consequent simplifications often produce hybrid dynamics, a fact already observed in the tank where the fast, but continuous, switch of the transistors in the motor controller and the sudden slipping of the tracks are replaced by discrete transitions. The simplification pursued here will not have so dramatic an outcome, but it is still instructive to see how fast rates can be removed from a model to reduce its execution time while maintaining its validity.

To isolate the computational problem, we will focus solely on the circumstance where the duty ratios of both motors are at 100%; this requires no discrete-events because the motor switches are always closed and the tank moves in a straight line. The left and right treads are identical, and so four equations are sufficient to model the tank’s motion:

$$\dot{v}=\frac{1}{m_t}\left(2F-B_rv\right) \tag{5.18}$$

$$\dot{i}=\frac{1}{L_m}\left(-e-iR_m-\alpha\omega\right) \tag{5.19}$$

$$\dot{\omega}=\frac{1}{J_g}\left(\alpha i-\omega B_g-\frac{r}{g}F\right) \tag{5.20}$$

$$\dot{F}=\frac{1}{K_l}\left(\frac{r}{g}\omega-v\right) \tag{5.21}$$

The pair of identical forces $F_r$ and $F_l$ in Equations 2.19–2.31 have been replaced by a single force $F$, the equations that describe a turn have been eliminated, and the position of the tank is ignored. Retained are the speed of the tank and the dynamic behavior of the motors and gearbox (observe that $\omega$ in the equations above is not the rotational velocity of the tank, but the angular velocity of the gears); only three, rather than six, equations are needed for these because the pair acts indistinguishably.

Figure 5.10 shows the trajectories of the four state variables $v$, $i$, $\omega$, and $F$. The voltage $e$ is a constant 7.2 V. Figure 5.11 uses a logarithmic scale for time to show the initial inrush of current when the battery is connected to the motors. Using a per step error tolerance of $10^{-2}$, the step size selection ranges from $10^{-9}$ at the start of the simulation to $10^{-4}$ after the initial transients have died off.