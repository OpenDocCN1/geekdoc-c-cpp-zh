```
w = exp(-r2) / pi2;                     // distribution function value
r = sqrt(2e0*r2); theta = pi2 * random();          // polar coordinates
x = r * cos(theta); y = r * sin(theta);            // Cartesian projections
}
//==============================================================================
double randMet(double w(double), double delta, int iopt)
//------------------------------------------------------------------------------
// Generates random numbers x with the distribution w(x) by the Metropolis
// method, using a maximal trial step size delta
// iopt = 0 initializes the sequence
//------------------------------------------------------------------------------
{
    static double dx, xrnd;                     // conserved between calls
    if (iopt == 0) xrnd = random();             // initialization
    dx = delta * (2e0*random() - 1e0);          // trial step size
    if (random() <= w(xrnd+dx)/w(xrnd)) xrnd += dx;  // accept with prob. w(x)
    return xrnd;
}
#endif
```

# 11.7 Problems

The Python and C/C++ programs for the following problems may import the functions developed in this chapter from the modules random1.py and, respectively, random.h, which are available as supplementary material. For creating runtime plots, the graphical routines contained in the libraries graphlib.py and graphlib.h may be employed.

# PROBLEM 11.1

Consider the one-dimensional integrals:

1/√(2π) ∫₀^∞ e^{-x²/2} dx = 1/2, (11.42)

1/√(2π) ∫₀^∞ x⁴ e^{-x²/2} dx = 3/2. (11.43)

+   a. Evaluate the integrals by Monte Carlo techniques, applying comparatively uniform and exponential sampling (using function randExp). Consider numbers of sampling points ranging from n = 250 to 100,000, and plot the integral estimates and the associated standard deviations.
+   b. Explain the significant variance reduction when using exponential sampling for the first integral and the lack of effect in the case of the second integral.
+   c. Use the routine LinFit (from modfunc.py) to perform linear regression and extract the scaling laws of the standard deviations for the two probability distributions from their log–log plots.