```
template<class T>
const difference<T>
operator*(const difference<T>&d, const T&t) {
    return difference<T>(d) *= t;
}  // "difference" times scalar
```

Next, we introduce the operator that returns the product of a difference operator and a vector, or the difference operator applied to a vector. Here, the read-only version of the "operator()" of the "difference" class and the read-only "operator[]" of the "dynamicVector" class are used in the calculations, and the read/write "operator()" of the "dynamicVector" class is then used to assign these calculated values to the appropriate components in the output vector. We also use here the "min()" and "max()" functions from Chapter 1, Section 9:

```
template<class T>
const dynamicVector<T>
operator*(const difference<T>&d,
        const dynamicVector<T>&v) {
dynamicVector<T> dv(v.dim(),0.);
for(int i=0; i<v.dim(); i++)
    for(int j=max(0,i-1); j<=min(v.dim()-1,i+1); j++)
        dv(i) += d(i,j,"read")*v[j];
return dv;
}  // "difference" times vector
```

Next, we implement the operator that "divides" a vector by a difference operator, or, more precisely, solves numerically a tridiagonal linear system of the form Dx = f. Because the solution vector x can be expressed as D⁻¹f or f/D, the binary "operator/" seems to be most suitable for denoting this operation.

For simplicity, the solution vector x is computed approximately using the Gauss-Seidel iterative method of Chapter 17, Section 3. Of course, this is not a very efficient linear-system solver: the multigrid algorithm used in Chapter 10, Section 5 and Chapter 17, Section 8, makes a much better solver that is particularly well implemented in C++. Still, the Gauss-Seidel iteration is good enough for our main purpose: writing and debugging the overall algorithm and code for the numerical solution of the convection-diffusion equation:

```
template<class T>
const dynamicVector<T>
operator/(const dynamicVector<T>&f,
        const difference<T>&d) {
dynamicVector<T> x(f);
for(int iteration=0; iteration < 100; iteration++)
    for(int i=0; i<f.dim(); i++){
        double residual = f[i];
        for(int j=max(0,i-1); j<=min(f.dim()-1,i+1); j++)
            residual -= d(i,j,"read")*x[j];
```