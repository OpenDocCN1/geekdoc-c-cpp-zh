
"rowSumCoarse" and "addCoarse" are member functions of the "row" class. "rowSumCoarse" sums only those elements in the "row" argument that lie in columns $j \in c$ for which the corresponding element in the current "row" object is also nonzero:

```
const T rowSumCoarse(const row<T>&r,
    const dynamicVector<int>&coarse) const{
    T contribution =
        coarse[getColumn()] ? r[getColumn()] : 0.;
    return next ? contribution +
        ((row<T>*)next)->rowSumCoarse(r,coarse)
        : contribution;
} // row sum at coarse points
```

"addCoarse" adds values to nonzero elements in the current "row" object that lie in columns $j$ for which $j \in c$:

```
void addCoarse(const row<T>&r,
    const dynamicVector<int>&coarse){
    if(coarse[getColumn()])
        item += r[getColumn()];
    if(next) ((row<T>*)next)->addCoarse(r,coarse);
} // add values at coarse points
```

Note that the vector of integers "coarse" that indicates the coarse grid is passed to the above functions by reference rather than by name to avoid highly expensive and unnecessary reconstructions, particularly in the inner recursive calls.

Next, we implement the assignment operator of the "multigrid" class in Chapter 17, Section 10. This operator uses the recursive nature of the "multigrid" class: it first assigns the matrices corresponding to the finest grid and is then applied recursively to the coarser grids in the "next" field:

```
template<class T>
const multigrid<T>&
multigrid<T>::operator=(const multigrid<T>&mg){
    if(this != &mg){
        A = mg.A;
        U = mg.U;
        L = mg.L;
        P = mg.P;
        R = mg.R;
        if(next){
            if(mg.next)
                *next = *mg.next;
            else{
                delete next;
                next = 0;
            }
        }
        else
            if (mg.next) next = new multigrid(*mg.next);
    }
    return *this;
} // assignment operator
```

Similarly, the "print" friend function first prints the matrices in the "multigrid" object and then is applied recursively to the coarser grids in the "next" field:

```
template<class T>
void print(const multigrid<T>&mg) {
    print(mg.A);
    print(mg.P);
    print(mg.R);
    if (mg.next) print(*mg.next);
} // print the multigrid object
```

## A.19 Acceleration Techniques

Here, we implement several Krylov-subspace methods to accelerate the convergence of the basic multigrid iteration or any other iteration. The preconditioned conjugate gradient (PCG) acceleration method is limited to symmetric and positive definite (SPD) problems and SPD preconditioners. Therefore, we also implement the conjugate gradient squared (CGS), transpose-free quasi-minimal residual (TFQMR), and general minimal residual (GMRES) acceleration methods, which can be used in more general cases as well.

The PCG algorithm in Chapter 17, Section 11, works well for linear systems with SPD coefficient matrix $A$ and iterative methods with SPD preconditioner $P$. Here, we assume that the preconditioner is that of the multigrid iteration in Chapter 17, Section 8. (The ILU and symmetric Gauss–Seidel iterations can also be obtained from it by setting "gridRatio" = -1 in the implementation in Chapter 17, Section 10, which means that no coarse grids are actually used.) For this iterative method, the preconditioner is SPD whenever $A$ is (see Chapter 12, Section 7, of [68]), so PCG is indeed applicable.

Here is the detailed implementation of the PCG iteration. It terminates when the initial error has been reduced (in terms of the energy norm) by six orders of magnitude:

```
template<class T>
void
PCG(const multigrid<T>& MG, const sparseMatrix<T>&A,
    const dynamicVector<T>&f, dynamicVector<T>&x) {
    const double eps=1.e-15, threshold=1.e-12;
    const int iterationnumber = 1000;
    dynamicVector<T> zero(x.dim(),0.);
    dynamicVector<T> keep(x);
    dynamicVector<T> rr(MG.Vcycle(f,keep) - x);
    dynamicVector<T> r = f - A * x;
    dynamicVector<T> pp(rr);
    dynamicVector<T> p = r;
    double gamma = r * rr;
    double gammainit = gamma;
    int count = 0;
    while((abs(gamma/gammainit) >= 
        threshold * threshold &&
        (count <= iterationnumber))){
        keep = pp;
        dynamicVector<T> ww = pp - MG.Vcycle(zero,keep);
        dynamicVector<T> w = A * pp;
        double alpha = gamma / (pp * w);
        x += alpha * pp;
        rr -= alpha * ww;
        r -= alpha * w;
        double gammaold = gamma;
        gamma = r * rr;
        double beta = gamma/gammaold;
        pp = rr + beta * pp;
        count++;
        printf("at MG it. %d in PCG, (r,Pr)=%f\n",count,gamma);
    }
} // PCG acceleration
```

The "PCG()" function is called as follows:

```
PCG(MG,A,f,x);
print(x);
```

Next, we implement the CGS algorithm in [74] for the preconditioned system

$P^{-1}Ax = P^{-1}f$

where $P$ is the preconditioner of the multigrid iteration in Chapter 17, Section 8. In this system, the application of the coefficient matrix $P^{-1} A$ to a vector is done as in Chapter 17, Section 11.

If one wants to apply CGS to the ILU or symmetric Gauss–Seidel iteration, then one should just use a multigrid object with zero "next" field.

The initial direction vector is the initial preconditioned residual. The code also uses the "fabs" and "sqrt" functions available in the included "math.h" library. The "fabs()" function (absolute value) is actually equivalent to the "abs()" function in Chapter 1, Section 9. The "sqrt()" function returns the square root of a real number.

One of the arguments in the "CGS()" function is the integer "TFQMR". If this argument is zero, then CGS is indeed used. Otherwise, TFQMR [34] is used instead:

```
#include<stdio.h>
#include<math.h>
template<class T>
void CGS(const multigrid<T>& MG,
    const sparseMatrix<T>&A, int TFQMR,
    const dynamicVector<T>&f, dynamicVector<T>&x) {
    // ... [Continuation of CGS/TFQMR implementation across pages] ...
    T scala=vv*vv+eta/alpha;
    d = keep + scala * d;
    vv=omega/tau;
    T c=1./sqrt(1.+vv*vv);
    tau *= vv*c;
    eta=c*c*alpha;
    x += eta * d;
    printf("res=%f,it.=%d\n", sqrt((A*x-f)*(A*x-f)),2 * count+1);
}
omega0=omega1;
if (fabs(rho1=rbar*rcgs)<eps)
    printf("rho1=%f,mg it.=%d\n", fabs(rho1),2*count+1);
beta=rho1/rho0;
rho0=rho1;
u = rcgs + beta * q;
pp = u + beta * (q + beta * pp);
} while((fabs(omega1/omegainit) >= thresholdCG)&&
    (++count <= iterationnumber));
printf("total MG it. in CGS=%d\n",2 * count + 1);
} // CGS or TFQMR acceleration
```

Finally, we also implement the GMRES acceleration method [62]. Here, we use two extra integer arguments. The argument "preIterations" denotes the number of multigrid iterations used before GMRES starts (as in [70]). The argument 'K' denotes the dimension of the Krylov subspace used in GMRES:

```
template<class T>
const dynamicVector<T>&
GMRES(const multigrid<T>&MG, const sparseMatrix<T>&A,
      int preIterations, int K,
      const dynamicVector<T>&f, dynamicVector<T>&x){
for(int i=0;i<preIterations;i++)
    MG.Vcycle(f,x);
dynamicVector<T> s = x;
dynamicVector<T> r = x;
T R[K+1][K+1];
for(int i=0;i<=K;i++)
    for(int j=0;j<=K;j++)
        R[i][j]=0.0;
T Givens[2][K];
T xi[K];
for(int i=0;i<K;i++){
    Givens[0][i] = 0.0;
    Givens[1][i] = 0.0;
    xi[i] = 0.0;
}
dynamicVector<T>* Q[K+1];
dynamicVector<T> zero(x.dim(),0.0);
dynamicVector<T> keep(x);
double res=sqrt((A*x-f)*(A*x-f));
for(int k=0;k<=K;k++){ 
    if(k)keep = *Q[k-1];
    Q[k] = k ?
        new dynamicVector<T>(*Q[k-1]-MG.Vcycle(zero,keep))
        : new dynamicVector<T>(MG.Vcycle(f,keep)-x);
    for(int j=0;j<k;j++)
        *Q[k] -= (R[j][k] = *Q[j] * *Q[k]) * *Q[j];
    *Q[k] *= 1.0/(R[k][k] = sqrt(*Q[k] * *Q[k]));
    T givensa;
    T givensb;
    if(k){
        for(int j=1;j<k;j++){
            givensa=R[j-1][k];
            givensb=R[j][k];
            R[j-1][k] =
                givensa*Givens[0][j-1]+givensb*Givens[1][j-1];
            R[j][k] =
                -givensa*Givens[1][j-1]+givensb*Givens[0][j-1];
        }
        T ab=sqrt(R[k-1][k]*R[k-1][k]+R[k][k]*R[k][k]);
        Givens[0][k-1]=R[k-1][k]/ab;
        Givens[1][k-1]=R[k][k]/ab;
        givensa=R[k-1][k];
        givensb=R[k][k];
        R[k-1][k] =
            givensa*Givens[0][k-1]+givensb*Givens[1][k-1];
        R[k][k]=0.0;
        R[k][0]=-R[k-1][0]*Givens[1][k-1];
        R[k-1][0]=R[k-1][0]*Givens[0][k-1];
    }
    for(int i=k-1;i>=0;i--){
        xi[i]=R[i][0];
        for(int j=i+2;j<=k;j++)
            xi[i] -= R[i][j] * xi[j-1];
        xi[i] /= R[i][i+1];
    }
    s = x;
    for(int j=0;j<k;j++)
        s += xi[j] * *Q[j];
    printf("res. at step k=%d is %f\n",
        k,res=sqrt((r=A*s-f)*r));
}
return x = s;
} // GMRES with initial iterations
```
