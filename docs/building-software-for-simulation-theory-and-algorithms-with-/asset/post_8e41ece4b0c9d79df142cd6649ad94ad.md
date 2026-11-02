
```text
91  delete sim; delete hybrid_model;
92  return 0;
93 }
```

## 5.6 INTERACTIVE SIMULATION OF THE ROBOTIC TANK

In Chapter 4 the robot’s computer was modeled, and now the gears, tracks, motors, and equations of motion can be connected to it. Section 2.2.3 gives the complete set of equations.

### 5.6.1 Correcting the Dynamics of a Turn

An inflectional description of the event condition that initiates and ends a turn is obtained by rearranging Equation 2.19 to obtain the zero-crossing function

\[
g = \frac{B}{2}|F_l - F_r| - S_l \tag{5.14}
\]

When $g$ is equal to zero, the discrete variable *turning* switches its binary value. Brief consideration reveals that this model is unable to begin or end a turn. After *turning* changes value, $g$ is still zero, and so the model switches forever from turning to not turning and back, producing an illegitimate event trajectory.

This illegitimate behavior can be corrected with a hysteresis value $\epsilon$ to separate the torques that begin and end a turn. If $\epsilon$ is small, then the behavior of the model should very nearly approximate what was intended by Equation 5.14. This adjustment creates an event surface that moves when *turning* changes:

\[
g = \begin{cases}
\frac{B}{2}|F_l - F_r| - (S_l - \epsilon) & \text{if } turning = \text{true} \\
\frac{B}{2}|F_l - F_r| - S_l & \text{if } turning = \text{false}
\end{cases}
\tag{5.15}
\]

This solves the illegitimacy problem, but a smooth $g$ is also desirable so that linear interpolation gives a reasonable approximation. The absolute values are removed by creating two event surfaces, one for $F_l - F_r > 0$ and another for $F_l - F_r < 0$. The functions

\[
g_r = \begin{cases}
\frac{B}{2}(F_l - F_r) - (S_l - \epsilon) & \text{if } turning = \text{true} \\
\frac{B}{2}(F_l - F_r) - S_l & \text{if } turning = \text{false}
\end{cases}
\tag{5.16}
\]

initiate and end a clockwise (right-hand) turn and

\[
g_l = \begin{cases}
\frac{B}{2}(F_r - F_l) - (S_l - \epsilon) & \text{if } turning = \text{true} \\
\frac{B}{2}(F_r - F_l) - S_l & \text{if } turning = \text{false}
\end{cases}
\tag{5.17}
\]

a counterclockwise (left-hand) turn. These are both continuous functions between discrete-events, and can be efficiently handled by the event detection algorithm described in Section 5.4.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_223_0.png)
FIGURE 5.8 Tank shuddering through a turn with the duty ratio of the left motor at 75% and right motor at 50%.

Continuing the example in Section 4.4, we can now simulate the response of the entire tank to a sequence of commands from the driver. The first command sets the duty ratio for the right motor at 50% and for the left motor at 75% (Figure 5.12 shows the voltage signal produced by the computer). The tank responds by surging forward and making a shuddering turn to the right. Figure 5.8 shows the torque increasing until it breaks the tracks free and the tank begins the turn. Resistance from the laterally sliding tracks then draws power from the turn, reducing the torque and causing the tracks to stick again. This pattern rapidly repeats, keeping the torque near 0.3 as the tank staggers through its maneuver. One second later, a command from the driver sets the duty ratios to zero, and momentum carries the tank through the rest of a 3.5° turn.

Switching $\omega$ to zero instantaneously when the tracks stick has a curious effect on the model. It is apparent in Figure 5.8 when the torque peaks at 0.3, and is much more obvious in Figure 5.9, which shows a turn in place as the left and right motors work at 100% in opposite directions. At $t = 1$, when the motors are turned off, friction and electrical resistance slow the gears and deenergize the motor windings, thereby reducing the torque acting on the tank. In the instant before the tracks stick, viscous friction opposes the motors with a counterforce of about 0.02 N. After the tracks stick, this friction vanishes, and so does the counterforce. The motors and gears, their energy undiminished by the sudden transition, now apply torque sufficient to again overcome the sticking friction of the tracks, causing the tank to turn. High-speed switching between turning and not turning continues for 0.75 s until resistance in the motors, gearbox, and tracks removes enough energy to end the cycle.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_224_0.png)
FIGURE 5.9 Tank spinning in place with the duty ratios at 100% for each motor, but working in opposite directions.

Is this rapid switching an accurate portrayal of a real turn? Probably not. A more comprehensive analysis will likely reveal a better model in this respect (see, e.g., Mosterman’s and Biswas’s discussion of this issue [90, 91]). The validity of the model, however, is undiminished by this curious phenomenon. The real tank and its model handle so sluggishly that the slight prolongation of a turn is unnoticeable to the driver; and the efficiency calculations that relate the frequency of the voltage and the consumption of power are calculated for straight-line motion. The issue must be revisited, however, if the model’s scope of use is expanded at some later time.

### 5.6.2 A Simplified Model of the Motor

The corrected Euler integrator is adequate to construct the power-frequency plot shown in Figure 2.12 and for simulating single maneuvers like the ones above. However, the step size required for even a modest error tolerance of 10⁻² ranges over five orders of magnitude, from 10⁻⁹ when the tank is accelerating to 10⁻⁴ as it trundles along at constant speed. The small step required for maneuvering makes this simulator impractical for interactive use.

This problem can be solved by using a more sophisticated numerical integration scheme or by devising a simpler model. The former is an advisable solution, and to implement it requires only that a new *ode_solver* be built and supplied to the *Hybrid* class. Suitable methods can be found in any textbook on numerical analysis.

Nonetheless, it is not uncommon for a model to have dynamics that cannot be simulated in detail, either for lack of information or for want of computing capabilities. The consequent simplifications often produce hybrid dynamics, a fact already observed in the tank where the fast, but continuous, switch of the transistors in the motor controller and the sudden slipping of the tracks are replaced by discrete transitions. The simplification pursued here will not have so dramatic an outcome, but it is still instructive to see how fast rates can be removed from a model to reduce its execution time while maintaining its validity.

To isolate the computational problem, we will focus solely on the circumstance where the duty ratios of both motors are at 100%; this requires no discrete events because the motor switches are always closed and the tank moves in a straight line. The left and right treads are identical, and so four equations are sufficient to model the tank’s motion:

\[
\dot{v}=\frac{1}{m_t}\left(2F-B_rv\right) \tag{5.18}
\]

\[
\dot{i}=\frac{1}{L_m}\left(-e-iR_m-\alpha\omega\right) \tag{5.19}
\]

\[
\dot{\omega}=\frac{1}{J_g}\left(\alpha i-\omega B_g-\frac{r}{g}F\right) \tag{5.20}
\]

\[
\dot{F}=\frac{1}{K_l}\left(\frac{r}{g}\omega-v\right) \tag{5.21}
\]

The pair of identical forces $F_r$ and $F_l$ in Equations 2.19–2.31 have been replaced by a single force $F$, the equations that describe a turn have been eliminated, and the position of the tank is ignored. Retained are the speed of the tank and the dynamic behavior of the motors and gearbox (observe that $\omega$ in the equations above is not the rotational velocity of the tank, but the angular velocity of the gears); only three, rather than six, equations are needed for these because the pair acts indistinguishably.

Figure 5.10 shows the trajectories of the four state variables $v$, $i$, $\omega$, and $F$. The voltage $e$ is a constant 7.2 V. Figure 5.11 uses a logarithmic scale for time to show the initial inrush of current when the battery is connected to the motors. Using a per step error tolerance of $10^{-2}$, the step size selection ranges from $10^{-9}$ at the start of the simulation to $10^{-4}$ after the initial transients have died off.
