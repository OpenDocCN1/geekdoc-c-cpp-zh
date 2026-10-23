# 2.23. Diagonalization

Let A^{(i)} denote the ith column in A, so (A')^{(i)} is the ith row in A. The algorithm is now defined as follows [15]:



+   - Initialize both W and Z to be the identity matrix of order n.

+   - For i = 1,2,...,n, do the following:

1. For j = 1,2,...,i-1, update W^{(i)} (the ith column in W) by

W^{(i)} \leftarrow W^{(i)} - \frac{(A^{(i)},Z^{(j)})}{D_{j,i}} W^{(j)}

[where the numerator in the above coefficient is the so-called real inner product (that declines to take the complex conjugate) of the ith row in A with the jth column in Z].

2. Similarly, for j = 1,2,...,i-1, update Z^{(i)} (the ith column in Z) by

Z^{(i)} \leftarrow Z^{(i)} - \frac{(W^{(j)},A^{(i)})}{D_{j,i}} Z^{(j)}

(where the numerator in the above coefficient is the real inner product of the jth column in W with the i column in A).

3. Finally, define

D_{i,j} \equiv (W^{(i)},A Z^{(j)})

(real inner product, with no complex conjugate).

Fortunately, this algorithm uses mainly column operations, so the implementation of the "matrix" object in Section 2.20 as a collection of column vectors is particularly suitable. To benefit from this structure fully, however, we must first add an extra "operator()" member function to the block of the base "vector" class in Section 2.18:

```
T& operator() (int i) {
return component[i];
} // read/write ith component
```

This operator can now be called from another "operator()" member function that should be added to the block of the derived "matrix" class in Section 2.20:

```
vector<T,N>& operator() (int i) {
return vector<vector<T,N>,M>::operator() (i);
} // read/write ith column
```

With this new operator, one may not only read the 'i th column of a "matrix" object 'm' by writing "m[i]", but also change it by writing "m(i)", which returns a nonconstant reference to it.