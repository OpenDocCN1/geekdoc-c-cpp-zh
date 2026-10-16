E = R i + L \frac{di}{dt} = R i + 10^{-5} \frac{d\Phi}{dt}

where L = self-inductance (henrys), R = resistance (ohms), and t = time (sec). Assume N = 100 and R = 500. Then

\frac{d\Phi}{dt} = E - 2.5\Phi' - 0.015\Phi^3, \quad \Phi(0) = 0

where t is now measured in milliseconds. For E = 20 V, solve this initial-value problem in the interval [0, 2] using a step size Δt = 0.01.

# 33. The number of individuals in a population is measured each year. Let P(t) denote the population at year t. Let α denote the birthrate, and assume that the death rate β is proportional to the size of the population, that is, β = γ P(t), where γ is a constant. Hence, the growth rate of the population is given by the logistic equation P'(t) = α P(t) − γ [P(t)]². Assume that P(0) = 50,000, α = 3 × 10⁻², and γ = 1.5 × 10⁻⁷. Solve this initial-value problem with step size Δt = 0.01 to find the population after 5 years.

# 34.–38. The Runge-Kutta method is a popular and one of the most accurate numerical methods for solving a first-order differential equation y' = f(x, y) with initial condition y(x₀) = y₀:

+   1. Select an x-increment Δx.
+   2. The approximate solution yₙ₊₁ at xₙ₊₁ = x₀ + (n + 1)Δx for n = 0, 1, 2, … is given by
+   
+   yₙ₊₁ = yₙ + \frac{1}{6}(K₁ + 2K₂ + 2K₃ + K₄)

where

K₁ = Δx · f(xₙ, yₙ)

K₂ = Δx · f(xₙ + \frac{Δx}{2}, yₙ + \frac{K₁}{2})

K₃ = Δx · f(xₙ + \frac{Δx}{2}, yₙ + \frac{K₂}{2})

K₄ = Δx · f(xₙ + Δx, yₙ + K₃)

Write a program to implement the Runge-Kutta method and use it to solve Problems 29–33.