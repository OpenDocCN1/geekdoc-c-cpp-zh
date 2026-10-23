where:

a(z, w) = 4(1 − z)(1 + z)(1 − w)(1 + w)

and where f̃ tilde is a variant of f.

Discretise this new PDE using the same second-order scheme as in equation (16.6). In the interest of reusability and effort, modify the code to accommodate the form of this new PDE. Test the scheme.

+   b) Compute the relative accuracy of the finite difference schemes based on domain truncation and domain transformation. Incidentally, we shall use the domain transformation technique to transform a PDE on a semi-infinite interval to a PDE on the unit interval. We discuss this technique in Chapter 23.
+   c) Modify the class GoursatFdmExtrapolation to support the new PDE and test its accuracy.

# 2. (Modelling Bivariate t-Distribution, Medium-Size Project)

Apply the finite difference method to compute the BVT. The possible definitions are (Cornish, 1954; Genz, 2004):

Tᵥ(b, ρ) = 1/(2π√(1−ρ²)) ∫_{-∞}^{b₁} ∫_{-∞}^{b₂} f(x₁,x₂; ρ, ν) dx₂ dx₁,   b = (b₁,b₂)ᵀ

where:

f(x₁,x₂; ρ, ν) = ( 1 + (x₁² + x₂² − 2ρx₁x₂)/((1−ρ²)ν) )

and

Tᵥ(b, ρ) = 2^{1−ν/2}/Γ(ν/2) ∫₀^{∞} f(s,b; ρ, ν) ds

where:

f(s,b; ρ, ν) = s^{ν−1} e^{−s²/2} M( s/√ν b₁, s/√ν b₂, ρ )

and Γ(z) is the Gamma function, Γ(z) = ∫₀^{∞} x^{z−1} e^{−x} dx.

Answer the following questions:

+   a) Apply the finite difference method to compute the above integrals. The class GoursatFdm can be used without modification as it has been designed to operate with any two-dimensional distribution.
+   b) Determine whether domain transformation or domain truncation is better as a means of reducing the region of integration to a bounded domain in this case.
+   c) Test and debug the new code by first taking examples whose values you know (for example, the integral should be 1 for the complete domain). This would be the first ‘sanity’ check.