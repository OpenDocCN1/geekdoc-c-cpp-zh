```
template<class T>
const dynamicVector<T>
fuse(const list<dynamicVector<T> >&u1m,
    const list<dynamicVector<T> >&f1m,
    const multigrid<T>&mg) {
```

This list is indeed used to produce the alternative right-hand side 'f' at the fine level:

```
dynamicVector<T> f = max(mg.getA(), u1m, f1m);
```

Furthermore, in the recursive call to the "fuse()" function at the coarse level, the first argument is set to Q⁻¹ R times the original fine-level vectors f⁽¹⁾, f⁽²⁾, ..., f⁽ᵐ⁾.

```
return mg.getNext() ?
    mg.getP() *
    (fuse(mg.getR() * f1m / *mg.getNext(),
    mg.getR() * f1m, *mg.getNext())
    - mg.getR() * f / *mg.getNext())
    + f / mg
    :
    f / mg;
} // fuse the images in f1m
```

This completes the reimplementation of the multigrid fusion algorithm with the alternative right-hand side in Chapter 23, Section 23.10.

# A.25 Integral on the Unit Tetrahedron

The following code implements polynomials of three variables as in Section 24.8, and integrates them over the unit tetrahedron as in Section 24.12. In particular, the code defines the nodal basis functions in the unit tetrahedron, that is, the polynomials of three variables that have the value 1 at one corner of the tetrahedron and 0 at the other three corners:

p0(x,y,z) = 1 - x - y - z
p1(x,y,z) = x
p2(x,y,z) = y
p3(x,y,z) = z

First, we define the constant polynomial "zero" by calling the constructor that takes the integer argument 1 (to indicate that the degree of the polynomial is zero) and the "double" argument 0:

```
int main() {
    polynomial<double> zero(1,0.);
```

Next, we use the same constructor to define the constant polynomial of two variables "Zero":

```
polynomial<polynomial<double> > Zero(1,zero);
```