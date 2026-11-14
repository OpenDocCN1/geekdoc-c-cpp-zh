embedded system. Building on these notions, we will evolve a formal FSM model. We will then briefly examine basic *registers* and *shift registers*, which are fundamental to the register transfer level (RTL) model of most contemporary computing cores and to error-detecting and error-correcting systems. Next, we will revisit fundamental *counters* and *dividers* and the critical role they play in the design of clock and time-base subsystems commonly used in embedded designs. Building on this theoretical basis, we will then examine the effects of nonideal behavior in real-world applications.

As we did with our studies of combinational circuits, we will conclude with an introduction to testing sequential circuits. Many of these techniques will subsequently be applied in our studies of debugging embedded designs in Chapter 10. Because they are built around memory devices, sequential systems are significantly more complex to test than combinational circuitry. Their behavior is time dependent and governed by the values of their input signals and the order in which they appear. Compounding the test problem in FSMs is the inherent cyclic nature of such systems. We will introduce and study several different methods for attacking the problems unique to sequential circuitry.

# 3.2 THE CONCEPTS OF STATE AND TIME

We begin the discussion of finite-state systems by examining the concepts of time and state.

# 3.2.1 Time

A combinational logic system has no notion of time or history. The present (static) output does not depend in any way on how the output values were achieved. Neglecting delays through the system, we find that the output is immediate and a direct function of the current input set. In contrast, the current output of a finite-state system depends both on the path the system took to reach the current state and, potentially, the present values of the input set. Time is an integral part of the behavior of such systems.

# 3.2.2 State

In an analog circuit, we define branch and mesh currents and branch or node voltages. The values these variables assume over time characterize the behavior of that circuit. If we know the values of the specified variables over time, we know the behavior of the circuit.

*state variables, state of a system*

Such variables are called *state variables*. We define the *state* of a system at any time as a set of values for such variables; each set of values represents a unique state. Figure 3.1 illustrates a collection of example states. When the value of any variable changes, the state of system changes.

![](bbox=[0.25, 0.74, 0.65, 0.89])

Figure 3.1 A Collection of States