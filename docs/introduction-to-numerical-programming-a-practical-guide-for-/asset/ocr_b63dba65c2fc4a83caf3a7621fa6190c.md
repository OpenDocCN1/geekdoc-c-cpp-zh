where ρ is the density of the air (1.2 kg/m³) and A = πR² is the cross-sectional area of the hammer. The hammer can experience, in principle, either a “laminar-separated” flow, with a typical drag coefficient C_d = 0.5, or an “unsteady-oscillating” flow, with C_d = 0.75.*

+   a. Solve Newton’s equation of motion for the oblique throw of the hammer using Euler’s predictor–corrector method with a time step h = 0.01, transforming first the ODEs for the x and y motions into a system of four first-order ODEs. Consider throws from the initial position x₀ = 0, y₀ = 2 m, under the ideal angle φ = 45° and find the initial velocity that produces the throw distance of the world record.

+   b. Calculate and plot the time dependence of the hammer’s altitude and its trajectory y = y(x) in three flow regimes: (a) frictionless, (b) laminar-separated flow, and (c) unsteady-oscillating flow. Evaluate the amount by which the throw distance is influenced by the drag.

+   c. Solve the same problem employing the Euler–Cromer and Verlet methods. Use the step-halving technique to estimate the error affecting the throw distance for each of the employed methods and discuss the results with respect to their known orders of precision.

# Solution

The equivalent Cauchy problem for first-order equations, using the notations y₁ = x, y₂ = y, y₃ = vₓ, and y₄ = v_y, reads:

⎧ y₁′ = y₃,          y₁(0) = x₀,
  y₂′ = y₄,          y₂(0) = y₀,
  y₃′ = −(k/m) y₃ |y₃| ,   y₃(0) = vₓ₀,
  y₄′ = −(k/m) y₄ |y₄| − g,   y₄(0) = v_y₀.    (12.111)

The Python program based on the Euler predictor–corrector method is presented in Listing 12.22. The corresponding C/C++ implementation is available as supplementary material (P12–ThrowPCg.cpp), along with the variants using the Euler–Cromer method

![](bbox=[0.15, 0.6, 0.85, 0.85])

FIGURE 12.11 Time-dependent altitude and trajectory of a hammer thrown under 45° and experiencing quadratic drag, as yielded by Euler’s predictor–corrector method (for Problem 12.2).

* https://www.grc.nasa.gov/www/k-12/airplane/dragsphere.html