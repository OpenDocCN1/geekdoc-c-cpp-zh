# 14.11.5

# Two Predators, One Prey (Exploration)

+   1. Another version of the LVM includes the possibility that two populations of predators P₁ and P₂ may “share” the same prey population p. Investigate the behavior of a system in which the prey population grows logistically in the absence of predators:
+   
+   \[ \frac{dp}{dt} = a p \left(1 - \frac{p}{K}\right) - (b_1 P_1 + b_2 P_2) p \tag{14.53} \]
+   
+   \[ \frac{dP_1}{dt} = \epsilon_1 b_1 p P_1 - m_1 P_1, \quad \frac{dP_2}{dt} = \epsilon_2 b_2 p P_2 - m_2 P_2 \tag{14.54} \]
+   
+   a) Use the following values for the model parameters and initial conditions: a = 0.2, K = 1.7, b₁ = 0.1, b₂ = 0.2, m₁ = m₂ = 0.1, ε₁ = 1.0, ε₂ = 2.0, p(0) = P₂(0) = 1.7, and P₁(0) = 1.0.
+   b) Determine the time dependence for each population.
+   c) Vary the characteristics of the second predator and calculate the equilibrium population for the three components.
+   d) What is your answer to the question, “Can two predators that share the same prey coexist?”

+   2. The nonlinear nature of the Lotka–Volterra model can lead to chaos and fractal behavior. Search for complex behaviors by varying the growth rates.