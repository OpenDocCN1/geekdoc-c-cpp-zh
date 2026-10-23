# 5.38 Convolution

Let

u ≡ (u0, u1, u2, …, u_{l−1})^t

be an l-dimensional vector and

v ≡ (v0, v1, v2, …, v_{m−1})^t

be an m-dimensional vector. The convolution of u and v is the (l + m − 1)-dimensional vector defined by

(u * v)_k ≡ Σ_{0 ≤ i < l, 0 ≤ j < m, i + j = k} u_i v_j

(0 ≤ k < l + m − 1).

Clearly, if u contains the coefficients of the polynomial

u(z) ≡ Σ_{i=0}^{l−1} u_i z^i

and v contains the coefficients of the polynomial

v(z) ≡ Σ_{j=0}^{m−1} v_j z^j

then the convolution vector defined above contains the coefficients of the product polynomial u(z)v(z).

Let us now use FFT to calculate the convolution efficiently. To this end, let us first define a simple operator that multiplies two vectors of the same dimension component by component:

```
template<class T>
const dynamicVector<T>
operator|(const dynamicVector<T>&u,
    const dynamicVector<T>&v) {
    dynamicVector<T> uv(u.dim(),0.);
    for(int i=0; i<u.dim(); i++)
        uv(i) = u[i] * v[i];
    return uv;
} // multiply component by component
```

With this operator, one can simply write "u|v" to return the vector whose i-th component is the product of the i-th component in `u` by the i-th component in `v`. This operator is indeed useful in the convolution operator defined next:

```
template<class T>
const dynamicVector<complex>
operator||(const dynamicVector<T>&u,
    const dynamicVector<T>&v) {
    const complex I(0.,1.);
```