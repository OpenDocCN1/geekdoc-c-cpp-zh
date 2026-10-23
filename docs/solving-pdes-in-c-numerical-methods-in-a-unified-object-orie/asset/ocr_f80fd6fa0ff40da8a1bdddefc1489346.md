```
if(((*vertex[i])()[0]>0.)||((*vertex[i])()[1]>0.))
    return 1.;
return 1000.;
} // coefficient of y-derivative
```

These functions should be used in the calculation of the stiffness matrix according to the guidelines in Chapter 12, Section 5. Actually, the only change is that the 2 × 2 matrix "weight" in the constructor that assembles the stiffness matrix in Chapter 16, Section 5, should also contain the factor diag(P, Q) in the middle of it:

```
point diffX((*runner()).p(),0.);
point diffY(0.,(*runner()).q());
matrix2 diffCoef(diffX,diffY);
matrix2 S((*runner())[1]() - (*runner())[0](),
    (*runner())[2]() - (*runner())[0]());
matrix2 Sinverse = inverse(S);
matrix2 weight = abs(det(S)/2) *
    Sinverse * diffCoef * transpose(Sinverse);
```

We leave to the reader the details of incorporating the mixed boundary conditions and eliminating the equations corresponding to nodes on the Dirichlet boundary Γ_D (see Sections A.23 and A.33). This completes the definition of the stiffness matrix.

In order to refine not only in the interior of the domain but also at the circular part of its boundary, we also use automatic boundary refinement (Chapter 14, Section 7). For this purpose, we introduce an extra "if" question in the code in Chapter 14, Section 8, to make sure that automatic boundary refinement is used only at boundary edges that lie next to circular boundary segments.

The adaptive-refinement loop is as in Section A.21 above. This completes the definition of the diffusion solver.

# A.23 The Linear Elasticity Solver

Here, we show how to implement the adaptive-refinement algorithm in Chapter 20, Section 8, to solve the linear elasticity equations. First, we present the constructor that assembles the stiffness matrix described in Chapter 20, Section 7. The code is similar to the code in Chapter 16, Section 5, except that the three blocks A^(0,0), A^(1,1), and A^(0,1) in Chapter 20, Section 7, need to be constructed. Thus, the body of the inner loop in the code in Chapter 16, Section 5, is actually repeated here three times, using three different 2 × 2 matrices: "diffCoef" to construct A^(0,0), "diffCoef2" to construct A^(1,1), and "mixed" to construct A^(0,1).

In order to impose Dirichlet boundary conditions at points in Γ_D, we define a vector of integers named "DirichletBoundary". For each node i in Γ_D, the i-th component in "DirichletBoundary" vanishes. The rest of the components in "DirichletBoundary" have the value 1. Now, the matrix A is "masked" by the "DirichletBoundary" vector in the sense that the i-th row and i-th column are dropped for every i ∈ Γ_D and replaced with the standard unit vector e^(i), which has the value 1 at its i-th component and 0 at all the others. This results in a trivial equation for the unknown x_i in the stiffness system for every i ∈ Γ_D.

The constructor that assembles the stiffness matrix for the elasticity equations is thus as follows: