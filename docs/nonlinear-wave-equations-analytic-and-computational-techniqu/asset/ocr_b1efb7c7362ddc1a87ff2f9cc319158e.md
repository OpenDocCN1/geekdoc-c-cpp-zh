limit; these caustics are one of the dramatic features of the semiclassical behavior (see Figure 2 below). Indeed, in §3.3 we show new, previously unpublished, computations by the numerical inverse scattering technique originally proposed and implemented by Miller & Kamvissis [26] and later refined by Lyng & Miller [22]. These computations show, in addition to the previously studied primary and secondary caustics, the presence of a tertiary caustic. Lastly, in §4 we describe a coordinated collection of numerical experiments (taken from [17,20,21]) aimed at exploring the connections between the limiting behavior of the SSE and the corresponding true solutions, and, in §§5, we discuss possible future developments related to SSEs and their role in the theory of the semiclassical limit problem.

# 2. REMARK (Other aspects of the semiclassical focusing NLS equation).

We shall confine our discussion here to the issues related to SSEs, and we shall not touch on other aspects of the fashionable semiclassical limit problem. However, we do note that substantial progress has been made in recent years on other fronts including, for example, the following.

+   (a) A detailed analysis of the nonlinear caustics and their “universal” properties has been undertaken by Bertola & Tovbis [3,4]; see also [11].

+   (b) Tovbis, Venakides, & Zhou [31–33] have written extensively about this problem. Much of their work is based on a particular one-parameter family of complex data (with nontrivial phase) identified by Tovbis & Venakides [30]. For certain parameter values, their data generates no solitons (a case in some ways the opposite of the case considered here), and in this setting they are able to establish the long-time (t → ∞) behavior of the semiclassical limit.

+   (c) Tovbis & Venakides [29]—sidestepping WKB issues by using a kind of complexified Abel transform—have recently proposed an alternative approach to the forward scattering map in the semiclassical regime.

# 2. Background & framework

# 2.1. Inverse scattering transform & the nonselfadjoint Zakharov–Shabat problem.

The construction of the SSE is intimately connected to the integrability of the nonlinear equation (1.1). We recall that Zakharov & Shabat [34] discovered a Lax pair for the NLS equation. That is, they showed that nonlinear equation (1.1) can be represented as the compatibility condition for two auxiliary linear problems, and this structure allows one to construct solutions of the initial-value problem by the IST. For (1.1), (1.2), the first of these auxiliary problems is the eigenvalue problem

```
(2.1) ε d/dx w = [ -iλ  A0 ; -A0  iλ ] w .
```

In (2.1), we have written w(x; λ, ε) = (w1(x; λ, ε), w2(x; λ, ε))ᵀ for the solution and λ ∈ ℂ is the eigenvalue parameter. As above, the real parameter ε is assumed to be positive but small. Our principal interest here are those values of λ ∈ ℂ for which (2.1) has a solution in L²(ℝ)²; these values comprise the discrete spectrum—the eigenvalues. In addition, to fully implement the IST, we recall that the essential properties of the data for the initial-value problem are encoded in the scattering data. In addition to the eigenvalues, this includes the norming constants, and the reflection coefficient. In the construction of the SSE, the reflection is assumed to