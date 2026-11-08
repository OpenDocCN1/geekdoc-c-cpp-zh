
![](img/55ff3770fcfe64effe3c90a4d4692fa6_354_0.png)

Fig. 1. Demonstration of the basic ideas of the model construction. Agents use different level technologies (mobile phones) to communicate with each other. The different capabilities of the devices (SMS, MMS, video-phone) induce difficulties, i.e. communication is the easiest between devices of the same technological level (this is indicated by the black lines between agents). The height of the colored rectangle indicates the “technological level” of the device of the corresponding agent.

difficult and uncomfortable. In the opposite direction we have to notice that our message will be automatically split up into pieces. Agents using mobile phones are presented in Fig. 1. This simple example clearly illustrates that the source of difficulties is the difference in the technological levels of the devices used for communication and they would not occur if the two partners would use equally advanced technologies. It has to be emphasized that in our modeling approach cost does not only mean the money one has to pay for the services or for the device, but it covers all types of difficulties (including also financial ones) that can affect the quality of the communication (e.g. time, convenience etc.) Kocsis & Kun (2008); Kun et al. (2007).

Based on the above arguments it is reasonable to assume that the cost $C$ induced by the communication of agents $i$ and $j$ is a monotonic function of the difference of the technological levels $|\tau_i-\tau_j|$. For the purpose of the explicit mathematical analysis we consider the most simple functional form and cast the cost of cooperation into the following form Kun et al. (2007)

$$C(i \to j) = a|\tau_i - \tau_j|. \tag{1}$$

Equation (1) expresses that having products of different technological levels (having different values of $\tau$) incurs cost, while interaction with devices of the same technological level is cost-free. This crude assumption describes a socio-economic system which favors the local communities being at the same technological level. Producers fabricate and introduce new communication devices on the market with the goal to provide solutions of possible problems, difficulties customers may have. This generic tendency of technological development can be captured in the model by setting appropriate values for the multiplication factor $a$ of the cost function Eq. (1). Hence, we assume that the value of $a$ depends on the relative technological level of interacting agents as

$$a=\begin{cases}a_1, & \text{if }\tau_i>\tau_j\\a_2, & \text{if }\tau_i<\tau_j\end{cases}\qquad\text{where}\qquad a_1<a_2$$

which clearly favors the higher technological level of users. As a result of the condition $a_1<a_2$ using a more advanced technology than the surroundings $\tau_i>\tau_j$ implies lower costs compared to the opposite case. Note that as a result of this condition the cost function is not symmetric with respect to agents $i$ and $j$. This property of $C$ is expressed by the arrow $\rightarrow$ in the argument so that $C(i\rightarrow j)$ defines the cost of agent $i$ arising due to the cooperation with agent $j$ which is not equal to the cost of agent $j$, i.e. $C(i\rightarrow j)\neq C(j\rightarrow i)$. Knowing the cost of interaction between communication partners we can now define the total cost of a given agent in the model system. If agent $i$ has $n$ collaborating partners with technological levels $\tau_1,\tau_2,\ldots,\tau_n$, the total cost of its collaboration can be obtained by summing up the cost function Eq. (1) over all connections

$$C(i)=\sum_{j=1}^{n}C(i\rightarrow j).$$

### 3.2 Time evolution

In order to reduce their costs, agents are assumed to be able to change their technological level which results in a non-trivial time evolution of the system. Our approach focuses on the spreading of technologies so that agents do not invent new products, the possible level of technologies are determined by the initialization of agents’ characteristics. The driving force of evolution in the system is the tendency that agents try to optimize the cost of their communication reducing the value of $C$. To achieve this goal, however, they can only adopt/copy technologies choosing the one of their interacting partners

$$C^{t+1}(i)=\min\{C(\tau\in\{\tau_i^t,\tau_1^t,\tau_2^t,\ldots,\tau_n^t\})\},$$

where the copy is always executed if it provides cost reduction $C^{t+1}(i)<C(i)$. It is assumed in the model that adopting a technology does not induce costs, i.e. no money is required to buy the new products, thus agents can change their technological level anytime if the change provides cost reduction in the future. The financial status of agents, the amount of money, statistics of income in the society do not play any role in the present setup of the model system but of course it can easily be implemented. This rejection-adoption process based on local cost minimization results in the spreading of the adopted technologies while the rejected ones disappear from the system. Our model emphasizes that the key component of the spreading of innovations is the copying with the aim of ensuring compatibility and hence, reduction of the difficulties (cost of communication). Note that in the model there is no intrinsic advantage of using more advanced technologies, the cost is the same independently of the technological level when consensus has been reached Kocsis & Kun (2008); Kun et al. (2007).

### 3.3 Topology of social contacts

For agent-based socio-dynamics models it is a crucial point to implement a realistic representation of agents' social contacts. We apply the Watts-Strogatz rewiring algorithm Watts & Strogatz (1998) to generate complex networks in order to mimic the topological features of the social contacts in real social systems Kocsis & Kun (2008). We start the process with a square lattice of agents with periodic boundary conditions. The rewiring process is performed such that we take every edge on the lattice and remove it with a probability $p$. After that the connection is re-established between two agents selected randomly with a uniform distribution.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_356_0.png)

Fig. 2. (a) Complex networks of agents with long range connections are obtained by rewiring a square lattice. The color of the nodes corresponds to the number of their connections (lighter blue stands for a higher degree). (b) Degree distribution $\rho(n)$ of rewired square lattices for different rewiring probabilities $p$. Increasing the value of $p$, the distribution gets broader but the position of the maximum does not change.

The rewiring procedure is illustrated by Fig. 2(a). The rewiring process has the consequence that degrees different from 4 occur in the social network with a certain probability and the topology of the system is changed from short ranged ($p = 0$) to random graphs ($p \to 1$) with long range connections Watts & Strogatz (1998). The distribution $\rho(n)$ of the degree of agents $n$, i.e. the number of connections of the agents, can be determined analytically as the convolution of a binomial and a Poissonian distribution Albert & Barabási (2002)

$$\rho(n)=\sum_{s=0}^{\min(n-k,k)}\binom{k}{s}(1-p)^s p^{k-s}\frac{(pk)^{n-k-s}}{(n-k-s)!}e^{-pk}, \tag{5}$$

where $k$ denotes the half of the average degree and $n$ is the observed degree. The weights of the binomial and Poissonian components are in a linear relation to the rewiring probability $p$. Fig. 2(b) illustrates degree distributions of rewired square lattices, generated with the Watts-Strogatz method using various values of the rewiring probability $p$. It can be observed that with the increase of $p$, however, the average degree remains constant $\langle n\rangle = 4$, the distribution $\rho(n)$ gets broader, increasing the polydispersity of social contacts.

The Watts-Strogatz type complex networks have been proven to be very useful in studying social phenomena Watts (1999). For the spreading of technological development the main limitation we face is that the network has a static structure, it does not evolve during the diffusion process. However, this frozen structure allows us to make an efficient cellular automata implementation of the system.

## 4. Analytical investigation of the model

In order to understand the decision making mechanism, how agents select the technology to adopt, and to reveal which features of the system determine the success of technologies on the market, it is useful to study simplified configurations by analytical calculations. First we analyze the ideal case when all agents communicate with each other irrespective of their spatial distance then we consider isolated local communities of relatively small size. We work out a master equation approach which reveals interesting fixed points in the parameter space of the system governing the long term time evolution of technological levels and the overall technological progress of the system.

### 4.1 Mean field versus local interaction

As a starting scenario, let us assume that the system is composed of a large number of agents which have randomly distributed technological levels in an interval $\tau_{\min} \leq \tau \leq \tau_{\max}$ with a probability density $p(\tau)$ and distribution function $P(\tau)=\int_{\tau_{\min}}^{\tau}p(\tau')d\tau'$. If we assume infinite range of interactions, all agents are connected with each other so the cost of interaction of an agent of technological level $\tau$ can be cast into the form

$$C(\tau)=a_1\int_{\tau_{\min}}^{\tau}(\tau-\tau')p(\tau')d\tau' + a_2\int_{\tau}^{\tau_{\max}}(\tau'-\tau)p(\tau')d\tau' \tag{6}$$

as a function of $\tau$. In the next time step the agent will change its technological level from $\tau$ to that $\tau^*$, which minimizes the cost function Eq. (6), i.e. $dC/d\tau|_{\tau=\tau^*}=0$. The technology optimizing the cost can finally be obtained as the solution of the equation

$$P(\tau^*)=\frac{1}{1+1/r} \tag{7}$$

where $r=a_2/a_1$ is the ratio of the two cost factors $a_1$ and $a_2$, and $P$ is the cumulative probability distribution of the technological levels of agents in the initial configuration. A very interesting outcome of the above calculations is that the result does not depend on the precise value of the cost factors $a_1$ and $a_2$ but only on the relative amount of advantages $r=a_2/a_1$ more advanced technologies provide with respect to the lower level ones. Since the range of interaction is infinite, all agents make the same decision, thus after a single time step all agents adopt the same technology $\tau^*$ leading to the end of the evolution of the system. In the special case of $r=1$ (when a higher technological level does not provide any advantages), the system adopts the median $\tau^*=m$ of the initial distribution of techniques $p(\tau)$ Sornette (2000). It is interesting to note that the optimal choice $\tau^*(r)$ is a monotonically increasing function of $r$, however, the most advanced technology $\tau_{\max}$ is solely chosen in the limiting case $\lim_{r\to\infty}\tau^*(r)=\tau_{\max}$. At any finite value of $r>1$ the large number of agents of low level technologies are forced to stay at a lower technological level which shows that for
