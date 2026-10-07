
## 306 Performance, Reliability, and Availability Evaluation of Computational Systems

![](img/2d1450514bb14a0cdf0eb5048614afab_322_0.png)

Figure 22.28 A of a Data Center Information Infrastructure.

[content]or the number of failed servers. In such a case, as soon as a server fails, one repair team is assigned to recover the respective server. Also, consider the times to repair servers are independent and identically distributed random variables, $TTR_i^j$ according to $Exp(\mu)$. As already seen in the chapter, a system is well represented by the SPN in Figure 22.29.a. This net is composed of two places, $S_{OK}$ and $S_F$, with transitions $F$ and $R$, and their respective arcs. Assume all servers are initially operational, which is represented by $\#S_{OK} = 8$. The semantics of both transitions, $F$ and $R$, are iss, all servers are operational, and the number of repair teams is infinity. Here the enhancing degree of $R$ is only constrained by $\#S_F$. A second case is when only one repair team is available. This case is well depicted by the SPN in Figure 22.29.b. The difference between this net and that presented in Figure 22.29.a is the semantics of transitions $R$. A third model is presented in Figure 22.29.c. This represents a configuration in which the number of repair teams is $k$. For representing such a case, one place was added to the previous models, where $\#RP = k$ denotes the number of repair teams, and the semantics of R is iss. Thus, the maximal enhancing degree of R is $k$.

Now, let us all devices depicted in Figure 22.28. This system is composed of eight servers ($Rach_1$ and $Rach_2$), four switches ($Rach_1$ and $Rach_2$), two aggregation routers ($Rach_3$), and two storage units ($Rach_4$) that compose a attached network (SAN). The repair facilities (repair teams) are shared to repair all devices that compose the system. Figure 22.30 presents an availability model that

## Modeling Availability, Reliability, and Capacity with SPN

![](img/2d1450514bb14a0cdf0eb5048614afab_323_0.png)

**22.29** Basic Corrective Repair Models.

represents this system. The initial marking of place RT, NRT, represents the number of teams available for corrective maintenance. The sub-net represented by places SUP and SD, transitions Fs, Rss and Res, and their respective arcs and tokens represent the eight servers, states (operational or in failure), faults, and their respective repairs, where #SUP=#NS=8 is the number of servers available when the system started. Similarly, the sub-net depicted by places SWUP and SWD, transitions Fsw, Rssw and Res represent the two switches, their states, their faults, and their respective repairs. #SWUP=#NSW=4 is the number of switches available in the initial configuration. Likewise, the aggregation routers of the SAN are similarly represented by specific sub-nets. The sub-net composed of places RUP and RD, transitions Fr, Rr and R, their respective arcs, states, their faults, and repairs, where #RUP=#NR=2 is the number of aggregation routers available when the system starts. The last sub-net composed of places SU and SUD, transitions Fsu, Rssu and Res, their arcs and tokens represent the two storage units, their states, faults, and repairs. #SU=#SUD=2 is the number of aggregation storage units available in the initial state. The server semantics of every transition that represents a fault (Fs, Fsw, Fr, and Fss) is iss for each of these device classes, there is more than one. The timed transition adopted to represent the repair (Res, Rss, Res, and Res) also has server semantics (iss). However, the enabling credit is initially stored in place RT; their actual server semantics are kss, where k is their enabling degree (see Section 13.1). The immediate transitions represents the team allocation to a repair activity (repairing a system's component). Their weights define the probability of a team repairing a system component (probability choice in Section 13.1). The probability of firing the immediate transitions will depend on the respective weights, the number of tokens in SD, SWD, SUD, and if place RT is marked. The immediate transition weights may be marked to consider the number of devices of a specific failure. In this study, their weights were defined as constant and equal to one. The priorities assigned to the immediate transitions are also one. The repairing activities for each device class are represented by an immediate transition (Rsi, i $\in \{s,sw,r\}$), a place (i $\in \{S,SW,R\}$ and a timed transition ($Re \in \{s, sw, su\}$). transition $Rsi$ is only enabled if at least one device of the respective class $i \in \{S, SW, R\}$, and a repair team is available, $\#RT > 0$. The time to failure and the repair of each component $i$ are exponentially distributed with rates $\lambda_i$ and $\mu_i, i \in \{s, sw, su\}$, respectively.![](img/2d1450514bb14a0cdf0eb5048614afab_324_0.png)

Figure 22.30 Shared Repair Facility – Corrective Maintenance. Consider the system available if at least four servers, two switches, one router, and one storage unit are operational. Therefore, the steady-state availability is calculated through

$A = P(\#SUP > 3 \cap \#SWUP > 1 \cap \#RUP > 0 \cap \#SU > 0)$

The availability expressed in number of nines is calculated by

$UA = 1 - A$. The downtime in period $T$ is computed through

$DT = UA \times T$.

## Modeling Availability, Reliability, and Capacity with SPN

Table 22.7 MTTF, MTTR, and Number of Type

| Component | MTTF (h) | MTTR (h) | Number |
| :--- | :--- | :--- | :--- |
| Server | 800 | 20 | 8 |
| Switch | 6000 | 40 | 4 |
| Router | 3000 | 40 | 2 |
| Storage Units | 8000 | 48 | 2 |

Assume the components’ MTTF and MTTR are shown in Table 22.7. The system availability and the yearly downtime are shown in Table 22.8 and Figure 22.31 considering the number of repairs as $NRT \in \{1,2,3,4,5,6\}$. It is worth mentioning the impact of having two teams instead of one. The reduction for three teams was far significant, whereas four or more teams did not improve the system availability.

Table 22.8 Availability and Downtime - Shared Repair Facility

| NRT | A | UA | DT (min) |
| :--- | :--- | :--- | :--- |
| 1 | 0.9992364 | 3.1171 | 401.349 |
| 2 | 0.999765533 | 3.6269 | 124.088 |
| 3 | 0.999787871 | 3.6732 | 111.559 |
| 4 | 0.999789848 | 3.6767 | 110.649 |
| 5 | 0.999789672 | 3.6771 | 110.548 |
| 6 | 0.999789686 | 3.6771 | 110.542 |

![](img/2d1450514bb14a0cdf0eb5048614afab_325_0.png)

Figure 22.31 Availability and Downtime – Shared Repair Facility – Corrective Maintenance.

If the priorities assigned to $Rsi, i \in \{s, sw, r, su\}$, are $\pi(Rss) = \pi(Rssw) = 1, \pi(Rssu)=2$ and $\pi(Rsr)=3$, the availability is improved, and the respective times reduced. Table 22.9 shows the availabilities and the respective downtimes when considering $NRT \in \{1, 2, 3, 4, 5, 6\}$.

Table 22.9 Availability and Downtime - Shared Repair Facility - Corrective Maintenance.

- $\pi(Rss) = \pi(Rssw) = 1, \pi(Rsr) = 2$

| NRT | A | UA | DT |
| :--- | :--- | :--- | :--- |
| 1 | 0.999924165 | 3.1201 | 397.446 |
| 2 | 0.999765533 | 3.6299 | 123.207 |
| 3 | 0.999787871 | 3.6733 | 111.524 |
| 4 | 0.999789848 | 3.6767 | 110.648 |
| 5 | 0.999789672 | 3.6771 | 110.548 |
| 6 | 0.999789686 | 3.6771 | 110.542 |

## 22.10 PREVENTIVE MAINTENANCE

Preventive maintenance was already discussed and modeled using CTMCs in Section 21.10. As mentioned in that section, preventive maintenance should be considered when the time to failure has an increasing failure rate over time. Preventive maintenance is an investment. Like anything we invest money and resources, we expect benefits that outweigh our investment. Preventive analysis is used to determine if maintenance will be cost-effective, and if so, it is required to define the requirement and parameter values. This section introduces the SPN pooling of preventive maintenance of systems [282].

In computer systems, preventive maintenance is the task of regularly inspecting the computer hardware and software to ensure that it continues to function correctly. The main activity when performing preventive maintenance on a computer can be summarized by (1) cleaning up the hardware, (2) downloading the latest drivers, and updating the software, checking the antivirus updates, running the software utility disk, and erasing unused programs or other files.

A computer system composed of only one server with an increasing failure rate is first adopted to illustrate a basic availability model, represented in SPN, depicting failure, corrective and preventive maintenances. This system is composed of a hardware subsystem and its software subsystem (see Figure 22.32). The software system comprises an operating system, a web-server, a database-server, and other
