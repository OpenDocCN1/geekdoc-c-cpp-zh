# Fault Injection and Failure Monitoring

# 621

![](bbox=[0.118, 0.095, 0.875, 0.245])

**Figure 26.3** a $\lambda(s) \times s$ and $b$ $MTTF(s) \times s$,

The mean square error for the model shown above and the respective data points are $RMSE = 4.66 \times 10^{-4}$. Extrapolating $s$ to normal operation conditions, $s = 1$, we obtain $\hat{\lambda} = 1.776 \times 10^{-3}$ fph (a constant failure rate at normal);); $MTTF = 575.26h$. Regression models are one of the most popular statistical procedures used for forecasting, and many of such models could be applied to data sets according to their trends.

# Arrhenius Model

In 1889, Svante August Arrhenius¹ proposed an equation that combines the concepts of temperatures and rates of chemical reactions [23, 378]. More precisely, Arrhenius’ model relates the concepts of activation energy and the Boltzmann probability distribution. The Boltzmann distribution (also called Gibbs distribution) provides the probability of a specific system state as a function of the state’s energy and temperature [122]; that is

$p_i = \frac{e^{\frac{E_i}{kT}}}{\sum_{j=1}^{m} e^{\frac{E_j}{kT}}}$,

where $p_i$ is the probability of the system being in state $i$, $E_i$ is the energy of that state, $m$ is the number of all accessible states in the system, and a constant $kT$ of the distribution is the product of Boltzmann’s constant ($k = 8.62 \times 10^{-5}$ eV/K) and thermodynamic temperature $T$ (in Kelvin).

The Arrhenius formula characterizes the dependency between the reaction rates (r), the system temperature, and the activation energy ($E_a$).

$r = F \times e^{-\frac{E_a}{kT}}$, (26.1.12)

> ¹A Swedish physicist who received the Nobel Prize for Chemistry in 1903 [378].