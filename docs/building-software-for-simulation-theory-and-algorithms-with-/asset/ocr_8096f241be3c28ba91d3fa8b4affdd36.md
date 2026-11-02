![](bbox=[0.295, 0.105, 0.725, 0.318])

# **FIGURE 4.2** Corrected event graph for the tank’s interrupt handler.

is used to indicate the state of the system. Input to the model has the form \((o'_l, r'_l, o'_r, r'_r)\), which carries the desired values for the ON times and directional switches of the motors. Output from the model are bags that contain the interrupt indicator, and the pair of voltages \((e_l, e_r)\).

In spite of its large set of states, the behavior of the model is quite simple. Figure 4.2 shows the modified event graph, which includes the new state variables and phase.³ The *Output* and *Start interrupt* events produce output. As before, input is applied immediately but has no effect on the time of the next event.

The time advance function is the simplest part of the interrupt handler’s definition. It returns the time remaining until the next event and is defined by

$$ta(q)=\sigma$$

The output function generates events at the start and end of an interrupt. An interrupt begins when the time advance expires and the model is in its WAIT phase. At this time, an *interrupt* signal is produced for the packet processor. An interrupt ends when the time advance expires and the model is in its OUTPUT phase. Another *interrupt* signal is produced at this time, along with new voltage values for the motors. Specifically, we obtain

$$\lambda(q)=\begin{cases}\{interrupt\}, & \text{if } i=\mathrm{WAIT}\\[2pt]\{interrupt\}, & \text{if } i=\mathrm{OUTPUT}\land(e_l=e'_l\land e_r=e'_r)\\[2pt]\{interrupt,(e_l,e_r)\}, & \text{if } i=\mathrm{OUTPUT}\land(e_l\ne e'_l\lor e_r\ne e'_r)\\[2pt]\varnothing, & \text{otherwise}\end{cases}$$

³ False predicates have a numerical value of zero and true predicates a value of one. So, for example, the voltage \(e_l\) is 7.2 if \(c <\) left motor on time and 0 if it is not.