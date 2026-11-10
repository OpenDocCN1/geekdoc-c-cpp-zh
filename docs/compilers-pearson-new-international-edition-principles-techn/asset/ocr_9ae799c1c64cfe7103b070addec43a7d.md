**OUTPUT:** Two loops, one software pipelined and one unpipelined.

# **METHOD:**

+   1. Remove the loop-carried antidependencies and output dependences associated with privatizable variables from the data-dependence graph.

+   2. Software-pipeline the resulting dependence graph using Algorithm 10.21. Let $T$ be the initiation interval for which a schedule is found, and $L$ be the length of the schedule for one iteration.

+   3. From the resulting schedule, compute $q_v$, the minimum number of registers needed by each privatizable variable $v$. Let $Q = \max_v q_v$.

+   4. Generate two loops: a software-pipelined loop and an unpipelined loop.

The software-pipelined loop has

$$\left\lfloor\frac{L}{T}\right\rfloor + Q - 1$$

copies of the iterations, placed $T$ clocks apart. It has a prolog with

$$\left(\left\lfloor\frac{L}{T}\right\rfloor - 1\right)T$$

instructions, a steady state with $QT$ instructions, and an epilog of $L-T$ instructions. Insert a loop-back instruction that branches from the bottom of the steady state to the top of the steady state.

The number of registers assigned to privatizable variable $v$ is

$$q'_v = \begin{cases} q_v & \text{if } Q \bmod q_v = 0 \\ Q & \text{otherwise} \end{cases}$$

The variable $v$ in iteration $i$ uses the $(i \bmod q'_v)$th register assigned.

Let $n$ be the variable representing the number of iterations in the source loop. The software-pipelined loop is executed if

$$n \geq \left\lfloor\frac{L}{T}\right\rfloor + Q - 1.$$

The number of times the loop-back branch is taken is

$$n_1 = \left\lfloor\frac{n - \left\lfloor L/T \right\rfloor + 1}{Q}\right\rfloor.$$

Thus, the number of source iterations executed by the software-pipelined loop is

$$n_2 = \begin{cases} \left\lfloor L/T \right\rfloor - 1 + Qn_1 & \text{if } n \geq \left\lfloor L/T \right\rfloor + Q - 1 \\ 0 & \text{otherwise} \end{cases}$$

The number of iterations executed by the unpipelined loop is $n_3 = n - n_2$.