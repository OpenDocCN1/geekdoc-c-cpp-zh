
referred as GC-1DTCA). We will assume that each model in this class has all the common basic features we described in Section 2.2.1, but no particular or explicit specification of the dynamical updating rules of the model will be done. About these rules, we just will assume that they conserve the number of particles and that prevent collisions and overtaking by assigning the speed $v$ to a particle if, and only if, it has, at least, a number $v$ of free sites ahead. Within this framework, as we will see, an entropy function can be found for the models belonging to GC-1DTCA, which allows the study of the properties of the equilibrium states (which here will be understood as the maximum entropy states) of the cellular automata models for multi-speed traffic flow in a single-lane.

After description of the model system and of the variables that will describe its state, as well as the identification of the microcanonical entropy function, the maximum entropy principle will be applied to determine the equilibrium state, partial densities and the thermodynamic properties of the system, such as temperature, pressure, specific heat, and isothermal compressibility. The theoretical partial densities of the allowed velocities and fundamental diagrams will be compared with computer simulation results we obtained with the Nagel-Schreckenberg and Fukui-Ishibashi probabilistic cellular automata traffic models. In particular, as a part of this comparison, it is shown that, although the NS and FI traffic models behave as non-equilibrium systems, they evolve rapidly towards steady states (at least under periodic boundary conditions) which we have found very close to equilibrium under the view of our theoretical framework.

### 3.1 Entropy and maximum entropy states of 1D traffic cellular automata

Our system is a traffic cellular automaton defined on a 1D-lattice with $L$ sites. It is assumed to have all the basic features cited in Section 2.2.1, but no particular or explicit specification of the velocity updating-rules is made here. However, concerning these rules, we assumed they conserve the number of particles, and prevent collisions and overtaking by assigning the speed $v$ to a particle if, and only if, it has, at least, a number $v$ of free sites ahead. This means, in particular, that velocity anticipation is not considered here.

With this background, a particle with speed $v$ ($v = 0, 1, \ldots, v_{\max}$) can be imagined as a brick of length $v + 1$ which has to be inserted in a 1D ring lattice (the brick row under question of a ring wall). This way, at any time $t$, the model system can be considered as one row of a ring wall, made of holes and $v_{\max}+1$ types of bricks (different in length) not overlapping each other. Since the dynamical rules of a particular model may change the lengths of the bricks, under certain conditions the system could reach states where the concentration of a particular type of bricks predominates over the others. The critical density is an upper bound of the density values for which only particles with speeds up to $v$ (bricks with length $v + 1$) can be found in the system.

$$n_c(v)=\frac{1}{v+1} \tag{1}$$

The macroscopic state of the system will be described by the set of velocity distribution functions $N_v$ ($v = 0, 1, \ldots, v_{\max}$), each defined as the number of particles with some speed $v$ in the lattice. The intensive variables defined as $n_v = N_v/L$ are global partial densities of the system. Then, the global density of the number of particles, $n = N/L$, the traffic flow (or momentum per site), $q$, and the kinetic energy per site, $\epsilon$, of the system, are defined as

$$\sum_{v=0}^{v_{\max}} n_v=n,\qquad \sum_{v=0}^{v_{\max}}vn_v=q,\qquad \sum_{v=0}^{v_{\max}}\varepsilon_v n_v=\varepsilon$$

Here $\varepsilon_v$ stands for the kinetic energy of a particle with unit mass and speed $v$. It is easy to show that flow $q$ and kinetic energy $\varepsilon$ of the system cannot exceed, respectively, the maximum values $q_{\max}(n)$ and $\varepsilon_{\max}(n)$ given by

$$q_{\max}(n)=\begin{cases}
nv_{\max},&0\le n\le n_c(v_{\max})\\
(1-n),&n_c(v_{\max})\le n\le 1
\end{cases}$$

$$\varepsilon_{\max}(n)=\begin{cases}
\frac{1}{2}nv_{\max}^2,&0\le n\le n_c(v_{\max})\\
\frac{1}{2}(1-n)v_{\max}^2,&n_c(v_{\max})\le n\le 1
\end{cases}$$

In the thermodynamic limit $L\to\infty$, where $n_c(v_{\max})$ is the critical density for $v=v_{\max}$. Diagrams of $q_{\max}(n)$ and $\varepsilon_{\max}(n)$ are shown in Fig. 10. In the free-flow regime, $n<n_c(v_{\max})$, vehicles move with speed $v_{\max}$, and the gap between vehicles is either $v_{\max}$ or larger. In consequence, the traffic flow in this regime is $q_{\max}=nv_{\max}$. If global density is larger than the critical density, i.e. $n>n_c(v_{\max})$, only $(L-N)/v_{\max}$ vehicles can move with maximum speed and, in the limit $L\to\infty$, the maximum traffic flow is given by $q_{\max}=1-n$. Similarly, the maximum value $\varepsilon_{\max}$ of kinetic energy can be obtained for both $n<n_c(v_{\max})$ and $n>n_c(v_{\max})$. As a consequence, the possible macroscopic states of the system are defined by those partial densities $n_v$ which correspond to values of particle densities $n$ and kinetic energies $\varepsilon$, ranging in the intervals $0\le n\le1$ and $0\le\varepsilon\le\varepsilon_{\max}(n)$, respectively.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_190_0.png)

Fig. 10. Maximum flow $q_{\max}$ (left) and maximum energy $\varepsilon_{\max}$ (right) as functions of the density of particles $n$, for models with $v_{\max}=1,2,3$ and 4. For each $n\in[0,1]$, the possible states of the system are those with energy $\varepsilon\in[0,\varepsilon_{\max}(n)]$. The transition points correspond to the critical densities $n_c=1/2,1/3,1/4$ and $1/5$.

Given initial and boundary conditions, the specific dynamical rules of the considered traffic cellular automata will define the macroscopic state of the system at any time $t$. Macroscopically, the state of the system will be characterized by the set of values of its partial densities $n_v$, or by the numbers $N_v=n_vL$, which is equivalent. Microscopically, however, there are many different arrangements in the lattice of given numbers $(N_0,N_1,\ldots,N_{v_{\max}})$ of particles moving there with speeds (0, 1, 2, ..., $v_{\max}$), respectively, including a number $\Lambda$ of sites which must remain empty. For models belonging to the GC-1DTCA, with periodic boundary conditions, the number $\Omega(L, N_v)$ of all these different microscopic arrangements of moving particles is given by

$$\Omega=\binom{L}{\Lambda+N}\frac{(\Lambda+N)!}{\Lambda!N_0!N_1!\cdots N_{v_{\max}}!}\tag{5}$$

and the number of empty sites in the lattice (i.e., the lattice sites available for speeding up the particles) can be expressed as

$$\Lambda=L-\sum_{v=0}^{v_{\max}}(v+1)N_v\ge 0\tag{6}$$

Negative values of $\Lambda$ are forbidden because of the non-anticipation restriction that we imposed on the models in the class we are considering.

We underline that $\Omega(L,N_v)$ is the number of all the possible configurations in which we can arrange $N_0$ bricks with 1-site length (representing the particles at rest), $N_1$ bricks with 2-sites length (representing the particles moving with speed $v=1$), $N_2$ bricks with 3-sites length (representing the particles moving with speed $v=2$), and so on, up to $N_{v_{\max}}$ bricks with $(v_{\max}+1)$-sites length (representing the particles with speed $v_{\max}$), by inserting them with no overlaps in a 1D ring-shaped lattice with $L$ sites in total, but allowing that a number $\Lambda$ of sites remain empty. We underline also that this result is valid for any cellular automata traffic model with all the common features we have specified above (Section 2.2.1). However, since particular dynamical rules of a model could prevent the system from reaching some microscopic states with particular configurations of particles, Eqn. (5) will provide, at least, for such cases, an upper bound to the number of them for that model.

Starting from $\Omega(L,N_v)$, the entropy function is defined by $S=\ln(\Omega)$. Then, with the help of Stirling's approximation, the entropy per site, $s=S/L$, in the thermodynamic limit $(L\to\infty)$, can be expressed as

$$s=(\lambda+n)\ln(\lambda+n)-\lambda\ln\lambda-\sum_{v=0}^{v_{\max}}n_v\ln n_v\tag{7}$$

where

$$\lambda=\frac{\Lambda}{L}=1-\sum_{v=0}^{v_{\max}}(v+1)n_v\tag{8}$$

As a pretty nice consequence of the existence of entropy for the cellular automata traffic models we are considering here, we can follow microcanonical equilibrium statistical mechanics to find the equilibrium states of these models as the states that maximize the entropy for given density and energy. These constraints seem suitable because cellular automata traffic models involve rules with parameters (such as randomization $p$ in the NS-model) that control the kinetic energy of the particles, and drive the system towards macroscopic steady-states with velocity distribution densities (and kinetic energies) well defined.
