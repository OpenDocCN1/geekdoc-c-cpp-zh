To search for relative periodic solutions, we use a variant of the overdetermined shooting method developed by the author and collaborators in previous work to study several related problems: time-periodic solutions of the Benjamin-Ono equation [3,5] and the vortex sheet with surface tension [4,6]; Hopf bifurcation and stability transitions in mode-locked lasers [50]; cyclic steady-states in rolling treaded tires [21]; self-similarity (or lack thereof) at the crests of large-amplitude standing water waves [47]; harmonic resonance and spontaneous nucleation of new branches of standing water waves at critical depths [49]; and three-dimensional standing water waves [42]. The three approaches developed in these papers are the adjoint continuation method [5,50], a Newton-Krylov shooting method [21], and a trust region shooting method [49] based on the Levenberg-Marquardt algorithm [39]. We adopt the latter method here to exploit an opportunity to consolidate the work in computing the Dirichlet-Neumann operator for many columns of the Jacobian simultaneously, in parallel.

One computational novelty of this work is that we search directly for large-amplitude solutions of a nonlinear two-point boundary value problem, without using numerical continuation to get there. This is generally difficult. However, in the present case, numerical continuation is also difficult due to non-smooth bifurcation "curves" riddled with Cantor-like gaps [41], and the long simulation times that occur between collisions in the unidirectional case. Our shooting method has proven robust enough to succeed in finding time-periodic solutions, when they exist, with a poor starting guess. False positives are avoided by resolving the solutions spectrally to machine accuracy and overconstraining the minimization problem. Much of the challenge is in determining the form of the initial condition and the objective function to avoid wandering off in the wrong direction and falling into a nonzero local minimum before locking onto a nearby relative-periodic solution.

# 2. Equations of motion

The equations of motion of a free surface η(x,t) evolving over an ideal fluid with velocity potential φ(x,y,t) may be written [17,18,27,46]

(2.1)
η_t = φ_y - η_x φ_x,
φ_t = P[ φ_y η_t - ½ φ_x² - ½ φ_y² - g η ] ,

where subscripts denote partial derivatives, φ(x,t) = φ(x, η(x,t), t) is the restriction of φ to the free surface, g = 1 is the acceleration of gravity, ρ = 1 is the fluid density, and P is the projection

(2.2)
P f = f - 1/(2π) ∫₀^{2π} f(x) dx,

where we assume a 2π-periodic domain. The velocity components u = φ_x and v = φ_y at the free surface can be computed from φ via

(2.3)
( φ_x )   = 1/(1+η'(x)²) ( 1   -η'(x) ) ( φ'(x) )
( φ_y )                     ( η'(x)  1   ) ( G φ(x) )

where a prime denotes a derivative and G is the Dirichlet-Neumann operator [16]

(2.4)
G φ(x) = √(1+η'(x)²) ∂φ/∂n (x + i η(x)) = φ_y - η_x φ_x