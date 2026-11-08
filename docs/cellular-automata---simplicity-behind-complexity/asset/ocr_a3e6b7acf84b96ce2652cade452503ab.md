$N_{v_{\max}})$ of particles moving there with speeds (0, 1, 2, ..., $v_{\max}$), respectively, including a number $\Lambda$ of sites which must remain empty. For models belonging to the GC-1DTCA, with periodic boundary conditions, the number $\Omega(L, N_v)$ of all these different microscopic arrangements of moving particles is given by

$$\Omega=\binom{L}{\Lambda+N}\frac{(\Lambda+N)!}{\Lambda!N_0!N_1!\cdots N_{v_{\max}}!}\tag{5}$$

and the number of empty sites in the lattice (i.e., the lattice sites available for speeding up the particles) can be expressed as

$$\Lambda=L-\sum_{v=0}^{v_{\max}}(v+1)N_v\ge 0\tag{6}$$

Negative values of $\Lambda$ are forbidden because of the non-anticipation restriction that we imposed to the models in the class we are considering.

We underline that $\Omega(L,N_v)$ is the number of all the possible configurations in which we can arrange $N_0$ bricks with 1-site length (representing the particles at rest), $N_1$ bricks with 2-sites length (representing the particles moving with speed $v=1$), $N_2$ bricks with 3-sites length (representing the particles moving with speed $v=2$), and so on, up to $N_{v_{\max}}$ bricks with $(v_{\max}+1)$-sites length (representing the particles with speed $v_{\max}$), by inserting them with no overlaps in a 1D ring-shaped lattice with $L$ sites in total, but allowing that a number $\Lambda$ of sites remain empty. We underline also that this result is valid for any cellular automata traffic model with all the common features we have specified above (Section 2.2.1). However, since particular dynamical rules of a model could prevent the system of reaching some microscopic states with particular configurations of particles, Eqn. (5) will provide, at least, for such cases, an upper bound to the number of them for that model.

Starting from $\Omega(L,N_v)$, the entropy function is defined by $S=\ln(\Omega)$. Then, with the help of Stirling's approximation, the entropy per site, $s=S/L$, in the thermodynamic limit $(L\to\infty)$, can be expressed as

$$s=(\lambda+n)\ln(\lambda+n)-\lambda\ln\lambda-\sum_{v=0}^{v_{\max}}n_v\ln n_v\tag{7}$$

where

$$\lambda=\frac{\Lambda}{L}=1-\sum_{v=0}^{v_{\max}}(v+1)n_v\tag{8}$$

As a pretty nice consequence of existence of entropy for the cellular automata traffic models we are considering here, we can follow microcanonical equilibrium statistical mechanics to find the equilibrium states of these models as the states that maximize the entropy for given density and energy. These constraints seem suitable because cellular automata traffic models involve rules with parameters (such as randomization $p$ in the NS-model) that control the kinetic energy of the particles, and drive the system towards macroscopic steady-states with velocity distribution densities (and kinetic energies) well defined.