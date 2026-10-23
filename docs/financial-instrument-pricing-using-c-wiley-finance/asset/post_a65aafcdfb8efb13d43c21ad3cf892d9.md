
We use `std::transform` to create arrays and we also use the Excel driver that we introduced in Chapter 14:

```cpp
template <typename T, template <typename T> class Dist>
    void DisplayDistributionCurves(const Distribution<T, Dist>& dist,
                                   T a, T b, std::size_t N)
{ // Display a number of functions of a distribution as line graphs

    // Try to use as much of standard C++ and STL as possible

    // A. Create abscissa array
    T h = (b - a) / static_cast<T>(N);
    std::vector<T> x(N+1, h);
    x[0] = a;
    for (std::size_t i = 1; i < x.size(); ++i)
    {
        x[i] = x[i - 1] + h;
    }

    // B. Create arrays for pdf, cdf and hazard functions
    std::vector<T> pdf(x.size());
    std::transform(std::begin(x), std::end(x), std::begin(pdf),
                   [&](T t) { return dist.pdf(t); });

    std::vector<T> cdf(x.size());
    std::transform(std::begin(x), std::end(x), std::begin(cdf),
                   [&](T t) { return dist.cdf(t); });

    // C. Labels and assemble input for Excel
    std::list<std::string> labels{"pdf", "cdf"};

    // The list of Y values
    std::list<std::vector<double> > curves{pdf,cdf};

    ExcelDriver xl; xl.MakeVisible(true);
    xl.CreateChart(x, labels, curves, "pdf", "cdf", "x", "y");
}
```

In other words, we create a single object and we call two of its member functions (`pdf` and `cdf`). An example of use is:

```cpp
double a = 0.0; double b = 6.0;
std::size_t n = 50;
DisplayDistributionCurves(normalDist,a,b,n);
```

The output is shown in Figure 15.7.

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_519_0.png)

**FIGURE 15.7** Normal distribution

We now give an example of the *non-central chi-squared distribution*. Its constructor takes two parameters *k* and *λ* that represent the *number of degrees of freedom* and the *non-centrality parameter*, respectively. The code is:

```cpp
void DisplayNonCentralChiSquared(double a, double b, std::size_t N)
{
    // Display non-central chi^2 pdf for a range of k and lambda.

    using T = double;

    // A. Create abscissa array
    T h = (b - a) / static_cast<T>(N);
    std::vector<T> x(N + 1, h);
    x[0] = a;
    for (std::size_t i = 1; i < x.size(); ++i)
    {
        x[i] = x[i - 1] + h;
    }

    // B. Create arrays for pdf for different values of k and lambda
    Distribution<T, DistNCChiSquared> dist21(2,1);
    Distribution<T, DistNCChiSquared> dist22(2, 2);
    Distribution<T, DistNCChiSquared> dist43(4, 3);

    std::vector<T> pdf21(x.size());
    std::transform(std::begin(x), std::end(x), std::begin(pdf21),
        [&](T t) { return dist21.pdf(t); });

    std::vector<T> pdf22(x.size());
    std::transform(std::begin(x), std::end(x), std::begin(pdf22),
        [&](T t) { return dist22.pdf(t); });

    std::vector<T> pdf43(x.size());
    std::transform(std::begin(x), std::end(x), std::begin(pdf43),
        [&](T t) { return dist43.pdf(t); });

    // C. Labels and assemble input for Excel
    std::list<std::string> labels{
        "k=2, lambda = 1", "k=2, lambda = 2", "k=4, lambda = 3" };

    // The list of Y values
    std::list<std::vector<double> > curves{ pdf21, pdf22, pdf43 };

    ExcelDriver xl; xl.MakeVisible(true);
    xl.CreateChart(x, labels, curves, "NonCentral Chi^2 pdf", "x", "y");
}
```

An example of use is:

```cpp
std::size_t M = 10;
double L = 0.01; double R = 8.0;
DisplayNonCentralChiSquared(L,R, M);
```

The output is shown in Figure 15.8.

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_520_0.png)

**FIGURE 15.8** Modifying parameters

## 15.8 SUMMARY AND CONCLUSIONS

In this chapter we introduced two C++ libraries that support random number generation and univariate statistical distributions, namely the standard C++ `<random>` library and the Boost Statistics library. We discussed the functionality that they deliver and we gave some applications to option pricing and to computing option sensitivities. We also created two generic classes that encapsulate the functionality of the distributions in `<random>` and Boost. Finally, we also showed how to create input datasets to numerical processes based on random number generators.

## 15.9 EXERCISES AND PROJECTS

### 1. (PDE and Numerical Analysis Project)

In this exercise we reduce the one-factor Black–Scholes PDE to a simpler heat equation PDE that we then solve using the finite difference methods that we introduced in Chapter 13. The PDE is:

∂V/∂t + ½ σ² S² ∂²V/∂S² + r S ∂V/∂S − r V = 0

and let us define the new variable u by:

V(S, t) = e^{αx + βτ} u(x, τ)

where:

α = −½ (2r/σ² − 1)

β = −¼ (2r/σ² + 1)²

S = e^{x}, t = T − 2τ/σ².

We can then show that the function u satisfies the heat equation:

∂u/∂τ = ∂²u/∂x².

Answer the following questions:

- a) Check that the above transformation leads to a heat equation PDE on an infinite interval.

- b) Let h(x) be the payoff (initial condition) corresponding to the new heat equation. It can be shown (Tolstov, 1962) that the solution is:

  u(x, τ) = 1/(2√(πτ)) ∫_{−∞}^{∞} h(v) e^{−(x−v)²/(4τ)} dv.

  Compute this solution numerically using your favourite numerical quadrature scheme. For example, we could use Tanh–Sinh quadrature (Takahasi and Mori, 1974) which uses a transformation of the interval (−1, 1) to the real line. The integrand decays at a double-exponential rate. For this reason the method is also known as the *double-exponential (DE) formula*.

- c) Now approximate the heat equation using the Crank–Nicolson and ADE (Barakat and Clark variant) methods that we introduced in Chapter 13. You will need to truncate the (infinite) domain of integration to a bounded interval in the space direction and apply numerical boundary conditions.

- d) Compare the relative accuracy of the methods in part c). Use the Excel driver software from Chapter 14 to visualise the option price as an array of values at expiration.

- e) Compare the values produced by the finite difference method with the solution based on the error function.

### 2. (Computing Option Sensitivities/Greeks, Small Project)

We focus on computing an option’s delta and gamma. *Delta* is an option’s sensitivity to small changes in the underlying asset price while *gamma* is the delta’s sensitivity to small changes in the underlying asset price. The objective is to use a number of methods to compute delta and gamma and then to analyse their results:

- Analytical solutions (see Haug, 2007 for an extensive list of formulae).
- Numerical Greeks (Haug, 2007). In this case we use divided differences to compute delta and gamma, as discussed in a more general setting in Chapter 8. The advantage is that this approach is model independent. The disadvantage is that numerical differentiation is an ill-posed process in general.
- Using cubic splines as discussed in Chapter 13. See also Exercise 3 in Chapter 13.

Answer the following questions for the case of a call option:

- a) Create an array of stock prices and compute the corresponding array of option prices for each stock price (keeping the other parameters constant).

- b) Compute the arrays containing the delta and gamma values for each stock price. Use analytical formulae for delta and gamma (see Haug, 2007, for example).

- c) Compute the arrays containing the delta and gamma values for each stock price. Use divided difference formulae for delta and gamma (see Chapter 8).

- d) Approximate the values in part a) using cubic splines. Apply formulae (13.38) and (13.37) to approximate delta and gamma, respectively.

- e) Compare the solutions in parts b), c) and d) by displaying them in Excel using the software from Chapter 14. Do you see major differences in the accuracy produced by the different solutions?

- f) Compare the relative run-time performance of the methods. Which one performs best?

### 3. (Computing Option Sensitivities/Greeks Part II, Small Project)

This exercise is in a sense a mirror image of Exercise 2 except that in this we use the array of option prices that are generated by the finite difference method instead of the analytical option price as used in Exercise 2 (Chapters 20 to 25).

Answer the following questions:

- a) Create an array of stock prices and compute the corresponding array of option prices for each stock price (keeping the other parameters constant). Use the Crank–Nicolson method to generate the array of option prices.

- b) Compute the arrays containing the delta and gamma values for each stock price. Use divided differences for delta and gamma (see Chapter 8). Experiment with forward, backward and centred differencing.

- c) Approximate the values in part a) using cubic splines. Use formulae (13.38) and (13.37) to approximate delta and gamma, respectively.
