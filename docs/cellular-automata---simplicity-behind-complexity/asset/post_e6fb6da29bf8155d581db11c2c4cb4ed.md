
of such calculation. As it is seen, before the critical point ($K<K_c$), $\langle m \rangle \approx 0$ and after that ($K>K_c$), $\langle m \rangle \neq 0$. The obtained value of the critical point from this approach is $K_c = 0.310$ for the two-layer Ising model.

For calculation of $\chi$ for each $K_i$, first we have calculated the value of $(m-\langle m \rangle)^2$ in each time step. Then these values are averaged in the same way explained above. According to eq. 8, this average could be used for computation of $\chi$. Using eq. 9 for calculation of the specific heat ($C$), we have done it in a similar manner as described above. Figures 5 and 6 show the graphs of $\chi$ vs. $K$ and $C$ vs. $K$, respectively, for the two-layer Ising model. These graphs are other ways for obtaining the critical point. The maximum of these graphs indicates the critical point. The obtained value for $K_c$ from these graphs is 0.310 for the two-layer Ising model.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_458_0.png)

Fig. 5. Magnetization susceptibility per spin ($\chi$) versus $K$ for the two-layer Ising model. (The calculated data are the results for the lattice in which each layer has 250 × 250 sites, starting from the homogeneous initial state with all spins up, time steps = 50000)

![](img/55ff3770fcfe64effe3c90a4d4692fa6_459_0.png)

Fig. 6. Specific heat per spin ($C$) versus $K$ for the two-layer Ising model. (The calculated data are the results for the lattice for which each layer has 2500 × 2500 sites, starting from the homogeneous initial state with all spins up, time steps = 50000)

## 3. Isotropic two-layer 3-state Potts model

Although we do not know the exact solution of the Potts model for any two-layer lattice at present time, a large amount of numerical information has been accumulated for the critical properties of the various Potts models. Consider a two-layer square lattice with the periodic boundary condition, each layer with p columns and r rows. Each layer then has r × p sites and the number of sites in the lattice is 2 × r × p = N. We consider the next-nearest-neighbor interactions as well, so the number of neighbors for each site is 5. For any site we define a spin variable $\sigma(i,j) = 0, \pm 1$ so that $i = 1,\ldots,r$ and $j = 1,\ldots,p$. The configurational energy of a standard 3-state Potts model is given (Asgari et al., 2004) as:

$$\frac{E(\sigma)}{kT}=-\sum_{i=1}^{r}\sum_{j=1}^{p}\sum_{n=1}^{2}\left[K_x\delta_{\sigma(i,j,n),\sigma(i+1,j,n)}+K_y\delta_{\sigma(i,j,n),\sigma(i,j+1,n)}+K_c\delta_{\sigma(i,j,n),\sigma(i,j,\bar n)}\right]$$

Where

$$\delta_{i,j} = 1 \text{ for } i = j$$
$$\delta_{i,j} = 0 \text{ for } i \neq j \quad (15)$$

and * indicates the periodic boundary condition and $K_x$ and $K_y$ are the nearest-neighbor interactions within each layer in $x$ and $y$ directions, respectively, and $K_c$ is the interlayer coupling. Therefore, the configurational energy per spin is

$$e = \frac{E(\sigma)}{kTN} \quad (16)$$

and the general equations (5-9) are applicable to this model. For quantitative computation of the critical temperature of a two-layer 3-state Potts model, we considered the isotropic ferromagnetic case in which $K_x = K_y = K_c \geq 0$. We have used a two-layer square lattice in which each layer has 1500 × 1500 sites and to reduce the finite size effects, the periodic boundary condition is used. Each site can have a value of +1, -1 or zero. We used the Glauber method with checkerboard approach to update the sites. Namely, each layer is like a checkerboard surface and at first, the updating is done for the white parts of the first layer. Then the black ones are updated. After which, this approach is done for the second layer. The updating of +1 spins is based on the probabilistic rules. The probability that the spin of one site will be +1 ($p_i^+$) is given by

![](img/55ff3770fcfe64effe3c90a4d4692fa6_461_0.png)

Fig. 7. Relaxation time ($\tau$) versus coupling coefficients ($K$). (The calculated data are the results for the lattice with 1500 × 1500 sites in each layer, starting from the homogeneous initial state with all spins up, time steps = 100000)

(t = 100000). For example, to calculate the average value of magnetization per spin ($\langle m \rangle$), one should add all of the values for m from the relaxation time to the end of the automaton (or end of the time step) and divide the result by the number of steps. By drawing the graph of $\langle m \rangle$ versus $K$, we could get $K_c$. In this graph, for $K < K_c$, the value of $\langle m \rangle$ lies around zero. But it becomes nonzero at $K=K_c$, after which, its value increases gradually. For calculation of the susceptibility per spin $\chi$ (eq. 8), for each $K$, first we calculated the value of $(m-\langle m \rangle)^2$ in each time step. Then these values are averaged by the same method explained above. Also the calculation of the specific heat $C$ (eq. 9) may be done in a similar way. The graphs of $\chi$ versus $K$ and $C$ versus $K$ are another approach to obtain the critical point. The maximum of such graphs gives the critical point.

The results of such calculations are shown in figures 8-10 for the simplest case of the two-layer 3-state Potts model when $K_1=K_2=K_3=K\geq 0$. The obtained value for the critical point is 0.726 for this case.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_462_0.png)

Fig. 8. $\langle m \rangle$ versus coupling coefficients ($K$). (The calculated data are the results for the lattice with 1500 × 1500 sites in each layer, starting from the homogeneous initial state with all spins up, time steps = 100000)

![](img/55ff3770fcfe64effe3c90a4d4692fa6_462_1.png)

Fig. 9. Magnetization susceptibility per spin ($\chi$) versus $K$. (The calculated data are the results for the lattice with 1500 × 1500 sites in each layer, starting from the homogeneous initial state with all spins up, time steps = 100000)

![](img/55ff3770fcfe64effe3c90a4d4692fa6_463_0.png)

Fig. 10. Specific heat per spin ($C$) versus $K$. (The calculated data are the results for the lattice with 1500 × 1500 sites in each layer, starting from the homogeneous initial state with all spins up, time steps = 100000)

## 4. Constructing the critical curve for anisotropic two-layer models

The previous approach could easily be used for calculation of the critical point of anisotropic two-layer Ising and Potts models which have different interlayer coupling coefficients ($K_1 \neq K_2 \neq K_3$) (Asgari & Ghaemi, 2006 and Asgari & Ghaemi, 2008). The critical points that are obtained for the two-layer Ising model in the case of different values of $\xi=K_2/K_1$ and $\sigma=K_3/K_1$ are given in Table 1.

The results are compared with other numerical methods and it is shown that they are in good agreement. So, this comparison confirms the reliability of our approach. Furthermore, it is clear from the graph of M versus t (Fig. 1) that the critical point could be easily obtained with high precision using the CA approach. In the next step, we have fitted the obtained results which are in Table 1 in order to get a general ansatz equation for the critical point for the anisotropic two-layer Ising model in terms of inter- and intra-layer interactions ($\xi$ and $\sigma$) as,

$$K_C^{-1}=a+b\xi^{1/2}+c\sigma^{1/2}\tag{22}$$

where $a = 0.170937(\pm 0.002708)$, $b = 0.724762(\pm 0.003046)$, and $c = 2.19985(\pm 0.004167)$. This equation could be a reliable way to investigate the critical point for the anisotropic ferromagnetic two-layer Ising model by considering the nearest-neighbor interactions within each layer in the $x$ and $y$ directions and also the inter-layer coupling. So, having the desired values of $\xi$ and $\sigma$, one could obtain the critical point for this model with acceptable precision.

In the next step, we have done similar calculation to obtain the critical points for the anisotropic two-layer Potts model which is shown in Table 2. Some of the results are compared with the recent transfer matrix method and it is shown that they are in good agreement. This comparison shows the reliability of our approach. The results are obtained from the graph of M versus t with high precision (see for example Fig. 2). Then, the obtained results have been fitted in order to obtain a general ansatz equation for the critical point for the anisotropic two-layer Potts model in terms of inter- and intra-layer couplings ($\xi$ and $\sigma$) as follow,

$$K_C^{-1}=a+b\xi^{1/2}+c\sigma^{1/2}\tag{23}$$

where $a = 0.162203(\pm 0.001257)$, $b = 0.246394(\pm 0.003882)$, and $c = 0.800764(\pm 0.003190)$. This equation seems to be a useful expression in order to calculate the critical point for the
