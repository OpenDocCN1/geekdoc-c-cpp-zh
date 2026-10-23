
```
if(fabs(u[i]) < fabs(v[i]))
    maxuv(i) = v[i];
return maxuv;
} // maximum absolute value
```

This function is now used to implement the max() function for a list of m vectors as well, as in Section 23.9 above:

```
template<class T>
const T
max(const list<T>&l){
    T maxl = l[0];
    for(int i=1; i<l.size(); i++)
        maxl = max(maxl,l[i]);
    return maxl;
} // maximum modulus of list of vectors
```

We are now ready to implement the multigrid fusion algorithm. This is indeed done in the "fuse()" function below. This function takes two arguments: the list of vectors "f1m" that contains the multiple right-hand-side vectors f^(1), f^(2), ..., f^(m), and the multigrid object "mg" that contains the sparse coefficient matrix that discretizes the Laplacian with Neumann boundary conditions.

```
template<class T>
const dynamicVector<T>
fuse(const list<dynamicVector<T> >&f1m,
    const multigrid<T>&mg){
    dynamicVector<T> f = max(f1m);
    return mg.getNext() ?
        mg.getP() * (fuse(mg.getR() * f1m,
            *mg.getNext()))
        - mg.getR() * f / *mg.getNext()
    + f / mg
    :
    f / mg;
} // multigrid fusion algorithm
```

## 23.14 Example

In the present example, two blurred images of Lena are used. Each image is divided into four subsquares. One image contains blur in the upper-right and lower-left subsquares, including Lena's eyes and nose (Figure 23.1). The other image contains blur in the upper-left and lower-right subsquares, including Lena's eyebrows (Figure 23.2). The multigrid fusion algorithm implemented in Section 23.13 above fuses these two images into one good image with no blur at all (Figure 23.3).

![](img/1f293b0ceb2de964310ea7f941a1b580_576_0.png)

Figure 23.1. The first blurred image, in which the upper-right and lower-left subsquares (including Lena’s eyes and nose) are blurred.

![](img/1f293b0ceb2de964310ea7f941a1b580_577_0.png)

Figure 23.2. The second blurred image, in which the lower-right and upper-left subsquares (including Lena's eyebrows) are blurred.

![](img/1f293b0ceb2de964310ea7f941a1b580_578_0.png)

Figure 23.3. The result of the multigrid fusion algorithm that fuses the above blurred images of Lena into one good image.

# Part VII

Applications in Three Spatial Dimensions

# Part VII. Applications in Three Spatial Dimensions

In this part, we use the present object-oriented framework to implement three-dimensional finite elements as well. The resulting mesh of tetrahedra is particularly suitable for adaptive refinement. High-order finite elements with continuous gradients across edges in the mesh are implemented as well.

These advanced objects are then used in the numerical solution of complicated systems of nonlinear PDEs, including Navier–Stokes, Maxwell, and Helmholtz equations in three spatial dimensions.

The present object-oriented framework is particularly useful for the linearization required in Newton’s iteration. Indeed, the stiffness matrix that is assembled and (implicitly) inverted in each Newton iteration contains elements that are complicated objects in their own right, rather than mere scalars.

The present Maxwell solver is a combination of the present Stokes and Helmholtz solvers. Inverse problems associated with these problems are also discussed. Finally, the Maxwell solver is also modified to serve as a Navier–Stokes solver.

# Chapter 24

# Polynomials in Three
# Independent Variables

In this chapter, we reimplement polynomials of one and two variables in a slightly more straightforward way than in Chapter 5. Furthermore, we use this implementation to implement polynomials of three variables as well. Moreover, we implement useful operators and functions, including integration over the unit tetrahedron in Figure 27.1. These functions are particularly useful in the finite-element discretization of linear and nonlinear PDEs later on in the book.

## 24.1  The Polynomial Object

The template “polynomial” class is derived from the “list” class in Section 3.4 above:

```
template<class T> class polynomial:public list<T>{
```

Thanks to the fact that the fields “number” and “item” are declared as merely protected (rather than private) in the base “list” class, they can be accessed and set in the following constructor:

```
public:
    polynomial(int n=0){
        number = n;
        item = n ? new T*[n] : 0;
        for(int i=0; i<n; i++)
            item[i] = new T(0);
    }  // constructor
```

In fact, this constructor first calls implicitly the default constructor of the base “list” class to initialize the “number” and “item” fields to zero, and then changes these fields to construct a trivial polynomial with ‘n’ zero coefficients.

Similarly, the following constructor constructs a polynomial of ‘n’ coefficients that are all equal to ‘a’.

```
polynomial(int n, const T&a){
    number = n;
    item = n ? new T*[n] : 0;
    for(int i=0; i<n; i++)
        item[i] = new T(a);
}   // constructor with 'T' argument
```

As mentioned above, some compilers (such as GNU Version 3.2 and higher) may require the prefix 'this->' to access the fields 'number' and 'item' inherited from the base "list" class:

```
this->number = n;
```

(See also the code in Section A.34 in the Appendix and the code on the Web page of the book at http://www.siam.org/books/cs09, which compile with new GNU versions as well.) In the sequel, however, we don't bother to add this prefix.
The next constructor constructs a polynomial with the two coefficients 'a' and 'b':

```
polynomial(const T&a, const T&b){
    number = 2;
    item = new T*[2];
    item[0] = new T(a);
    item[1] = new T(b);
}   // constructor with 2 'T' arguments
```

The following destructor only calls implicitly the default destructor of the base "list" class:

```
~polynomial(){
}   // destructor
```

The next function returns the degree of polynomial:

```
int degree() const{
    return number-1;
}   // degree of polynomial
```

The next function allows the user to access the 'i'th coefficient in the polynomial:

```
T& operator()(int i){
    return list<T>::operator()(i);
}   // read/write ith coefficient
```

Indeed, with this function, the user can access the 'i'th coefficient in the well-defined polynomial 'p' simply by writing 'p(i)'.
The following member functions are only declared here; their detailed definitions will be provided later on. Note that the arguments passed to the functions are of type 'S', which may be different from 'T':

```
```cpp
template<class S>
    const T
    HornerArray(T* const&, int, const S&) const;
template<class S>
    const T operator()(const S&) const;
template<class S>
    const S operator()(const S&, const S&) const;
template<class S>
    const S operator()(const S&,
        const S&, const S&) const;
};
```
```

This completes the block of the "polynomial" class. Next, we define some useful arithmetic operators with polynomials.

## 24.2  Adding Polynomials

The "+ =" operator defined below is an ordinary (nonmember) function that takes two polynomial arguments, and adds the second one to the first one. This is why only the second one is declared as constant, whereas the first one is nonconstant.

```
```cpp
template<class T>
const polynomial<T>&
operator+=(polynomial<T>& p, const polynomial<T>& q){
```
```

If 'p' has a larger degree than 'q', then the coefficients in 'q' are added one by one to the corresponding coefficients in 'p':

```
```cpp
if(p.degree() >= q.degree())
    for(int i=0; i<=q.degree(); i++)
        p(i) += q[i];
```
```

If, on the other hand, 'q' has a larger degree than 'p', then 'q' cannot be added to 'p' by a straightforward procedure as above. Instead, the "+ =" operator must be called recursively, with the roles of 'p' and 'q' interchanged. However, since 'q' is constant, it must first be assigned to the local nonconstant polynomial "keepQ", to which 'p' can be added:

```
```cpp
else{
    polynomial<T> keepQ = q;
    p = keepQ += p;
}
return p;
}   // add a polynomial
```
```

With this operator, the user can write commands like “p += q” to add the well-defined polynomial ‘q’ to the well-defined polynomial ‘p’. Furthermore, this operator is now used to define a ‘+’ operator as well:
