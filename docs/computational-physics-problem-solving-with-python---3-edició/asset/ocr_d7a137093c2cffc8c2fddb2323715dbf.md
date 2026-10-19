# 19.2

# Electrostatic Potentials

Your *problem* is to find the electric potential for all points *inside* the charge-free square shown in Figure 19.1. The bottom and sides of the region are made up of wires that are “grounded” (kept at 0 V). The top wire is connected to a voltage source that keeps it at a constant 100 V.

# 19.2.1

# Laplace's Elliptic PDE (Theory)

We consider the entire square in Figure 19.1 as our boundary with the voltages prescribed upon it. If we imagine infinitesimal insulators placed at the top corners of the box, then we will have a closed boundary. Because the values of the potential are given on all sides, we have Neumann conditions on the boundary and, according to Table 19.2, a unique and stable solution.

# Table 19.2 The relation between boundary conditions and uniqueness for PDEs.

| Boundary Condition | Elliptic (Poisson equation) | Hyperbolic (Wave equation) | Parabolic (Heat equation) |
|---|---|---|---|
| Dirichlet open surface | Underspecified | Underspecified | *Unique and stable (1D)* |
| Dirichlet closed surface | *Unique and stable* | Overspecified | Overspecified |
| Neumann open surface | Underspecified | Underspecified | *Unique and stable (1D)* |
| Neumann closed surface | *Unique and stable* | Overspecified | Overspecified |
| Cauchy open surface | Nonphysical | *Unique and stable* | Overspecified |
| Cauchy closed surface | Overspecified | Overspecified | Overspecified |

![](bbox=[0.13, 0.66, 0.62, 0.78])

Figure 19.1 (a) The shaded region of space within a square in which we determine the electric potential by solving Laplace’s equation. There is a wire at the top kept at a constant 100 V and a grounded wire (dashed) at the sides and bottom. (b) The computed electric potential as a function of x and y. The projections onto the shaded xy plane are equipotential (contour) lines.