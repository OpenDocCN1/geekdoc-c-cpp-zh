
in P by the standard unit row $e^{(i)}$, of which all components vanish except the $i$th one, which is equal to 1.

5. For every $i$ and $j$ that are both in $f$ and satisfy $i \neq j$ and $P_{i,j} \neq 0$, define

$$ W_{i,j} \equiv \sum_{k \in c, P_{i,k} \neq 0} B_{j,k}. $$

6. For every $i$ and $j$ that are both in $f$ and satisfy $i \neq j$ and $P_{i,j} \neq 0$, add a fraction of $P_{i,j}$ to every nonzero element $P_{i,k}$ that lies in the same row and in column $k \in c$ as follows:

$$ P_{i,k} \leftarrow P_{i,k} + \left( \frac{B_{j,k}}{W_{i,j}} \right) P_{i,j}. $$

7. For every $j \in f$, drop the corresponding column from $P$. (In this step, $P$ becomes rectangular.)

8. For every $i \in f$, divide the $i$th row in $P$ by its row-sum. (After this step, the row-sums in $P$ are all equal to 1.)

This completes the definition of the prolongation matrix $P$. The rest of the details of the definition are as in Section 17.8: that is, $R = P^T$ and $Q = R A P$. The coarse-grid equation $Q \mathbf{e} = \mathbf{r}$ is solved approximately by one AMG iteration, called recursively.

Because AMG has no theoretical background, it is not clear whether it works for special diagonally dominant examples such as the one in Figure 12.8 above. Still, the present numerical examples show practically no difference between the multigrid versions.

## 17.10 Implementation of Multigrid

As we’ve seen in Section 17.8, the multigrid iteration relies strongly on recursion. The coarse-grid system of the form $Q \mathbf{e} = \mathbf{r}$ is solved approximately by one multigrid iteration (V-cycle), which is applied to it recursively. This recursive call requires an even coarser grid, and the recursive process continues until the coarsest grid is reached, where a small system is solved (see Figure 17.1). Naturally, these matrices should thus be stored in a recursively defined object.

The "multigrid" class is indeed defined recursively. It contains not only the "sparseMatrix" objects required to store the fine-grid coefficient matrix and transfer operators to and from the coarse grid, but also a pointer-to-multigrid field that contains the address of the next (coarser) "multigrid" object.

This recursive structure is useful not only in the multigrid V-cycle but also in basic member functions of the "multigrid" class, such as constructors and assignment operators.

The structure of the "multigrid" object is displayed schematically in Figure 17.2. The "multigrid" object contains five "sparseMatrix" objects: 'A', 'U', 'L', 'P', and 'R'. The function "createTransfer" constructs the rectangular matrices 'P' and 'R', which transfer information between the fine and coarse grids. (The complete definition of this function is deferred to Section A.18 in the Appendix.) More precisely, 'R' transforms fine-grid vectors

![Figure 17.2](img/1f293b0ceb2de964310ea7f941a1b580_467_0.png)

**Figure 17.2.** The "multigrid" object contains the square matrices A, U, and L and the rectangular matrices R and P, which are used to transfer information to and from the coarse grid.

into coarse-grid vectors, and 'P' transforms coarse-grid vectors into fine-grid vectors. The information about the coarse grid, which is the next "multigrid" object in the multigrid hierarchy, is pointed at by the pointer-to-multigrid "next". This recursive pattern is used later in the implementation of the V-cycle.

The following code uses some predetermined parameters. "useILU" is an integer parameter that determines whether ILU or Gauss-Seidel is used as the relaxation method within the V-cycle. (In most of the present applications, "useILU" is zero.) In the Gauss-Seidel relaxation, the standard order of unknowns is used in the prerelaxation, and the reversed order is used in the post-relaxation. (This guarantees that the multigrid preconditioner is indeed symmetric for symmetric coefficient matrices.)

The parameter "gridRatio" determines whether the next-grid matrix is sufficiently small and deserves to be constructed or the grid hierarchy should terminate. In most of the present applications, "gridRatio" is 0.95. We also use a negative "gridRatio" when we want to use a trivial grid hierarchy that contains only the original grid. This is done when we want to run the standard symmetric Gauss-Seidel or ILU iteration, to compare its convergence rate to that of the multigrid iteration.

Here is the block of the "multigrid" class:

```cpp
const double gridRatio=0.95;
template<class T> class multigrid{
    sparseMatrix<T> A;
    sparseMatrix<T> U;
    sparseMatrix<T> L;
    sparseMatrix<T> P;
    sparseMatrix<T> R;
    multigrid* next;
public:
    multigrid():next(0){
    } // default constructor
```

The copy constructor copies the sparse matrices in the "multigrid" argument and then calls itself recursively to copy the coarse-grid matrices:

```cpp
multigrid(const multigrid&mg)
    : A(mg.A),U(mg.U),L(mg.L),P(mg.P),R(mg.R),
      next(mg.next ? new multigrid(*mg.next) : 0){
} // copy constructor
```

The most important function in the "multigrid" class is the constructor that uses a "sparseMatrix" argument to construct all the required sparse matrices in the entire grid hierarchy. This is done most elegantly in the initialization list as follows. Recall that the fields in the object are not necessarily constructed in their order in the initialization list but rather in the order in which they are declared in the class block. Here, the fields in the "multigrid" class are 'A', 'U', 'L', 'P', 'R', and "next" (in that order). First, 'A' is initialized to be the same as the matrix that is passed as an argument. Now, 'U' is initialized to be the same as 'A' and then changes and takes its final form when 'L' is initialized using the "factorize" function of Section 17.7, which modifies 'U' and returns 'L'. Similarly, 'P' is initialized to be the same as 'A' and then changes and takes its final form when 'R' is constructed using the "createTransfer" function, which modifies 'P' and returns 'R'. Finally, the "next" field is filled with the address of a new "multigrid" object, which is created using a recursive call to the same constructor itself, with the low-order matrix Q ('R' times 'A' times 'P') as argument. A necessary condition, however, to construct this new "multigrid" object is that it indeed contains much smaller matrices. In fact, the order of the matrices in it must be smaller than "gridRatio" times the order of 'A'. Otherwise, the hierarchy of the grids terminates, and "next" takes the zero value:

```cpp
multigrid(const sparseMatrix<T>&m)
    : A(m), U(useILU ? A : 0),
      L(useILU ? U.factorize(0.05) : 0),P(A),
      R(P.createTransfer()),
      next(R.rowNumber()<=gridRatio*A.rowNumber() ?
      new multigrid(R*A*P) : 0){
} // constructor with matrix argument
```

The assignment operator is only declared here, and will be defined later on. Here is the definition of the destructor:

```cpp
const multigrid<T>& operator=(const multigrid<T>&);
~multigrid(){
    delete next;
    next = 0;
}    // destructor
```

The "Vcycle" and "print" functions are only declared here and defined later.

```cpp
const dynamicVector<T>&
    Vcycle(const dynamicVector<T>&, dynamicVector<T>&);
friend void print<T>(const multigrid<T>&);
};
```

This completes the block of the "multigrid" class.
The V-cycle uses some more predetermined integer parameters:

1. "Nu1" is the number of prerelaxations that are used before the coarse-grid correction. ("Nu1" == 1 is used here.)
2. "Nu2" is the number of post-relaxations that are used after the coarse-grid correction. ("Nu2" == 1 is used here.)
3. "cycleIndex" is the number of coarse-grid corrections. ("cycleIndex" == 1 is used here.)
4. "NuCoarse" is the number of relaxations in the coarsest grid. ("NuCoarse" == 1 is used here.)

Here is the actual implementation of the multigrid V-cycle:

```cpp
const int Nu1=1,Nu2=1,cycleIndex=1,NuCoarse=1,useILU=0;
template<class T>
const dynamicVector<T>&
multigrid<T>::Vcycle(
        const dynamicVector<T>&f, dynamicVector<T>&x){
    if(next){
        for(int i=0; i<Nu1; i++){
            if(useILU)
                ILU(A,L,U,f,x);
            else
                GaussSeidel(A,f,x);
        }
```

So far, we have completed the first "Nu1" relaxations, whatever relaxation method is used.
We are now ready to do the coarse-grid correction:

```cpp
dynamicVector<T> residual = f - A * x;
dynamicVector<T> correction(R.rowNumber(), 0.);
for(int i=0; i<cycleIndex; i++)
    next->Vcycle(R * residual, correction);
x += P * correction;
```
