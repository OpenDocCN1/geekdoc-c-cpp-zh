the solution of partial differential equations, stochastic analyses, and related problems.

**Parallel operation:** This mode of operation requires real time operation by the digital computer as it operates in parallel with the analog computer and has to read and supply values with as little latency as possible. In a setup like this, the digital computer can not only change coefficients at run-time but also generate functions, act as a delay circuit, make decisions based on the values of analog variables, and much more.

# 7.1 Hybrid controllers

The following examples and explanations are based on the Analog Paradigm hybrid controller but the ideas and techniques presented are by no means restricted to this particular device. Similar and coupling devices have been available in the past and can be built using cheap off-the-shelf hardware such as Arduino®-boards etc. A hybrid controller like this might be connected via USB to the digital computer and will typically provide the following functions:

**Control lines:** The hybrid controller must be able to control the mode of operation of the analog computer’s integrators. In the simplest case it will accept commands like ic, op, or halt from the digital computer and set the ModeIC and ModeOP control lines accordingly.

Depending on its connection to the digital computer there might be considerable delays in the exchange of signals due to communication latencies. This can be problematic in applications where precise timing of IC- and OP-times is required. It is therefore recommended that the hybrid controller itself should feature a clock with at least a 1 μs resolution with all timing issues being performed locally by the hybrid controller – without the need to communicate with the attached digital computer.

The hybrid controller should also be able to sense overload conditions, to control the POTSET line, and it should feature an input line for an external halt signal.