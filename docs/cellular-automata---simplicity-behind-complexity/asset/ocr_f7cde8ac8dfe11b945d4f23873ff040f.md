# ### 3.3 Topology of social contacts

For agent based socio-dynamics models it is a crucial point to implement a realistic representation of agents' social contacts. We apply the Watts-Strogatz rewiring algorithm Watts & Strogatz (1998) to generate complex networks in order to mimic the topological features of the social contacts in real social systems Kossis & Kun (2008). We start the process with a square lattice of agents with periodic boundary conditions. The rewiring process is performed such that we take every edge on the lattice and remove it with a probability $p$. After that the connection is re-established between two agents selected randomly with a uniform distribution.

![](bbox=[0.13, 0.255, 0.86, 0.485])

Fig. 2. (a) Complex networks of agents with long range connections are obtained by rewiring a square lattice. The color of the nodes corresponds to the number of their connections (lighter blue stands for a higher degree). (b) Degree distribution $p(n)$ of rewired square lattices for different rewiring probabilities $p$. Increasing the value of $p$ the distribution gets broader but the position of the maximum does not change.

The rewiring procedure is illustrated by Fig. 2(a). The rewiring process has the consequence that degrees different from 4 occur in the social network with a certain probability and the topology of the system is changed from short ranged ($p = 0$) to random graphs ($p \to 1$) with long range connections Watts & Strogatz (1998). The distribution $p$ of the degree of agents $n$, i.e. the number of connections of the agents, can be determined analytically as the convolution of a binomial and a Poissonian distribution Albert & Barabasi (2002)

$$\rho(n)=\sum_{s=0}^{\min(n-k,k)}\binom{k}{s}(1-p)^s p^{k-s}\frac{(pk)^{n-k-s}}{(n-k-s)!}e^{-pk}, \tag{5}$$

where $k$ denotes the half of the average degree and $n$ is the observed degree. The weights of the binomial and Poissonian components are in a linear relation to the rewiring probability $p$. Fig. 2(b) illustrates degree distributions of rewired square lattices, generated with the Watts-Strogatz method using various values of the rewiring probability $p$. It can be observed