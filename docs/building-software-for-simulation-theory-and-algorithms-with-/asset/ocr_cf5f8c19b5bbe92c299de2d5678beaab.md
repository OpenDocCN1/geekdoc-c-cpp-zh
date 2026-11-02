![](bbox=[0.25, 0.09, 0.78, 0.28])

**FIGURE 5.5** A model of a circuit with two discrete elements.

The electric circuit shown in Figure 5.5 will illustrate the simulation procedure, and the outcome of the simulation is listed in Table 5.2. This circuit has a load that operates when the voltage $v_c$ is greater than the diode's threshold voltage. A capacitor stores energy to drive the load for short periods of time when the main power is disconnected. This capacitor charges rapidly when the load is disconnected, and it trickle-charges while the load is operating. The model has two discrete variables, $s \in \{0, 1\}$ for the switch with $s = 0$ open (not conducting) and $s = 1$ closed (conducting) and likewise for the diode; its state is indicated by $d$. The switch is an input to the system, and the diode state is determined by the capacitor voltage.

The voltage $v_c$ is the model's only continuous state variable. It evolves in each mode as follows:

$$ \dot{v}_c = \begin{cases} 0 & \text{if } s=0,d=0 \\ -\frac{v_c}{C R_i} & \text{if } s=0,d=1 \\ \frac{v_s-v_c}{C R_s} & \text{if } s=1,d=0 \\ \frac{1}{C}\left(\frac{v_s-v_c}{R_s}-\frac{v_c}{R_i}\right) & \text{if } s=1,d=1 \end{cases} \quad (5.13) $$

The diode conducts when $v_c$ exceeds the threshold voltage $v_{op}$ and stops conducting when the voltage drops below $v_{cl}$, where $v_{op} > v_{cl}$. A single function defines both cases:

$$ g(v_c,d) = \begin{cases} v_c-v_{op} & \text{if } d=0 \\ v_c-v_{cl} & \text{if } d=1 \end{cases} $$

Significantly, the diode does not open and close at the same voltage level. If this were the case, then the model would be illegitimate, switching endlessly between its two states when $v_c$ reached a threshold value. The model's output is the state of the diode.