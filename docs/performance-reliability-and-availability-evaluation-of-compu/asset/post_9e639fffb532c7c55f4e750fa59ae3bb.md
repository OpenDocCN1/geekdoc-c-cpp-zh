
# 340 Performance, Reliability, and Availability Evaluation of Computational Systems

![](img/2d1450514bb14a0cdf0eb5048614afab_356_0.png)

Figure 22.54 Computer System Specification.

**Exercise 6.** Consider the system depicted in the previous exercise. Instead of adopting cold-standby redundancy, now consider a warm-standby sparing mechanism for the standby subsystem. The standby server (when not operating) does not run software applications (A). Assume the time to start a server is exponentially distributed with $MTTS = 0.025h$. Propose an availability model of the system, considering a hierarchical model based on SPN and RBD. Consider only one-maintenance team. (a) Compute the steady-state availability of the system. (b) Calculate the respective system's downtime in minutes per year.

**Exercise 7.** Assume the single-component system shown is in Figure 22.3. Consider the time to failure of such a component has been registered. $MTTF = 3000h$ and $SD_{TTF} = 60h$. Applying the moment matching method depicted in Section 13.3.8, an Erlang distribution with the following parameters presented as: $ER(K, \lambda)$, where $K=25$ and $\lambda=8.333 \times 10^{-3}h^{-1}$, so $tfph = 1/\lambda = 120h$. The time to repair is suitably depicted by the following Cox-1 distribution: $Cox(\omega_1, \omega_2, K,\mu)$, where $\omega_1=0.0393$, $\omega_2=0.9670$, $K=3$, and $\mu=0.1461h$. Propose an SPN availability model and (a) compute the steady-state availability and yearly downtime. (b) Represent the availability in nines for $tfph$ $(120h,200h)$. (c) Using the reliability model (SPN) depicted in Figure 22.5/b (Figure 22.5a depicts a high-level model), plot the reliability in the interval $(0, 40000h)$.

**Exercise 8.** Assume the system is composed of two servers configured in hot-standby redundancy. Let define the servers' mean to failure as $MTTF = 900h$ and their mean to repair as $MTTR = 40h$. Both TT and TTR are exponentially distributed, and there is only one repair facility. From the SPN depicted in Figure 22.7, (a) calculate the steady-state availability and the yearly downtime. (b) Calculate the yearly downtime considering the $MTTF$ $(900h, 16000h)$. (c) Compute the reliability of this system in the interval $(0, 80000h)$ using a similar model to the one shown in Figure 22.9. (d) Calculate the mean time to failure through the mean time to absorption of the SPN model.

# Modeling Availability, Reliability, and Capacity with SPN

**Exercise 9.** Suppose the system depicted in Figure 22.7a with imperfect failure coverage. Consider the coverage probability $c = 0.97$, and the TTF, TTR, and DT are exponentially distributed with MTTF $=900h$, MTTR $=40h$, MDT $= 0.5$. Propose an SPN availability model and calculate (a) the steady-state availability, (b) the steady-state availability in number of n, (c) the probability of having a hidden failure, (d) the probability of the system being available and safe (without hidden failure), (e) the downtime in a period $T$, and (f) the time that stays in an unsafe state (hidden failure) in a period $T$, $T = 8760$.

**Exercise 10.** Assume the system depicted in Figure 22.14. As $TTF_j, j \in\{HW, OS, WS\}$ are exponentially distributed with $MTTF_{HW} = 20000h$, $MTTF_{OS} = 2800h$, $MTTF_{WS} = 2000h$, and $MTTF_{Fn} = 1600h$. Consider the servers' TTR being exponentially distributed with $MTTR_s = 40h$ and as the time required to switching on (TSSO) the spare server is also exponentially distributed with $MTTSO_S = 0.0667h$, Propose an SPN availability model and calculate the system steady-state availability, (b) the yearly downtime, (c) the system availability (in number of n), (d) the yearly downtime against $MTTS \in (0.05h, 0.2h)$, and propose an SPN reliability model, and calculate the reliability in $t \in (0, 2000)$.

**Exercise 11.** Consider the system depicted in Figure 22.18. As $TTF_j, j \in \{HW, OS, WS\}$ are exponentially distributed with $MTTF_{HW} = 20000h$, $MTTF_{OS} = 2800h$, $MTTF_{Fn} = 1600h, i \in \{1, 2\}$. Propose an SPN availability model and (a) calculate the servers' mean time to fail when in active mode, and the server's mean time to fail when in standby mode. As required to switching on (TSSO) the spare server is also exponentially distributed with $MTTSO_S = 0.017h$, calculate (a) the system steady-state availability, (b) the yearly downtime, (c) the system availability (in number of n), and (d) the yearly downtime.

**Exercise 12.** Assume a system composed of four servers in an active-active configuration. As the times to failure and to repairs is exponentially distributed with $MTTF = 700h$ and $MTTR = 20h$. Consider each server can handle 45000 requests. Propose an SPN availability model and (a) calculate the steady-state availability, (b) the yearly downtime, (c) ANSA, (d) COA, and (e) ATP using Mercury tool.

**Exercise 13.** Suppose a system composed of six similar physical servers ($N=6$). Each server is composed of a hardware infrastructure (HW), an operating system (OS), and a hypervisor (HP). In addition, six virtual machines are deployed each server over the hypervisors as shown in Figure 22.5/a. Each server is composed of a motherboard (MB), a network controller (NC), a video controller (VC), a disk (D), and a power source (S). The components' failure rates are constant and presented in Table 22.19.

# Performance, Reliability, and Availability Evaluation of Systems

![](img/2d1450514bb14a0cdf0eb5048614afab_356_0.png)

Figure 22.54 Servers and Hardware.

Table 22.19 Failure Rates

| i | $\lambda_i (h^{-1})$ |
|---|---|
| HP | $2 \times 10^{-4}$ |
| OS and VMs | $5.5 \times 10^{-4}$ |
| MB | $2 \times 10^{-5}$ |
| NC | $2.3 \times 10^{-5}$ |
| VC | $2.5 \times 10^{-5}$ |
| DC | $2 \times 10^{-5}$ |
| D | $3.8 \times 10^{-5}$ |
| S | $7 \times 10^{-5}$ |

The server time to repair is exponentially distributed with $MTTR_s = 20h$. The VMs' time to failure and to repair are also assumed to be exponentially distributed with $MTTF=800h$ and $0.05h$. Propose an availability model based on SPN and FT and (a) estimate each MTTF. (b) calculate the system availability, considering that the system is available if twenty-eight VMs out of thirty-six are operational, (c) calculate the yearly downtime, the (COA), and the average number of virtual machines in operational state.

**Exercise 14.** Assume the system is composed of eight servers, four switches, two routers, and two storage units. The system is available if at least four servers, two switches, one router, and one storage unit are operational. The repair facilities (repair teams) are shared to repair these devices that compose the system. Assume the components' $MTTF$ and $MTTR$ are shown in Table 22.20.

# Modeling Availability, Reliability, and Capacity with SPN

# Table 22.20 MTTF, MTTR, and Number of Resources of Each Type

| Component | MTTF (h) | MTTR (h) | Number |
|---|---|---|---|
| Server | 900 | 40 | 8 |
| Switch | 7000 | 48 | 4 |
| Router | 5000 | 96 | 2 |
| Storage Units | 9000 | 48 | 2 |

Calculate the system availability and the yearly downtime, considering the number of repairs as $NRT \in \{1, 2, 3, 4, 5, 6\}$.

**Exercise 15.** Now consider a system composed of two servers, where each server is similar to the server described in Figure 22.33. Assume the number of repair teams is one $\#RT = 1$. Consider the time to correct maintenance is exponentially distributed with mean $mttr = 10h$. Also, consider the inspection time is exponentially distributed with mean $mit = 1h$. The time to perform preventive maintenance is distributed according to an exponential distribution with mean $mpmt = 2h$. The system time to failure is distributed according to an Erlang distribution with parameters $k = 8$ and $\beta = 1/phtf = 2 \times 10^{-3}h^{-1}$, which leads to $phtf = 400h$. Calculate (a) the system availability and the respective yearly downtime when preventive maintenance is not adopted and (b) find out the $mtbpm$ that optimizes system availability.
