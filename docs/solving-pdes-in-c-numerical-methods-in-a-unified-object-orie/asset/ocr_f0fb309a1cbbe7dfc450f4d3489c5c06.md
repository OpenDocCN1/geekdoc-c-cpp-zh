In fact, if the left-hand side of this equation is denoted by a((u,v),(s,t)) and the right-hand side is denoted by f((s,t)), then the equation takes the form

a((u,v),(s,t)) = f((s,t)).

This formulation is used below to define an equivalent, well-posed minimization problem.

# 20.4 The Minimization Problem

This section and the next one are related to the theory in Chapter 11. Readers who are mainly interested in the practical aspects can skip them and proceed to Section 20.6. More advanced readers may find them interesting and relevant to understand better the finite-element scheme.

Let’s define the minimization problem that is equivalent to the weak formulation. Define the functional

g((s,t)) ≡ 1/2 a((s,t),(s,t)) − f((s,t)).

The minimization problem is defined as follows: from the family of pairs of functions that agree with γ₁ and γ₂ on Γ_D and have square-integrable derivatives in Ω, pick the pair (u,v) that minimizes g.

By following the proof in Chapter 11, Section 3, one can show that here also the minimization problem is equivalent to the weak formulation. Therefore, in order to show that the weak formulation is well posed, it is sufficient to show that the minimization problem is well posed (has a unique solution). As shown in Chapter 11, Sections 5 and 6, a sufficient condition for this is the coercivity of the quadratic form a((s,t),(s,t)). This property is shown below.

# 20.5 Coercivity of the Quadratic Form

In order to show the coercivity of the quadratic form a((s,t),(s,t)), we assume that the domain Ω is connected and Γ_D is (or contains) a curve in ∂Ω. Let s and t be some functions that vanish on Γ_D and have square-integrable derivatives in Ω. Assume also that

a((s,t),(s,t)) = 0.