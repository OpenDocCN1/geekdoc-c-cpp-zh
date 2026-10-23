The rationale is that an automated procedure can be run without human intervention and it produces a management report (for example, the results could be stored in a database) on the quality of the finite difference scheme that we are testing. In order to scope the problem we consider testing ADE against the Crank–Nicolson (CN) method and we can assume that the results produced by CN are accurate. Some of the features and requirements (accuracy and efficiency are the most important quality issues) are:

+   - F1: Test the accuracy of ADE against CN. Determine those regions in which ADE produces values that deviate from those produced by CN.
+   - F2: Test the robustness of ADE for a range of input parameters (which may be randomly generated).
+   - F3: Investigate the accuracy in the case of convection dominance, large and small expiration and other stressful cases.
+   - F4: Examine performance and accuracy of the different ADE variants for a range of mesh sizes and time steps.
+   - F5: Compute option sensitivities (in particular, delta and gamma).

Answer the following questions:

+   - a) Apply the methods in Chapter 9 to scope this problem by creating a system context diagram, describing what the major output and input are and how the core process maps input to output.
+   - b) Determine the interfaces of the modules in the system context diagram. Implement each module as an adapter class that reuses existing code.
+   - c) Determine how to model the input data. In an initial version it can be hardwired in the code. If time permits you can consider using XML files, regular expressions (C++ has a regex library) or the Boost Parameter library. An important part of the project is to define the data structures to hold both the input data and the generated output data.
+   - d) Do you see any opportunities for parallelising the code?

# 3. (Numerical Integrals and Derivatives with Cubic Splines, Small Project)

We gave an example in Section 22.3.3 of using a cubic spline to approximate a function and its derivatives. We also saw in Chapter 13 that cubic splines can be used for numerical integration (see also Stroud, 1974 for a mathematical discussion).

The main goal of this exercise is to determine how to use cubic splines in your applications as a competitor to other methods. Some of the reasons for doing so could be:

+   - Other methods may not be robust enough.
+   - Cubic splines have many applications and are easy to use.
+   - Cubic splines are accurate and have good performance characteristics.

Answer the following questions:

a) Compute the following integrals using cubic splines with different mesh sizes. How does the accuracy compare with the exact values and with those produced by other numerical integration rules (for example, the Gaussian methods that we discussed in Chapter 8)?

∫₁² dx/x (exact value 0.69314718055)
∫₀¹⁰ dx/(1 + x²) (exact value 1.471127674304)
∫₀ˣ e^(-y²/2) dy where 0 < x < ∞.