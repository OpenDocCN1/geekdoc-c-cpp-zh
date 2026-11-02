approximation would remain at that value. Instead, the simulated voltage overshoots the mark and descends slowly back to the correct solution.

At \(t = (1, 0)\) the switch is opened. This external event advances \(v\) by the elapsed time and invokes the \(\delta_{ext}\) function of the hybrid system to change its state. In this new configuration, the discrete-event system simulates \(v_c\) by

$$v_{c,k+1} = (1 - h + h^2/2)v_{c,k}$$

the error at each step is

$$\epsilon' = |h^2v_{c,k}/2|$$

and the interpolation function for \(g\), solved for time, is as before. The capacitor is drained to the cutoff point after another three events, and the diode opens at the real time of \(t \approx 1.7\).

Now the switch and diode are open and the equations governing the simulation are

$$v_{c,k+1} = v_c$$

$$\epsilon = 0$$

$$t = \infty$$

and so time advances with \(h = h_{max} = 0.2\) but nothing actually changes until the switch is closed again.

Working through this example, it quickly becomes apparent that an explicit formula for \(G\) saves a great deal of time and effort. When \(G\) can be calculated directly from the system’s state, and so the location of the next event in time is known explicitly, the resulting change is commonly called a *time event* and \(G\) a *time event function*. If the next event time must be inferred from event surfaces in the state space, then the resulting change is called a *state event* and the \(g_k\) are *state event functions*. State events require much more computational effort on the part of the simulator, and so result in slower-running simulations. Time events are therefore preferable when they can be constructed.

# 5.5 A SIMULATOR FOR HYBRID SYSTEMS

The *Hybrid* class extends the *Atomic* class of the discrete-event simulator from Chapter 4 to implement the approximating system constructed above. Algorithms for finding event surfaces in time and for solving the differential equation are encapsulated in two classes: the *event_locator* and the *ode_solver*. The differential function, state and time event functions, and discrete transition functions of the hybrid system