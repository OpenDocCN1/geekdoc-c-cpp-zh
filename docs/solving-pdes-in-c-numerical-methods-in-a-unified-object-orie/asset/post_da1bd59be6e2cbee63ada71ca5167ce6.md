
if(((*vertex[i])()[0]>0.)||((*vertex[i])()[1]>0.))
    return 1.;
return 1000.;
} // coefficient of y-derivative

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

## A.23 The Linear Elasticity Solver

Here, we show how to implement the adaptive-refinement algorithm in Chapter 20, Section 8, to solve the linear elasticity equations. First, we present the constructor that assembles the stiffness matrix described in Chapter 20, Section 7. The code is similar to the code in Chapter 16, Section 5, except that the three blocks A^(0,0), A^(1,1), and A^(0,1) in Chapter 20, Section 7, need to be constructed. Thus, the body of the inner loop in the code in Chapter 16, Section 5, is actually repeated here three times, using three different 2 × 2 matrices: "diffCoef" to construct A^(0,0), "diffCoef2" to construct A^(1,1), and "mixed" to construct A^(0,1).

In order to impose Dirichlet boundary conditions at points in Γ_D, we define a vector of integers named "DirichletBoundary". For each node i in Γ_D, the i-th component in "DirichletBoundary" vanishes. The rest of the components in "DirichletBoundary" have the value 1. Now, the matrix A is "masked" by the "DirichletBoundary" vector in the sense that the i-th row and i-th column are dropped for every i ∈ Γ_D and replaced with the standard unit vector e^(i), which has the value 1 at its i-th component and 0 at all the others. This results in a trivial equation for the unknown x_i in the stiffness system for every i ∈ Γ_D.

The constructor that assembles the stiffness matrix for the elasticity equations is thus as follows:

```
template<class T>
sparseMatrix<T>::sparseMatrix(mesh<triangle>&m) {
item = new row<T>*[number = 2 * m.indexing()];
for(int i=0; i<number; i++)
item[i] = 0;
point gradient[3];
gradient[0] = point(-1,-1);
gradient[1] = point(1,0);
gradient[2] = point(0,1);
dynamicVector<int> DirichletBoundary(number,1);
for(const mesh<triangle>* runner = &m; runner; runner = (const mesh<triangle>*)runner->readNext()){
point diffX(1.,0.);
point diffY(0.,(1.-NU)/2.);
point diffX2((1.-NU)/2.,0.);
point diffY2(0.,1.);
matrix2 diffCoef(diffX,diffY);
matrix2 diffCoef2(diffX2,diffY2);
point mixedX(0.,NU);
point mixedY((1.-NU)/2.,0.);
matrix2 mixed(mixedX,mixedY);
matrix2 S((*runner())[1]() - (*runner())[0](),
    (*runner())[2]() - (*runner())[0]());
matrix2 Sinverse = inverse(S);
matrix2 weight = abs(det(S)/2) * Sinverse * diffCoef * transpose(Sinverse);
matrix2 weight2 = abs(det(S)/2) * Sinverse * diffCoef2 * transpose(Sinverse);
matrix2 weightMixed = abs(det(S)/2) * Sinverse * mixed * transpose(Sinverse);
for(int i=0; i<3; i++) {
int I = (*runner())[i].getIndex();
if((abs(squaredNorm((*runner())[i]()))-1.)<1.e-7 &&
((*runner())[i][0] <= -0.5)){
DirichletBoundary[I] = 0;
DirichletBoundary[I+number/2] = 0;
}
for(int j=0; j<3; j++) {
int J = (*runner())[j].getIndex();
if(j>=i){
if(item[I]){
row<T> r(gradient[j]*weight*gradient[i],J);
*item[I] += r;
}
else
item[I] = new row<T>(gradient[j]*weight*gradient[i],J);
}
}
}
}
}
```

```
if(item[I+number/2]){
    row<T> r(gradient[j]*weight2*gradient[i],
        J+number/2);
    *item[I+number/2] += r;
}
else
    item[I+number/2] =
        new row<T>(gradient[j]*weight2*gradient[i],
            J+number/2);
}
if(item[I]){
    row<T> r(gradient[j]*weightMixed*gradient[i],
        J+number/2);
    *item[I] += r;
}
else
    item[I] = new
        row<T>(gradient[j]*weightMixed*gradient[i],
            J+number/2);
}
}
for(int i=0; i<number; i++){
    if(DirichletBoundary[i])
        item[i]->maskItems(DirichletBoundary, (double)0.);
    else
        *item[i] = row<T>(1.,i);
}
// assemble stiffness matrix for linear elasticity
```

As explained in Chapter 20, Section 7, after the matrix A has been constructed using the above constructor, it should be further modified by

```
A += transpose(A) - diagonal(A);
```

This completes the definition of the stiffness matrix.

Next, we implement the adaptive-refinement algorithm in Chapter 20, Section 8. For this purpose, the "if" question in the "refine" function in Chapter 14, Section 6, should be modified to read

```
if((item[i].getIndex() >= 0)&&
    (item[j].getIndex() >= 0)&&
    ((abs(v[item[i].getIndex()]) -
    v[item[j].getIndex()])>threshold)||
    (abs(v[item[i].getIndex()+v.dim()/2] -
    v[item[j].getIndex()+v.dim()/2])>threshold))){
    ...
```

This way, the criterion in Chapter 20, Section 8, is implemented.

Next, we implement the modified multigrid algorithm in Chapter 20, Section 9. The algorithm is in principle the same as in Chapter 17, Section 8, except that the block-diagonal part of A,

blockdiag(A^(0,0),A^(1,1)),

is used to construct the coarse grid and the prolongation matrix P and restriction matrix R. In order to obtain this block-diagonal matrix, we insert a few code lines at the beginning of the "createTransfer" function in Section A.18. These code lines delete the A^(0,1) and A^(1,0) blocks from the current copy of the stiffness matrix A. (Of course, it is assumed that the original matrix A is also stored elsewhere for safekeeping, so these changes don’t affect it.) The result is the required block-diagonal part of A, which is then used in the remainder of the "createTransfer" function to create the coarse grid and prolongation and restriction matrices.

The code lines that should be inserted at the beginning of the "createTransfer" function are as follows:

```
dynamicVector<int> one(rowNumber(),1);
dynamicVector<int> two(rowNumber(),1);
for(int i=0; i<rowNumber()/2; i++)
    two(i) = 0;
for(int i=rowNumber()/2; i<rowNumber(); i++)
    one(i) = 0;
for(int i=0; i<rowNumber()/2; i++)
    item[i]->maskItems(one, (double)0.);
for(int i=rowNumber()/2; i<rowNumber(); i++)
    item[i]->maskItems(two, (double)0.);
```

This completes the changes required in the linear elasticity solver. The loop that implements the adaptive-refinement algorithm is basically as in Section A.21.

## A.24 Fusion with the Alternative Right-Hand Side

Here we modify the original multigrid fusion algorithm to use the alternative right-hand side introduced in Chapter 23, Section 23.10. For this purpose, however, we must first define a new binary arithmetic operator that adds a sparse row to a dynamic vector:

```
template<class T>&
const dynamicVector<T>&
operator+=(dynamicVector<T>&v, const row<T>&r){
    for(const row<T>* runner = &r; runner;
        runner = (const row<T>*)runner->readNext())
        v(runner->getColumn()) += runner->getValue();
    return v;
} // adding a row to a dynamic vector
```

With this operator, the user can write "v += r" to add the well-defined row 'r' to the well-defined dynamic vector 'v'. Such a command is indeed used below.
