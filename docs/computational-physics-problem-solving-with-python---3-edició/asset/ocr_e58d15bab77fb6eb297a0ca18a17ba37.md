Decompose this into its components; then check that there are three of them in the ratio 5 : 2 : 1 (or 25 : 4 : 1 if a power spectrum is plotted) and that they resume to give the input signal.

+   4. Sample the signal
+   
+   y(t) = 5 + 10 sin(t + 2) .
+   
+   Compare and explain the results obtained by sampling (a) without the 5, (b) as given but without the 2, and (c) without the 5 and without the 2.

5. In our discussion of aliasing, we examined Figure 12.2 showing the functions sin(πt/2) and sin(2πt). Sample the function

y(t) = sin (πt/2) + sin(2πt)

(12.50)

and explore how aliasing occurs. Explicitly, we know that the true transform contains peaks at ω = π/2 and ω = 2π. Sample the signal at a rate that leads to aliasing, as well as at a higher sampling rate at which there is no aliasing. Compare the resulting DFTs in each case and check if your conclusions agree with the Nyquist criterion.

# Highly nonlinear oscillator

Recall the numerical solution for oscillations of a spring with power p = 12 (see (12.1)). Decompose the solution into a Fourier series and determine the number of higher harmonics that contribute at least 10%; for example, determine the n for which |b_n/b_1| < 0.1. Check that resuming the components reproduces the signal.

# Nonlinearly perturbed oscillator

Remember the harmonic oscillator with a non-linear perturbation (8.2):

V(x) = 1/2 k x^2 (1 - 2/3 a x) , F(x) = -k x (1 - a x) . (12.51)

For very small amplitudes of oscillation (x << 1/a), the solution x(t) essentially should be only the first term of a Fourier series.

+   1. We want the signal to contain “approximately 10% nonlinearity.” This being the case, fix your value of a so that a x_max ≈ 10%, where x_max is the maximum amplitude of oscillation. For the rest of the problem, keep the value of a fixed.
+   
+   2. Decompose your numerical solution into a discrete Fourier spectrum.
+   
+   3. Plot a graph of the percentage of importance of the first two ω, non-DC Fourier components as a function of the initial displacement for 0 < x_0 < 1/2a. You should find that higher harmonics are more important as the amplitude increases. Because both even and odd components are present, Y_n should be complex. Because a 10% effect in amplitude becomes a 1% effect in power, make sure that you make a semilog plot of the power spectrum.
+   
+   4. As always, check that resumations of your transforms reproduce the signal.

> (Warning: The ω you use in your series must correspond to the true frequency of the system, not the ω_0 of small oscillations.)