rule for rotations. In fact, if we could pluck a small element of the fluid into space (so it would not feel the internal strain of the fluid), we would find that it is rotating like a solid with angular velocity ω ∝ w (Lamb, 1993). That being the case, it is useful to think of the vorticity as giving the local value of the fluid’s angular velocity vector. If w = 0, we have irrotational flow.

The field lines of w are continuous and move as if they are attached to the particles of the fluid. A uniformly flowing fluid has vanishing curl, while a nonzero vorticity indicates that the current curls back on itself or rotates. From the definition of the stream function (25.24), we see that the vorticity w is related to it by

w = ∇ × v = ∇ × (∇ × u) = ∇(∇ ⋅ u) − ∇²u ,    (25.28)

where we have used a vector identity for ∇ × (∇ × u). Yet the divergence ∇ ⋅ u = 0 because u has a component only in the z-direction and that component is independent of z (or because there is no source for u). We have now obtained the basic relation between the stream function u and the vorticity w:

∇²u = −w .    (25.29)

Equation 25.29 is analogous to Poisson’s equation of electrostatics, ∇²φ = −4πρ, only now each component of vorticity w is a source for the corresponding component of the stream function u. If the flow is irrotational, that is, if w = 0, then we need only to solve Laplace’s equation for each component of u. Rotational flow, with its coupled nonlinearities equations, leads to more interesting behavior.

As is to be expected from the definition of w, the vorticity form of the Navier–Stokes equation is obtained by taking the curl of the velocity form, that is, by operating on both sides with ∇×. After significant manipulations one obtains

ν∇²w = [(∇ × u) ⋅ ∇]w .    (25.30)

This and (25.29) are the two simultaneous PDEs that we need to solve. In 2D, with u and w having only z components, they are

∂²u/∂x² + ∂²u/∂y² = −w ,    (25.31)

ν(∂²w/∂x² + ∂²w/∂y²) = (∂u/∂y)(∂w/∂x) − (∂u/∂x)(∂w/∂y) .    (25.32)

So after all that work, we end up with two simultaneous, nonlinear, elliptic PDEs that look like a mixture of Poisson’s equation with the wave equation. The equation for u is Poisson’s equation with source w, and must be solved simultaneously with the second. It is this second equation that contains mixed products of the derivatives of u and w and thus introduces the nonlinearity.