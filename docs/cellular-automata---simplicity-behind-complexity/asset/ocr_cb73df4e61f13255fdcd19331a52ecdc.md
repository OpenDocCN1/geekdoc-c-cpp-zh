is an open biophysical system moving step-wise and randomly in space, aiming at capturing, storing and processing discreet units of matter/energy (resources), thus assuring its “survival”. It can be seen as a black box excited by Poisson impulses and responding with limited spatial displacements through an appropriate transfer function. Due to these mechanical displacements, the resources that are available in the near-by space-environment can be captured. The latter can also be considered as a black box excited by a random step function, giving such energy impulses to the bioautomaton. (Fig. 1)

![](bbox=[0.07, 0.3, 0.93, 0.46])

Fig. 1. Left: Scheme of the bioautomaton/environment interaction; the bioautomaton has an internal reserve of energy. Heat exchange fluxes are not displayed for simplicity. Right: The bioautomaton-medium interaction seen as a closed system; B particle is the bioautomaton and B̄ antiparticle represents the near-by medium; the exchange is given by a discrete flux of resources R and of residues R̄.

The evolution in the state space of the whole system (bioautomaton / environment) is a stochastic process, depending, on one side, on the efficiency of the bioautomaton to collect resources and to adequately use its internal energy reserve and, on the other side, on the environmental offer and its renewal capacity. There will be stationary or quasi-stationary random solutions, as long as the expected value of the rate of energy consumption per period between impulses is higher or equal to the average minimum consumption rate:

⟨ ε_{0i}/T_{gi} ⟩ ≈ ε_0/T_0 ≥ (δε/δt)_{min}          (1)

Eq. (1) can be considered as the *first-class functional* of a bioautomaton or “survival” functional, where (δε/δt)_{min} plays a similar role to basal metabolism in living organisms. Here, the device’s “survival” consists of a set of conditions resulting in the sustenance in time of its internal reactions, within a relatively steady range, balancing dynamically the energetic exchange with the environment.

Since under stationary conditions the bioautomaton’s movement and survival are limited to an optimal use of its internal energy reservoir, a certain potential function can be associated to this storage, as a measure of the probability to capture new resources. This can be defined as a spatiotemporal convolution between a certain window S(r,t), representative of the perception and capture radio of the bioautomaton, and the spatial density of resources ρ(r) (ζ if it’s a process constant):

U_{bio}(r, t) = -1/(2πζ) ∫_S S(r(t) - r') ρ(r') dr'          (2)