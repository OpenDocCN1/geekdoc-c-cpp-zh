# 216 Performance, Reliability, and Availability Evaluation of Computational Systems

# 21.2 HOT-STANDBY REDUNDANCY

A computational system is composed of two application servers configured in hotstandby. The application server $S_1$ is the main server, and $S_2$ is the hot-standby spare. Figure 21.4.a presents this system. When $S_1$ fails, $S_2$ immediately assumes the main server functions (perfect switching). Assume the time to failure of both servers are identically distributed with constant failure rates equal to $\lambda$. The time to repair of each server is also identically distributed to an exponential distribution with rate $\mu$. Let us first assume the number of repair facilities is infinite.

![](bbox=[0.167, 0.273, 0.832, 0.466])

**Figure 21.4** Hot-Standby Configuration.

The CTMC shown in Figure 21.4.b is the availability model. This model is composed of three states. Although the spare server, $S_2$, is operational, it is processing the workload. It is ready to assume the main servers' activities as soon as $S_1$ fails. As both servers are turned on, both can fail. When one fails, the system transitions to state 1. In state 1, the spare server begins processing the system workload. The failure rate assigned to transition from state 2 to state 1 is $\lambda$. When in state 1, a repair occurs, which takes the system back to state 2. As in state 1, only one server fails; the failure rate from state 1 to state is $\mu$. When one fails, another failure may occur, which takes the system to state 0. As in state 1, we have only one server operational; the transition rate from state 1 to state 0 is $\lambda$. When the system reaches state 0, both servers fail. As the number of repair facilities is infinite, the repair rate assigned to the transition from state 0 to state 1 is $2\mu$. The rate matrix is

```
$Q = \begin{pmatrix} -2\lambda & 2\lambda & 0 \ \mu & -lambda-\mu & \lambda \ 0 & 2\mu & -2\mu \end{pmatrix}$
```

The instantaneous availability is $A(t) = \pi_2(t) + \pi_1(t)$.