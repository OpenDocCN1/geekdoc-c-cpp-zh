
neous, complex microstructures. The heterogeneity of the microstructures makes the underlying local deformations inherently complex.

Computational microscopic studies of nonlinear elastic materials, especially those with complex microstructures, help in gaining a quantitative understanding of the complex behavior of these materials. These studies are also essential in guiding the optimization of nonlinear elastic materials, so that they can enable new technological applications. It has long been recognized that standard finite elements, especially simplicial (triangular and tetrahedral) finite elements, are inadequate in simulating processes involving realistic, large deformations—an example is shown in Figure 12.1. By contrast, recent studies have demonstrated that polygonal elements possess significant potential in the study of nonlinear elastic materials under finite deformations. First, these elements are well-suited to model complex microstructures (e.g., particulate microstructures and microstructures involving different length scales) and to seamlessly incorporate periodic boundary conditions. Secondly, polygonal elements are found to be more tolerant to large localized deformations and to produce more accurate results in bending and shear than standard finite elements. With mixed formulations, lower-order mixed polygonal elements are also shown to be numerically stable on Voronoi-type meshes without the need for any additional stabilization terms. Likewise, numerical stability of the polygonal finite elements is also demonstrated in topology optimization [160, 389, 392] and in fluid mechanics [394] problems.

One major challenge in the polygonal finite method is accurate numerical integration of the weak-form integrals. The finite element space for polygonal elements contains non-polynomial (e.g., rational) functions, and therefore, the use of existing quadrature schemes, typically designed for integration of polynomial functions, leads to non-vanishing consistency errors [268, 388] and consequently, sub-optimal or even non-convergent finite element solutions under mesh refinement. In practice, using a sufficiently large number of integration points can lower the consistency error for linear polygonal elements in two dimensions. A triangulation scheme with three integration points per triangle is shown to be sufficiently accurate for practical problems and mesh sizes [99, 388]. However, for higher-order polygonal elements, the number of integration points for such a scheme can become prohibitively large [100]. This is also the case for polyhedral elements in three dimensions [268, 393]. In practical applications, as the number of elements increases, the associated computational cost for a polygonal discretization can become exorbitant.

Several attempts have been made in the literature to address the issue of numerical quadrature. For example, in the context of scalar diffusion problems, inspired by the virtual element method (VEM) [33, 72, 161], Talischi et al. [388] have proposed a polynomial projection approach to ensure the polynomial consistency of the bilinear form, and thereby ensure the satisfaction of the patch test and optimal convergence for both linear and quadratic polygonal elements. A similar approach was also adopted by Manzini et al. [268] to solve Poisson problems on polygonal meshes. However, these approaches require the existence of a bilinear form, and therefore, extension to general nonlinear problems is non-trivial and is still an open question. Borrowing the idea of pseudo-derivatives in the meshfree literature [229], Bishop has proposed an approach to correct the derivatives of the shape functions to enforce the linear consistency property on general polygonal and polyhedral meshes [46, 47]. With this correction, the linear patch test is passed and optimal convergence is achieved. Although applicable for general nonlinear scenarios, the extension to higher-order cases (for example, quadratic polygonal finite elements) is not straightforward. More recently, Talischi et al. [393] proposed a general gradient correction scheme that is applicable to both linear and nonlinear problems on arbitrary-order polygonal and polyhedral elements. By requiring a minimum order of accuracy in the numerical quadrature, the correction scheme is shown to restore optimal convergence for both linear and nonlinear problems [393]. In this chapter, we apply the gradient correction scheme to polygonal and polyhedral finite elements for finite elasticity problems and demonstrate that the gradient correction scheme can effectively and efficiently render optimally convergent polygonal and polyhedral finite element methods.

![](img/4913dd83a2a14bc205a0a92cce102c82_236_0.png)

Figure 12.1. An illustration of the limited capability of standard tetrahedral elements to undergo large deformation. Experimentally, a synthetic rubber filled with 20% volume fraction of randomly distributed silica particles can be stretched more than four times its original length (\(\lambda = 4\)) without internal damage under uniaxial tension [315]. By contrast, a finite element model, based on standard 10-node hybrid elements with linear pressure, is only able to deform to a macroscopic stretch of \(\lambda = 1.5\) [174]. See color insert.

## 12.2 FINITE ELASTICITY FORMULATIONS

This section briefly recalls the equations of elastostatics applied to hyperelastic materials. Two variational formulations are presented: (i) the standard displacement-based formulation [63, 294, 429], and (ii) a general mixed formulation involving the displacement field and a pressure-like scalar field as trial fields. Throughout this chapter, we adopt a Lagrangian description of the fields.

Consider a body in its stress-free, undeformed configuration that occupies an open domain \(\Omega \subset \mathbb{R}^d\) with boundary \(\partial \Omega\). On its boundary, it is subjected to a prescribed displacement field \(u^0\) on \(\Gamma^u\) and traction \(t\) (per unit undeformed surface) on \(\Gamma^t\), such that \(\Gamma^u \cup \Gamma^t = \partial \Omega\) and \(\Gamma^u \cap \Gamma^t = \varnothing\). The body is also assumed to be subjected to a body-force \(f\) (per unit undeformed volume) in \(\Omega\). A stored-energy function \(W\) is used to characterize the constitutive behavior of the body, which is assumed to be an objective function of the deformation gradient \(F\). In terms of \(W\), the first Piola-Kirchhoff stress tensor \(P\) at each material point \(x \in \Omega\) is thus given by the following relation:

\(P(x) = \frac{\partial W}{\partial F}(x, F),\)

which is used as the stress measure of choice in this chapter.

### 12.2.1 Displacement-based formulation

The well-known principle of minimum potential energy asserts that the equilibrium displacement field \(u\) minimizes the potential energy \(\Pi\) among all displacement fields that are kinematically admissible:

\(\Pi(u) = \min_{v \in \mathcal{K}} \Pi(v),\quad (12.1)\)

with

\(\Pi(v) = \int_{\Omega} W(x, F(v)) \, dx - \int_{\Omega} f \cdot v \, dx - \int_{\Gamma^t} t \cdot v \, ds.\quad (12.2)\)

In the above expression, \(\mathcal{K}\) stands for a sufficiently large set of displacements such that \(v = v^0\) on \(\Gamma^e\).

The weak form of the Euler-Lagrange equations associated with the variational problem (12.1) reads as follows:

\(G(v, \delta v) = \int_{\Omega} \frac{\partial W}{\partial F}(x, F(v)) : \nabla(\delta v) \, dx - \int_{\Omega} f \cdot \delta v \, dx\)
\(- \int_{\Gamma^t} t \cdot \delta v \, ds = 0 \quad \forall \delta v \in \mathcal{K}^0,\) (12.3)

where the test displacement field \(\delta v\) is the variation of \(v\), and \(\mathcal{K}^0\) denotes the set of all the kinematically admissible displacement fields that vanish on \(\Gamma^e\).

### 12.2.2 A general two-field mixed variational formulation

For nonlinear elastic materials that are nearly incompressible, the variational principle in (12.1)-(12.2) is known to perform poorly when approximated by standard finite element methods [204]. As a standard remedy, mixed variational principles that involve not only the deformation, but also a pressure field are utilized [17, 75, 87, 90, 99, 188, 362, 385]. Based on the multiplicative splitting of
