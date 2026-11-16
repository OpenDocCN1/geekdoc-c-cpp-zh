```
$$G_h^Q(u_h, \tilde{p}_h, \delta \tilde{q}_h) = \oint_{\Omega_h} \left[ \det(\mathbf{I} + \nabla_{h,k} \mathbf{u}_h) - 1 - \frac{\partial \tilde{W}^*}{\partial \tilde{p}}(\mathbf{x}, \mathbf{I} + \nabla_{h,k} \mathbf{u}_h, \tilde{p}_h) \right] \delta \tilde{q}_h \, d\mathbf{x}.$$ (12.15)
```

Notice that since we replace the gradient operators \(\nabla\) in both \(\mathbf{u}_h\) and \(\delta \mathbf{v}_h\) in (12.13), (12.14), and (12.15) with \(\nabla_{h,k}\), the resulting approximations yield symmetric linearizations. Moreover, both of the above finite element approximations pass the first-order patch test [100]. This means that when the exact displacement field is a linear field, the above finite element approximations give the exact results.

# 12.7 NUMERICAL EXAMPLES

In this section, we present a series of numerical tests to assess the performance of the displacement-based and the two-field mixed polygonal and polyhedral finite element methods. For 2D problems, both displacement-based and mixed polygonal elements up to the second order are considered, whereas only first-order displacement-based polyhedral elements are studied for the 3D case. We demonstrate, through the convergence studies of two boundary-value problems, that the gradient correction scheme is capable of ensuring optimal convergence of polygonal and polyhedral elements in finite elasticity. For mixed polygonal elements, we also provide numerical evaluations and discuss inf-sup stability for different choices of pressure approximations.

Throughout this section, a neo-Hookean material model is considered. For a compressible neo-Hookean material, the stored-energy function characterizing the material behavior has the form

```
$$W(\mathbf{F}) = \frac{\mu}{2}[\mathbf{F} : \mathbf{F} - 3] - \mu(\det \mathbf{F} - 1) + \frac{3\kappa + \mu}{6}(\det \mathbf{F} - 1)^2,$$
```

where \(\mu\) and \(\kappa\) denote the initial shear and bulk moduli of the material response. In the limit of incompressibility (\(\kappa \to \infty\)), the above compressible neo-Hookean material reduces to the standard neo-Hookean stored-energy function

```
$$W(\mathbf{x}, \mathbf{F}) = \begin{cases} \frac{\mu}{2}[\mathbf{F} : \mathbf{F} - 3], & \text{if } \det \mathbf{F} = 1, \\ +\infty, & \text{otherwise.} \end{cases}$$ (12.16)
```

The standard Newton-Raphson method is employed to solve the nonlinear system of equations, and we assume that convergence at each loading step is met if the norm of the residual falls below \(10^{-8}\) times that of the initial residual.

# 12.7.1 Displacement-based polygonal and polyhedral elements

This subsection presents a convergence study of the displacement-based polygonal and polyhedral finite elements using the gradient correction scheme. In particular, we consider a boundary-value problem as shown in Figure 12.6(a), where a rectangular block of dimensions \(1 \times 1 \times \pi\) is bent into a semi-circular shape. The corresponding analytical displacement solution \(\mathbf{u}\) is given by

```
$$u_x = -1 + (1+x)\cos(z) - x, \quad u_y = 0, \quad u_z = (1+x)\sin(z) - z,$$
```