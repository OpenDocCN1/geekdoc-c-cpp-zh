Note that Equation (9.2) is in bounded domains in ℝ³, and when n=2 the number 2* formally becomes ∞ but Equation (9.2) does not hold with p=∞ in this case. However one can show that:

Let Ω be a bounded domain in ℝ², then for any 1 ≤ p < ∞, there exists an optimal constant C_{p,Ω} > 0 such that

C_{p,Ω} [∫_Ω |u|^p dx]^{2/p} ≤ ∫_Ω |∇u|² dx  (9.3)

holds for all u ∈ C_c¹(Ω). Moreover C_{p,Ω} → 0 as p → ∞.

These inequalities play an important role in the analysis of partial differential equations, especially the ones in variational form. First recall if (X,‖·‖_X) and (Y,‖·‖_Y) are normed linear spaces and f : U → Y for an open subset U of X then f is said to be Fréchet differentiable at x₀ ∈ U if there exists an L ∈ BL(X,Y), satisfying

lim_{h→0} ‖f(x₀+h)−f(x₀)−L(h)‖_Y / ‖h‖_X = 0

The bounded linear map L if it exists is unique and is called the Fréchet derivative of f at x₀ and is denoted by Df(x₀). Also we say that x₀ is a critical of f if Df(x₀)=0.

Solutions of certain PDEs appear as the critical points of some functions defined on appropriate function spaces. For example one can easily see that solutions of the boundary value problem

−Δu = f(u)  in Ω
 u = 0      on ∂Ω  }  (9.4)

where f is sufficiently regular, appear as the critical points in the suitable function space of the corresponding energy

E(u)= 1/2 ∫_Ω |∇u|² dx − ∫_Ω F(u) dx  (9.5)

where F is the primitive of f given by F(t)=∫₀ᵗ f(s) ds. A natural space where one would define this energy is where ∫_Ω |∇u|² dx < ∞. In this space if the energy has to be well defined then ∫_Ω F(u) dx has to be finite which follows if we can control ∫_Ω F(u) by ∫_Ω |∇u|² and the latter is finite. Note that if f has polynomial growth of appropriate order then Equation (9.2) assures that E is well defined in H₀¹(Ω).

In the two-dimensional case if f has polynomial growth of any order, Equation (9.3) makes the energy well-defined in H₀¹(Ω). However, there are semilinear PDEs coming from geometry, physics,etc. where we have to deal with nonlinearities which are of the exponential type. Let us see two examples.

First let us consider the problem of prescribing the Gaussian curvature on a two-dimensional manifold in a conformal way. Let (M,g) be a two-dimensional Riemannian Manifold, and 	ilde{g}=e^{2u}g be a metric conformal to g. Suppose the Gaussian curvatures of g and 	ilde{g} are denoted by k_g and k_{	ilde{g}} respectively. Then the Gaussian curvatures are related by the relation