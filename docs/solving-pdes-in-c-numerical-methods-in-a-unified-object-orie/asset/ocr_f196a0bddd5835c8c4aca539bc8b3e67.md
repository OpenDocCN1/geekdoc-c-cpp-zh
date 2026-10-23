This formula is implemented in the code below. The function "deriveProduct()" takes as input two "list" objects that contain the derivatives of f and g up to and including order n at the fixed point x and returns the nth derivative of fg at x. It is assumed that a global array of integers that contains Pascal's triangle is available. This array, named "triangle", is formed in advance, as in Chapter 1, Section 19, and placed in a global domain accessible to the "deriveProduct()" function. This seems to be a better strategy than recalculating the required binomial coefficients each time the function is called:

```
template<class T>
const T
deriveProduct(const list<T>&f,const list<T>g,int n){
    T sum = 0;
    for(int i=0; i<=n; i++)
        sum += triangle[n-i][i] * f[i] * g[n-i];
    return sum;
} // nth derivative of a product
```

# 5.13 Polynomial of Two Variables

The polynomial ∑ a_i x^i in Section 5.4 is implemented as the list of coefficients a0, a1, a2, ..., an. This implementation is appropriate because the polynomial is defined uniquely by its coefficients.

Still, one may ask, why use a list rather than a vector? After all, the coefficients are all of the same type, so they can be safely stored in a vector of dimension n + 1. Furthermore, a vector is more efficient than a list thanks to direct indexing, that is, using an array to store the coefficients themselves rather than their addresses. This saves not only storage but also valuable time, by using efficient loops over the coefficients stored continuously in the computer memory. Why then use a list?

The answer is that, in some cases, the coefficients in the polynomial occupy different amounts of memory, and hence cannot be stored in an array. Consider, for example, the polynomial of two independent variables x and y:

p(x, y) ≡ ∑_{i+j ≤ n} a_{i,j} x^i y^j

where i and j are nonnegative indices, a_{i,j} are the given coefficients, and n is the degree of the polynomial. This polynomial may also be written in the form