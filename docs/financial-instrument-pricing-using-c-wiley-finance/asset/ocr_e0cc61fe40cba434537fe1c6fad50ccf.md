```
NumericalIntegrator myQuad;

myQuad.fun = func;
myQuad.ran = Range<double>(0.0, 1.0);

// Integrator is midpoint rule
myQuad.quad = MidpointRule;

std::size_t N = 1000;
std::cout << "Approx integral (Midpoint): " << myQuad(N) << std::endl;

// Integrator is Monte Carlo 'dart throwing'
HitOrMissMonteCarlo mc;
mc.C = 2.0;
myQuad.quad = mc;

N = 1000000;
std::cout << "Approx integral (MC): " << myQuad(N) << std::endl;

// Nasty functions
myQuad.fun = func2;
mc.C = func2(1.0);
N = 1000000;
std::cout << "Approx integral (MC): " << myQuad(N) << ", exact: " << -exp(-1.0) + 1.0 << std::endl;

myQuad.quad = MidpointRule;
N = 1000;
std::cout << "Approx integral (Midpoint): " << myQuad(N) << ", ";
```

The advantages of this approach are:

+   a) We are free to implement the integrand in a number of ways and not just as a free function.
+   b) The GOF Bridge pattern is now redundant because we use std::function<> which is more flexible. The latter class plays the role of the abstraction in the Bridge pattern.
+   c) We overload the function call operator(). This approach promotes standardisation and uniformity.
+   d) Clients have freedom in choosing how they implement schemes. It is no longer necessary to create specialisations of a common base class containing polymorphic functions. We also note improved performance.

This example could serve as a test case for other kinds of applications involving functions and numerical algorithms. We expand on this topic in later chapters.

# 3.10 SUMMARY AND CONCLUSIONS

We have given an introduction to modelling functions in C++. We discussed some new features in C++ such as std::function<> and lambda functions as well as function objects and function pointers. We also gave an introduction to a number of concepts from computer science