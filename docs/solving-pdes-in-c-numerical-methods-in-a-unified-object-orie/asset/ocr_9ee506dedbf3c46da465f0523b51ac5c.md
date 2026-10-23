which are again three linear combinations of the last three columns in J⁻¹. Thus, the last three columns in J⁻¹ span an invariant subspace of S in the sense that S applied to a vector in the subspace produces a vector in it.

From the Jordan form of exp(tS), it follows that the above subspace is invariant for exp(tS) as well. In other words, if the initial-condition vector u₀ lies in the subspace, then so also do all the vectors u(t) at every time t. Therefore, this subspace is called an invariant subspace of the system of ODEs.

If the real part of λ₂ is negative, then this subspace is also called stable, because every initial-condition vector u₀ in it produces a stable solution u(t). The union of all stable invariant subspaces forms the stable invariant subspace of the system of ODEs.

# 6.6 The Inhomogeneous Case

So far, we have considered only homogeneous ODEs, in which only the term Su(t) appears on the right-hand side. Here, we consider also the more general inhomogeneous case, in which a free term f(t) is added:

u′(t) = Su(t) + f(t),

where f is a given function that is integrable (in absolute value) in [0, ∞):

∫₀^∞ |f(τ)| dτ < ∞.

(In systems of ODEs, f is interpreted as a vector function, and the above condition should hold for each of its components.)

The solution to the initial-value problem (with initial condition as before) is

u(t) = exp(tS)u₀ + exp(tS) ∫₀^t exp(−τS) f(τ) dτ

= exp(tS)u₀ + ∫₀^t exp((t − τ)S) f(τ) dτ.

Unfortunately, the above integral is not always available in closed form. In the next section, we’ll see how it can be approximated numerically on a discrete mesh.

# 6.7 Numerical Solution

The numerical solution of an ODE is a numerical approximation to the solution u(t) of the original ODE on a grid of discrete times t₁, t₂, …. Here, we describe some basic numerical methods of obtaining a numerical solution. These methods are also called numerical schemes or discretization methods.

The above formula for the solution of an inhomogeneous ODE gives the analytic solution. However, it is useful only when the integral in the formula is easily calculated. Unfortunately, this integral is rarely available in closed form. Furthermore, the function f on the right-hand side of the ODE may be given only as a machine function, which returns the output f(t) for an input t. In such cases, the integral should be approximated