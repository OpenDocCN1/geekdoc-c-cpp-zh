In the beginning of the loop, the right-hand-side vector $f$ is defined. The dimension of this vector (the number of nodes in the mesh) is returned by the “indexing()” function, which also assigns indices to the nodes in a continuous order:

```
dynamicVector<double> f(m.indexing(),0.);
f(0) = 1.;
```

These indices are then used to refer to nodes when the stiffness matrix $A$ is assembled:

```
sparseMatrix<double> A(m);
A += transpose(A) - diagonal(A);
```

The PCG iteration is now used to solve the stiffness system:

```
dynamicVector<double> x(A.order(),0.);
multigrid<double> MG(A);
PCG(MG,A,f,x);
printf("value at (1,0)=%f\n",x[0]);
printf("at level %d number of nodes=%d\n",i,x.dim());
if(i<9)m.refine(x, 0.01);
}
```

The final command in the loop refines the mesh using the numerical solution $x$. This completes the adaptive-refinement code.

# A.22  The Diffusion Solver

Here, we show how to implement the adaptive-refinement algorithm to solve the diffusion problem in Chapter 19. First, we construct the initial coarse mesh in Figure 19.2. For this purpose, we need some constant parameters.

Note that the part of the boundary where Dirichlet boundary conditions are imposed in Figure 19.1 has a small slit in it. For simplicity, we assume here that the slit is four times as narrow as the entire rectangle that contains it (on which homogeneous Neumann boundary conditions are imposed). The code below uses two positive parameters, “SlitWidth” and “SlitLength”, so that the slit of size “SlitWidth”/4 by “SlitLength”.

The coarse mesh contains 9 triangles and 11 nodes (Figure A.4). In the code below, the nodes are defined and then used to define the triangles as well. Note that once a triangle is defined, the nodes used as vertices in it are no longer referred to by their original names but rather as vertices in this triangle. In this way, their “sharingElements” fields increase properly each time they are used as vertices in a new triangle. In fact, the original “node” objects are deleted once they have been placed in the required triangles:

```
const double SlitWidth=.2;
const double SlitLength=.5;
double angle = asin(SlitWidth);
double sinAngle=sin(angle);
double sinAngle2=sin(angle/2);
double cosAngle=cos(angle);
```