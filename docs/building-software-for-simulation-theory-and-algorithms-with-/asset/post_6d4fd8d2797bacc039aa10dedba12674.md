
Ames [4] distinguishes two types of illegitimate behavior. A chattering Zeno system gets stuck when it enters an endless sequence of states that have a zero time advance; a system with \(ta(s)=0\) for all \(s\in S\) is one example. A genuinely² Zeno system has an infinite series of states; although each has a positive time advance, it violates the legitimacy criteria. For example, a system that traverses a series of states \(s_1, s_2, \ldots\), where \(ta(s_k)=1/2^{k-1}\), is genuinely Zeno; the elements in this series of time advances are positive but the series converges to zero and its sum converges to a finite number. (The sum of the time advances converges to 2 and the system, begun in state \(s_1\) at time \(t\), gets stuck just prior to \(t+2\).)

² A chattering Zeno system is no less illegitimate than a genuinely Zeno system, and so this name is an odd choice.

Every reasonable model of a real system is legitimate. Illegitimate systems are usually due to errors made while building the model, and often these errors are discovered when a simulation program fails to stop. The examples given above are extreme, but illegitimate models can occur quite easily in practice, and care must be taken to avoid them.

### 4.1.5 An Example of an Atomic Model

A simple system that has a single input, single output, and single state variable will demonstrate the state transition and output functions. The model accepts a real-valued, nonnegative input that it multiplies by the elapsed time. The product is produced when a time equal to it has expired. If an input arrives while an output is pending, the new input replaces the stored value. An input that coincides with an output is treated as having an elapsed time equal to the time advance. On producing an output, the stored value is set to \(\infty\). The functions that define this system are

$$
\begin{aligned}
\delta_{\mathrm{int}}(q) &= \infty,\\
\delta_{\mathrm{ext}}(q,e,x) &= xe,\\
\delta_{\mathrm{con}}(q,x) &= xq,\\
ta(q) &= \lambda(q)=q.
\end{aligned}
$$

We will feed this system four primitive trajectories and calculate, using Equations 4.7 and 4.10, the state and output resulting from each. The trajectories are

- \(x_1[(0,0),(1,0)]\), with
  $$
  x_1(t)=
  \begin{cases}
  1 & \text{if } t=(0,0),\\
  \Phi & \text{otherwise}.
  \end{cases}
  $$
- \(x_2[(1,0),(1,1)]\), with
  $$
  x_2(t)=
  \begin{cases}
  0 & \text{if } t=(1,0),\\
  \Phi & \text{otherwise}.
  \end{cases}
  $$
- \(x_3[(1,1),(2,0)]\), with \(x_3(t)=\Phi\).
- \(x_4[(2,0),(2,2)]\), with
  $$
  x_4(t)=
  \begin{cases}
  2 & \text{if } t=(2,0),\\
  \Phi & \text{otherwise}.
  \end{cases}
  $$

The system starts with \(q=\infty\) and has been in that state for one unit of time. Using Equation 4.7 to compute its response to \(x_1\), we have

$$
\begin{aligned}
\delta((\infty,1), x_1[(0,0),(1,0)])
&= \delta((1,0), x_1[(0,1),(1,0)]) && \text{(Case 1)}\\
&= \delta((1,1), x_1[(1,0),(1,0)]) && \text{(Case 4)}\\
&= (1,1) && \text{(Case 5)}.
\end{aligned}
$$

With the system in total state \((1,1)\), applying \(x_2\) gives

$$
\begin{aligned}
\delta((1,1), x_2[(1,0),(1,1)])
&= \delta((0,0), x_2[(1,1),(1,1)]) && \text{(Case 2)}\\
&= (0,0) && \text{(Case 5)}.
\end{aligned}
$$

With the system in total state \((0,0)\), we apply \(x_3\) and get

$$
\begin{aligned}
\delta((0,0), x_3[(1,1),(2,0)])
&= \delta((\infty,0), x_3[(1,2),(2,0)]) && \text{(Case 3)}\\
&= (\infty,1) && \text{(Case 5)},
\end{aligned}
$$

and the system returns to where it began. Finally, injecting \(x_4\) gives

$$
\begin{aligned}
\delta((\infty,1), x_4[(2,0),(2,2)])
&= \delta((2,0), x_4[(2,1),(2,2)]) && \text{(Case 1)}\\
&= (2,0) && \text{(Case 5)},
\end{aligned}
$$

and the final, total state is \((2,0)\).

The output trajectory \(y[(0,0),(2,2)]\) produced by this simulation is

$$
y(t)=
\begin{cases}
1 & \text{if } t=(1,0),\\
0 & \text{if } t=(1,1),\\
\Phi & \text{otherwise},
\end{cases}
$$

and the state trajectory \(q[(0,0),(2,2)]\) is

$$
q(t)=
\begin{cases}
\infty & \text{if } t=(0,0),\\
1 & \text{if } t\in[(0,1),(1,1)],\\
0 & \text{if } t=(1,1),\\
\infty & \text{if } t\in[(1,2),(2,0)],\\
2 & \text{if } t\in[(2,1),(2,2)].
\end{cases}
$$

Next we construct the composite trajectory \(x=x_1\cdot x_2\cdot x_3\cdot x_4\). Its canonical decomposition into primitive parts is

$$
x=x_0[(0,0),(0,0)]\cdot x_1\cdot (x_2\cdot x_3)\cdot x_4,
$$

where \(x_0\) is an empty trajectory, \(x_1\) and \(x_4\) are as already defined, and the third primitive segment is \(x_2\cdot x_3\). Beginning again in the total state \((\infty,1)\) and using Equation 4.9 to apply \(x\) gives

$$
\begin{aligned}
\Delta((\infty,1), x_0\cdot x_1\cdot (x_2\cdot x_3)\cdot x_4)
&= \Delta(\delta((\infty,1), x_0), x_1\cdot (x_2\cdot x_3)\cdot x_4)\\
&= \Delta((\infty,1), x_1\cdot (x_2\cdot x_3)\cdot x_4) && \text{(Case 5)}\\
&= \Delta(\delta((\infty,1), x_1), (x_2\cdot x_3)\cdot x_4)\\
&= \Delta((1,1), (x_2\cdot x_3)\cdot x_4) && \text{(Previous calculation)}\\
&= \Delta(\delta((1,1), (x_2\cdot x_3)), x_4).
\end{aligned}
$$

To calculate the response of the system to \((x_2\cdot x_3)\), we use the fact that \(\delta((1,1), (x_2\cdot x_3))=\Delta((1,1), x_2\cdot x_3)=\Delta(\Delta((1,1), x_2), x_3)\) and proceeding from the inside to the outside, obtain

$$
\begin{aligned}
\Delta(\Delta((1,1), x_2), x_3)
&= \Delta(\delta((1,1), x_2), x_3)\\
&= \Delta((0,0), x_3) && \text{(Previous calculation)}\\
&= \delta((0,0), x_3)\\
&= (\infty,1) && \text{(Previous calculation)}
\end{aligned}
$$

as expected. Finally, applying \(x_4\), we obtain

$$
\Delta((\infty,1), x_4)=\delta((\infty,1), x_4)=(2,0)\quad \text{(Previous calculation)}
$$

just as before.

**TABLE 4.1** Table-Driven Simulation of a Discrete-Event System

| t | s | ta(s) | y | x | Type |
|---|---|---|---|---|---|
| (0, 0) | ∞ | ∞ | — | 1 | init,in,1 |
| (0, 1) | 1 | 1 | — | — | ext |
| (1, 0) | — | — | 1 | 0 | out |
| (1, 1) | 0 | 0 | 0 |  | con,out |
| (1, 2) | ∞ | ∞ | — | — | int |
| (2, 0) | — | — | — | 2 | in |
| (2, 1) | 2 | 2 | — | — | ext |
| (2, 2) | — | — | — | — | final,0 |

Discrete-event simulation by hand is greatly facilitated with a table similar to the one used for discrete-time simulation (recall Tables 3.1 and 3.2). The table has six columns: the time \(t\), state \(s\), time advance \(ta(s)\), output \(y\), input \(x\), and the type of event occurring at \(t\). The start and end of the trajectory and its intermediate events can be listed in a separate table and marked off as they are used.

The first row is filled in with the initial time, state and related values, and the appropriate input; its event type is “init,” and the initial elapsed time is recorded with it. Subsequent rows are filled by first determining the event type, which can be “in,” “out,” “int,” “ext,” “con,” or some combination of these, and then filling in the columns according to the event type. An “out” event does not change the state of the system, but may have a value in the \(y\) column; similarly, an “in” event puts a value in the \(x\) column. The new state due to all other events is calculated using the state, input, and elapsed time from the previous row; the elapsed time in a given row is the difference between \(\varphi(t)\) in that row and the previous row. Note that output appears in every row where the elapsed time is equal to the time advance. The type “final” is assigned to the last row and it records the ending value of \(e\). Table 4.1 shows a simulation of the abovementioned model using this method. The procedure is quickest if empty entries in the \(x\) and \(y\) columns and unchanged values in the \(s\) and \(ta(s)\) columns are omitted from the table.

### 4.1.6 The Interrupt Handler in the Robotic Tank

The model of the tank’s interrupt handler is a more complicated example of an atomic model. The event graph in Figure 2.6 illustrates its operation. The state space representation of this model must adhere to the two conventions that we established for it in Section 2.2.4: input changes the state variables immediately and without altering the time to the next interrupt, and output occurs immediately after the *End interrupt* event finishes its work.

The interrupt handler that is actually used in the tank simulator is slightly more complicated than the one shown in Figure 2.6. For reasons of computational efficiency, it restricts output events to instances where the voltage at the motors actually changes, whereas the event graph in Figure 2.6 indicates output after every *End interrupt* event.

When the interrupt handler was implemented in this way, the simulation was unable to keep up with time in the real world and could not be used interactively. The reason for this is that the interrupt handler provides input to the model of the tank’s physics, and calculating a state change for that model takes a (relatively) long time. When the output of the interrupt handler is restricted to just those instances where the voltage actually changes, the simulation avoids unnecessary, time-consuming updates of the physics model and is therefore able to be used interactively.

With this change, the code is simpler (but the event graph messier) if the model uses the output voltages \(e_l\) and \(e_r\) as state variables in place of the switch positions \(s_l\) and \(s_r\). To determine when a new output value must be produced, two new state variables are needed to remember the voltages at the last output. These variables are termed \(e'_l\) and \(e'_r\).

The operation of the interrupt indicator also requires a small modification with respect to its description in Section 2.2.4. An extra phase is needed to produce output after the *End interrupt* event occurs. The interrupt handler now has three distinct phases, corresponding to the two types of events and the production of an output. These phases are EXEC, WAIT, and OUTPUT. In the EXEC phase the model has executed the *Start interrupt* event and is waiting for the *End interrupt* event. In the WAIT phase the model has produced its output (one was required) and is waiting for the *Start interrupt* event. In the discrete instant of time between the EXEC and WAIT phases is the transitory OUTPUT phase, and it changes the voltage signal.

The period between interrupts is most conveniently expressed in terms of the desired signal frequency, rather than in terms of the number of machine cycles that separate interrupts. There are (see beginning of Section 2.2.4) about eight calls to the interrupt handler in each period of the voltage signal. Therefore, a voltage signal with frequency \(f_e\) requires an interrupt period \(t_e\) given by

$$
t_e=\frac{1}{8f_e} \qquad (4.11)
$$

With these changes, the complete set of state variables are the voltages \(e_l\) and \(e_r\) at the motors; the last voltages \(e'_l\) and \(e'_r\) supplied as output, the counter \(c\), the left motor on time \(o_l\) and right motor on time \(o_r\), the directions \(r_l\) and \(r_r\) of the left and right motors, the phase \(i\) (which was the Boolean interrupt indicator), and the time \(\sigma\) remaining until the next event. The range of the voltage variables is the set \(\{0,-7.2,7.2\}\). The range of the counter and motor on times is the set of natural numbers in the interval \([0,255]\). The direction indicators \(r_l\) and \(r_r\) are true if the motor runs in reverse and false otherwise. The phase \(i\) has the range \(\{\mathrm{EXEC},\mathrm{WAIT},\mathrm{OUTPUT}\}\). The time \(\sigma\) remaining to the next event has the range \([0,\max\{t_e,432\times 10^{-6}\}]\). The state of the model can be written, although somewhat awkwardly, as the tuple \((e_l,e_r,e'_l,e'_r,c,o_l,o_r,r_l,r_r,i,\sigma)\), and the set of states is the cross product of the ranges of these state variables.

For brevity

$$
q=(e_l,e_r,e'_l,e'_r,c,o_l,o_r,r_l,r_r,i,\sigma)
$$
