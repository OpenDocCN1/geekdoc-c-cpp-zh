
of some physical systems. There are some different approaches which are based on the CA method. The Q2R automaton is an approach which is used for the microcanonical Ising model. It is deterministic, reversible, and nonergodic, and is also a very fast method. Many works have been performed based on this model (Stauffer, 2000; Kremer & Wolf, 1992; Moukarzel & Parga, 1989; Stauffer, 1997; Glotzer & Stauffer, 1990; Zabolitzky & Herrmann, 1988; and MacIsaac, 1990). Although the Q2R model is deterministic and hence is fast, it was demonstrated that the probabilistic model of the CA like the Metropolis algorithm (Metropolis et al., 1953) is more realistic for description of the Ising model even though the random number generation makes it slower. There is a main difference between the Cellular Automata (CA) method and the Monte Carlo method which is in the updating of a system at each step. In the Monte Carlo method, only one site or a cluster which is randomly chosen is updated in each step. However, in the CA, all sites are updated in each time step without a random selection. In addition to the Monte Carlo method, it was proposed that the Cellular Automata (CA) could be a good candidate for simulating the Ising models (Domany & Kinzel, 1984).

In the last two decades, a large amount of work was done for describing Ising models by the CA approach, and a great number of papers and excellent reviews were published (MacIsaac, 1990; Creutz, 1986; Toffoli & Margolus, 1990; Kinzel, 1985; and Aktekin, 1999). Most of the works done so far are focused on the qualitative description of various Ising and Potts models or on introducing a faster algorithm. For example, the Q2R automaton was suggested as a fast algorithm and has been studied extensively (Vichniac, 1984; Pomeau, 1984; Herrmann, 1986; Glotzer et al., 1990; Moukarzel & Parga, 1989; and Jan, 1990). It was very fast because no random numbers had to be generated at each step. But in probabilistic CAs, like the Metropolis algorithm, generation of random numbers reduces the speed of calculation, even though it is more realistic for describing the Ising model.

## 2. Isotropic two-layer Ising model

Consider a two-layer square lattice with periodic boundary conditions, each layer with $r$ rows and $p$ columns. Each layer has then $r \times p$ sites, and the number of sites in the lattice is $2 \times r \times p = N$. We consider the next-nearest-neighbor interactions as well, so the number of neighbors for each site is 5. In the two-layer Ising model, for any site we define a spin variable $\sigma^{1(2)}(i,j)=\pm1$ in such a way that $i=1,\ldots,r$ and $j=1,\ldots,p$, where superscript 1(2) denotes the layer number. We include the periodic boundary conditions as

$$
\sigma^{1(2)}(i+r,j)=\sigma^{1(2)}(i,j) \tag{1}
$$

$$
\sigma^{1(2)}(i,j+p)=\sigma^{1(2)}(i,j) \tag{2}
$$

The configuration energy for this model may be defined (Ghaemi et al., 2003) as:

$$
\frac{E(\sigma)}{kT}=-\sum_{n=1}^{2}\sum_{i=1}^{r}\sum_{j=1}^{p}\left[K_x\sigma^{(n)}(i,j)\sigma^{(n)}(i+1,j)+K_y\sigma^{(n)}(i,j)\sigma^{(n)}(i,j+1)\right]-K_z\sum_{i=1}^{r}\sum_{j=1}^{p}\sigma^{(1)}(i,j)\sigma^{(2)}(i,j) \tag{3}
$$

where $*$ indicates the periodic boundary conditions (Eqs. (1), (2)), and $K_x$ and $K_y$ are the nearest-neighbor interactions within each layer in the x and y directions, respectively, and $K_z$ is the interlayer coupling.

Therefore, the configuration energy per spin is

$$
e=\frac{E(\sigma)}{kTN} \tag{4}
$$

The average magnetization of the lattice for this model can be defined (Newman & Barkema, 2001) as

$$
\langle M\rangle=\left\langle\sum_{i=1}^{r}\sum_{j=1}^{p}\sum_{n=1}^{2}\sigma^n(i,j)\right\rangle \tag{5}
$$

and the average magnetization per spin is

$$
\langle m\rangle=\frac{\langle M\rangle}{N} \tag{6}
$$

The magnetic susceptibility per spin ($\chi$) and specific heat per spin ($C$) are defined as

$$
\frac{\partial\langle M\rangle}{\partial\beta}=\beta\left(\langle M^2\rangle-\langle M\rangle^2\right) \tag{7}
$$

$$
\chi=\frac{\beta}{N}\left(\langle M^2\rangle-\langle M\rangle^2\right)=\beta N\left(\langle m^2\rangle-\langle m\rangle^2\right) \tag{8}
$$

$$
C=\frac{k\beta^2}{N}\left(\langle E^2\rangle-\langle E\rangle^2\right)=k\beta^2N\left(\langle e^2\rangle-\langle e\rangle^2\right) \tag{9}
$$

where $\beta=\frac{1}{kT}$.

In the present work, we considered the isotropic ferromagnetic and symmetric case, i.e., $K_x=K_y=K_z=K\ge 0$. We have used a two-layer square lattice with $2500 \times 2500$ sites in each layer with periodic boundary conditions. The Glauber method (Glauber, 1963) was used with a checkerboard approach to update sites. For this purpose, the surfaces of the two layers are checkered the same as each other. For updating the lattice, we use the following procedure: after updating the first layer, the second layer can be updated.

The updating of the spins is based on probabilistic rules. The probability that the spin of a site will be up ($p_i^+$) is calculated from

$$
p_i^+=\frac{e^{-\beta E_i^+}}{e^{-\beta E_i^+}+e^{-\beta E_i^-}} \tag{10}
$$

where

$$
E_i^{\pm}=-K\left[\sigma^n(i,j)\sigma^n(i+1,j)+\sigma^n(i,j)\sigma^n(i-1,j)+\sigma^n(i,j)\sigma^n(i,j+1)+\sigma^n(i,j)\sigma^n(i,j-1)+\sigma^n(i,j)\sigma^B(i,j)\right] \tag{11}
$$

$$
\sigma^n(i,j)=
\begin{cases}
+1 & \text{for } E_i^+,\\
-1 & \text{for } E_i^-,
\end{cases}
\tag{12}
$$

and $\sigma^B(i,j)$ is the neighboring site $(i,j)$ in the other layer. Hence, the probability that the spin will be down is

$$
p_i^-=1-p_i^+ \tag{13}
$$

The approach is as follows: first, a random number is generated. If it is less than $p_i^+$, the spin of the site $(i,j)$ is up; otherwise (it means that the random number is greater than $p_i^+$), it will be down.

When we start the CA with the homogeneous initial state (namely, all sites have spin up or +1), before the critical point ($K_c$), the magnetization per spin $\langle m\rangle$ will decay rapidly to zero and fluctuate around it. After the critical point, $m$ will approach a nonzero value and fluctuate around it; and with increasing $K$, the magnetization per spin will increase. But at the critical point, $m$ will decay very slowly to zero and the fluctuation of the system will reach a maximum. For each $K$, the time it takes for $m$ to reach the stable point and start to fluctuate around it is called the relaxation time ($\tau$). In other words, the relaxation time is the time that the system is thermalized. The value of $\tau$ can be obtained from the graph of $m$ vs. $t$ (Fig. 2).

![](img/55ff3770fcfe64effe3c90a4d4692fa6_456_0.png)

Fig. 2. The magnetization versus time in the two-layer Ising model, for three states. a: $K=0.304$ ($K<K_c$), $\tau=3500$. b: $K=0.310$ ($K=K_c$), $\tau=46000$. c: $K=0.313$ ($K>K_c$), $\tau=4000$. (Each layer has $2500\times2500$ sites, starts from the homogeneous initial state "all +1", time steps = 50000)

One can see from these graphs that the relaxation time increases before the critical point and reaches a maximum at $K_c$, but after the critical point, $\tau$ decreases rapidly. So, at the critical point, the system takes a long time to stabilize. Hence, the critical point may be obtained from the graph of $\tau$ vs. $K$ (Fig. 3). The critical point obtained from this graph is 0.310 for the two-layer Ising model.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_457_0.png)

Fig. 3. The relaxation time obtained from Figure 2 versus $K$ for the two-layer Ising model. The maximum appears at $K=K_c$.

In our approach, we have calculated the thermodynamic quantities after thermalization of the lattice. In other words, first we let the system reach a stable state after some time steps ($t=\tau$), and then it is updated up to the end of the automata ($t=50000$). For example, to calculate the average value of magnetization per spin ($\langle m\rangle$), one should add all values of $m$ from the relaxation time up to the end of the automata (or end of the time step) and divide the result by the number of steps. Another way to calculate the critical point is to use $\langle m\rangle$. By plotting the graph of $\langle m\rangle$ vs. $K$, we may also obtain $K_c$. Fig. 4 shows the results.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_457_1.png)

Fig. 4. $\langle m\rangle$ versus coupling coefficient ($K$) for the two-layer Ising model. The average value for each $K$ is calculated after its relaxation time. (Data are the results for the lattice where each layer has $2500 \times 2500$ sites, starting from the homogeneous initial state with all +1, time steps = 50000)
