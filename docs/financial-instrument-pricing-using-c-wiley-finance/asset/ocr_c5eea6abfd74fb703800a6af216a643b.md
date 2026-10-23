area, both on the continuous problem and its discrete formulations (for example, using finite difference and finite element methods).

The essence of the finite difference method is to discretise equations (20.14)–(20.16) by defining *discrete mesh points* and approximating the derivatives of the unknown solution of this system at these mesh points. The goal is to find accurate schemes that will be implemented in a programming language such as C++ and C#. Some typical attention points are:

+   - The PDE being approximated may need to be preprocessed in some way, for example transforming it from one on a semi-infinite domain to one on a bounded domain.
+   - Determining which specific finite difference scheme(s) to use based on requirements such as accuracy, efficiency and maintainability.
+   - Essential difficulties to resolve: *convection dominance*, avoiding oscillations and how to handle discontinuous initial conditions, for example.
+   - Developing the algorithms and assembling the discrete system of equations prior to implementation.

# 20.3 PDE PREPROCESSING

A PDE is defined in a region of two-dimensional space defined by the variables x (the underlying space) and time t. Regarding the x variable, the range of values can be:

−∞ < x < ∞ (infinite domain)
0 < x < ∞ (semi-infinite domain)
A < x < B, where −∞ < A < B < ∞ (bounded domain).

When approximating PDEs by FDM the underlying domain must be transformed to a bounded domain. Thus, we can decide to modify the PDE in some way before approximating it by the FDM:

+   - Change the coefficients of the PDE.
+   - Truncate an infinite or semi-infinite domain to a bounded domain.
+   - Transform an infinite or semi-infinite domain to a bounded domain by a change of independent variables.
+   - Change the structure of a PDE (for example, we can use an *integrating factor* to transform a non-conservative PDE to a conservative PDE).

It is important to determine what the consequences are when modifying a PDE. We now discuss each of the above topics.

# 20.3.1 Log Transformation

This is a popular method to transform the Black–Scholes PDE on a semi-infinite interval to a PDE with constant coefficients on an infinite interval. For example, we define