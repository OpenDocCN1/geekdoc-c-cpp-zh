*key for any model development; its precise specification enables a clear and compact formulation of the model* (Bessel 1992; Fischer (2006).

# 2. Modeling techniques

Numerical simulation is typically based on continuous models. Problems, which consider independent variables e.g. spatial elements and time can be modeled using partial differential equations (PDE), and problem without considering more independent variables can be formulated using ordinary differential equations (ODE). Furthermore, cellular automata can be used for modeling spatiotemporal problems.

# 2.1 Ordinary differential equations

As one example the Lotka-Volterra-Equation Volterra (1926), which is also know as Predator-Prey-Equation, is a mathematical system based on coupled differential equations, which describe the dynamics of predator and prey populations. The equations are based on three rules, which were constructed during World War II on observations of the fish stock in the Adria. The first rule describes the periodical fluctuations of a population. The fluctuations of the predator-population are phase-delayed compared to the prey-population. The second rule describes the stability of the mean value. Although there are periodical fluctuations, the number of the populations is constant. The last rule describes that the prey-population is growing faster than the predator-population. If predator- and prey-population becomes decimated for a defined period, then the prey-population recovers always faster than the predator-population.

This situation can be mathematical modeled using ordinary differential equations:

$$\frac{dx}{dt}=x(\alpha-\beta y) \tag{2}$$

$$\frac{dy}{dt}=y(\delta x-\gamma), \tag{3}$$

where y is the number of predator-population, x is the number of prey-population, t represents the time, $\frac{dx}{dt}$ and $\frac{dy}{dt}$ represents the growth of the given populations against time. α is the exponential growing rate of the prey population, β is the predator-capture-rate, δ is the reproduction rate of the predator population, and γ the natural predator death rate.

Models of this type are of importance in theoretical biology, and in epidemiology e.g. for describing the processes of disease spreading.

The disadvantage is, that the result describes the behavior of the whole population without having the chance to look at each individual directly. Another point is, that it is impossible to model topological structures, which may get important for some simulation cases.

# 2.2 Partial differential equations

As described, using ordinary differential equations enables only to model one dimension. Therefore, in the Predator-Prey-Model the overall behaviors over the time can be modeled and expressed. Partial differential equations, however, consider change of state along several dimensions.

The Predator-Prey-Model can be extended using PDEÖs for modeling spatial variations. These variations are that a predator has to move in order to catch a prey, and a prey is able to move for evading a predator. The model can be described as following: