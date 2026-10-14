where $u \in H^1(\Omega)$ is the electric potential and $q$ is known.

In an EIT experiment, an electrical current (Neumann data) $f$ on $\partial\Omega$ is applied and then the resulting electrical potential (Dirichlet data) $g$ on $\partial\Omega$ is measured. The data collected then provides information and is used to approximate $q$ from a set of EIT experiments using different input currents [3, 4, 5]. EIT can be applied to detecting ground water intrusions in geophysical applications [6], monitoring of oil and gas mixtures in oil pipelines [7], and noninvasive medical imaging [8, 9].

# 5.2.1 Analytical Setting for the EIT Model

We define the following Neumann and Dirichlet boundary value problems

$-\operatorname{div}\,(q\nabla u)=0 \quad \text{in }\Omega,$

$q\frac{\partial u}{\partial n}=f \quad \text{on }\partial\Omega,$

(5.2)

and

$-\operatorname{div}\,(q\nabla u)=0 \quad \text{in }\Omega,$

$u=g \quad \text{on }\partial\Omega.$

(5.3)

Let the conductivity $q \in Q$, an appropriate metric space. $q$ is assumed to be bounded below and above, i.e. $0 < c_1 \le q \le c_2 < \infty$. In addition, denote by $\Gamma_D u$ the Dirichlet trace operator, i.e. the restriction of $u$ to the boundary

$\Gamma_D : X \to Z$

$u \mapsto \Gamma_D u.$

As usual in EIT, we restore uniqueness of the solution $u$ of the Neumann problem (2) by requiring that the Dirichlet trace $\Gamma_D u$ satisfies

$\int_{\partial\Omega} \Gamma_D u(s) ds = 0.$

(5.4)

Note that to ensure the solvability of the Neumann problem in Equation (5.2) the current $f$ must satisfy the integrability condition, which, in the absence of a source term, reads $\int_{\partial\Omega} f(s) ds = 0$. The associated linear forward operator of the Neumann problem, which maps an input current $f$ to the solution $u$, is denoted by

$F_N^q : W \to X$

(5.5)

$f \mapsto u \text{ solves (2)}.$

(5.6)

The linear operator $F_D^q$ for the Dirichlet problem in Equation (5.3) can be defined analogously. The NtD map can be written as $\Gamma_D F_N^q$. The weak formulation of the Neumann problem in Equation (5.2) becomes