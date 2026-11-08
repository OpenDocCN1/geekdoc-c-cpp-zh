# 5.1 Distribution of technological levels in cellular automata – extreme order statistics

In order to give a quantitative characterization of the time evolution of the cellular automata on a square lattice, we determined the distribution $p_t(τ)$ of technological levels $τ$, and the mean $⟨τ^t⟩$ of technological levels at different times $t$.

$⟨τ^t⟩ = \frac{1}{N}\sum_{i=1}^{N} τ_i^t$  (24)

where $N$ denotes the total number of agents.

![](bbox=[0.161, 0.256, 0.868, 0.381])

Fig. 7. Probability distribution of technological levels $p(τ)$ obtained at different time values for three different values of the cost factor $r$. (a) For the case of $r = 1$ the rescaled plot of the distributions is presented, i.e. the distributions obtained at different times are rescaled by the mean $⟨τ^t⟩$ and by the standard deviation $σ^t$ of the distributions. The master curve obtained perfectly agrees with the standard Gaussian. (b) For $r = 2$ when the second largest technological level is favored locally by agents, the distributions converge to a highly peaked functional form. (c) In the range $r > 3$ agents always select the most advanced technology, hence, the distributions can be viewed as described by extreme order statistics represented by the continuous lines.

Figure 7(a) shows that for $r = 1$, when higher level technologies do not provide advantages for agents, the distribution $p_t(τ)$ rapidly attains a Gaussian shape. In order to demonstrate the validity of the assumption, we present the rescaled distributions in the figure: the distributions obtained at different times are rescaled by the average technological level $⟨τ^t⟩$ of the corresponding state and by the standard deviation of the distribution $σ^t$ so that $p_t(τ)/σ^t$ is plotted as a function of $(τ − ⟨τ^t⟩)/σ^t$. The high quality data collapse that can be seen in Fig. 7(a) and the good quality fit with the standard Gaussian

$g(x) = \frac{1}{\sqrt{2π}}\exp(−x^2/2)$  (25)

demonstrate the validity of the Gaussian description of the evolution of the cellular automata. The convergence to the Gaussian is very fast. In our test simulations after 30–40 iteration steps the system completely forgot its initial uniform state and $p_t$ attained the Gaussian limit distribution. This form implies that the fraction of agents having very high and very low level technologies both decrease and agents tend to copy technologies in the vicinity of the distribution mean. Consequently, the system does not have any technological progress, the average technological level remains nearly constant during the time evolution, and $⟨τ^t⟩ → 0.5$.

For the cost factor $r > 1$ agents locally prefer to adopt higher level technologies, namely, the highest or the second highest $τ$ value of the neighborhood will be adopted on the square lattice.