![](bbox=[0.22, 0.14, 0.78, 0.38])

# FIGURE 4. Pressure calculated at various depths and evaluated for a periodic traveling waves with h = 0.1, g = 1, L = 2π, and ||η||∞ = 0.01. The solid line represents pressure calculated using the methods outlined in [20]. The symbol ‘o’ represents pressures calculated using (6) while ‘+’ represents pressure calculations made using (28).

minimum value. At this point, the pressure is exactly the prescribed value given by the boundary condition p(x, η) = gη (up to 10⁻¹⁵). Furthermore, Figure 4 (a) examines the pressure along the line z₀ = 0. In this case, we have only drawn the pressure for x values such that (x,0) lies inside or on the boundary of the fluid domain D (see Figure 2(b) for reference).

# 5.2. The Inverse Problem.

We now consider the inverse problem, given p(x,z) measured at some height z = z₀, can we determine η(x). We proceed to only use (28) for this purpose as the wave-speed c is completely eliminated from this formulation. Specifically, using the pressure measured at various depths obtained in the previous section, we numerically solve (28) for the free surface η using a Newton method with an error tolerance of 10⁻¹⁴. As before, we use a pseudo-spectral method with differentiation carried out in Fourier space and multiplication is carried out in physical space.

As an initial guess for our Newton method, we use the zero averaged portion of given pressure which yields a hydrostatic approximation for the free-surface η based on the depth at which the pressure is measured. We find that this initial guess underestimates the peak height of the traveling wave as demonstrated in [14] and seen again in Figures 5(a-c) & 7(a-c). As expected, the error between the initial guess (the hydrostatic approximation for the free surface) and the true free-surface η decreases as z₀ increases from the bottom of the fluid (z = −h) to the free-surface z₀ = η(x).

Specifically, when pressure measurements are made near the free surface for small amplitude waves, the hydrostatic approximation provides a very close estimate to the free-surface η (see for example Figures 6(a) and 8(a) when z₀ =