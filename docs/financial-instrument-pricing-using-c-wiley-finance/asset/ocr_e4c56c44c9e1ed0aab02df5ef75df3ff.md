The C++ class that models the PDE in equation (23.6) based on the new coordinates becomes:

∂V/∂t = 1/2 σ² (S/A) x²(1−x)² ∂²V/∂x² + { r x(1−x) − σ² x²(1−x)² } ∂V/∂x + (γ (S−A)(1−y)² / b) ∂V/∂y − r V
for 0 < x < 1, 0 < y < 1 ( S = a x / (1−x), A = b y / (1−y) ). (23.7)

We thus see that equation (23.7) is a PDE defined on the unit square (0,1)×(0,1). In order to describe the resulting initial boundary value problem we need to impose boundary conditions. For x = 0 and x = 1 we impose the well-known boundary conditions that apply to plain call or put options. For y = 0 and y = 1 no boundary conditions are needed, as mentioned in WLD (2014). This fact can be verified and motivated by application of the Fichera theory (see Duffy, 2009; Duffy and Germani, 2013) or by the method of characteristics.

# 23.4 THE ANCHORING PDE

The financial background to the current problem is given in WLD (2014). We define a volatility function σ(ξ), where ξ = S/A and the model is:

dS = μ S dt + σ(ξ) S dW. (23.8)

We model the problem as one with memory. To this end, we define a variable A that represents an average or an anchoring value. One of the simplest and most tractable models is given by the following sigmoidal function:

σ(ξ) = a + (b − a) / (1 + e^{−c(log ξ − d)}). (23.9)

where a, b, c and d are known parameters.

The form of this function has been determined from time series (see WLD, 2014) and it will be used as the volatility function in the PDE that is represented in equations (23.6) and (23.7).

Moving to C++ design of the anchoring PDE, we first note that it plays the role of the implementer of TwoFactorAsianPde in the Bridge pattern. It is an instance of TwoFactorAsianPde that is created by a factory method. In this case we choose from the following alternatives:

+   A1: Defining the PDE components in a namespace.
+   A2: Creating a void function that initialises an already created reference to an instance of TwoFactorAsianPde.
+   A3: A factory method (as discussed in GOF, 1995) that creates an instance of std::shared_ptr<TwoFactorAsianPde<double>>.