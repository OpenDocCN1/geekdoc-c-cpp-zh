and the difference equation

$$\tilde{u}((j+1)h)=\sum_{i=0}^{n} h^{i}\frac{\tilde{u}^{(i)}(jh)}{i!}\,.$$

where the $\tilde{u}^{(i)}(jh)$'s are calculated by the recursive formula

$$\tilde{u}^{(0)}(jh)=\tilde{u}(jh),$$ $$\tilde{u}^{(i+1)}(jh)=S\tilde{u}^{(i)}(jh)+f^{(i)}(jh).$$

This recursion is a short-memory process: $\tilde{u}^{(i+1)}(jh)$ is a function of $\tilde{u}^{(i)}(jh)$ alone and is independent of $\tilde{u}^{(0)}(jh)$, $\tilde{u}^{(1)}(jh)$, ..., $\tilde{u}^{(i-1)}(jh)$. This is why the code below is based on the standard algorithm in Chapter 5, Section 11, rather than Horner's algorithm: it avoids storing the entire list of numbers calculated in the above recursion. Instead, each one of them contributes to the sum and is then replaced by the next one.

The advantage of object-oriented programming is clear here. Indeed, the matrix and vector objects implemented in the low-level code in Chapter 2, Sections 18 and 20, are used in the present high-level code, which preserves the spirit of the original mathematical formula:

```
template<class T, int N>
const vector<T,N>
TaylorScheme(const vector<T,N>&u0,
    const matrix<T,N,N>&S,
    const list<vector<T,N> >&f,
    const T&h){
    T powerOfHoverIfactorial = 1;
    vector<T,N> sum=0;
    vector<T,N> uDerivative = u0;
    for(int i=0; i<f.size(); i++){
        sum += powerOfHoverIfactorial * uDerivative;
        uDerivative = S * uDerivative + f[i];
        powerOfHoverIfactorial *= h/(i+1);
    }
    return sum;
} // Taylor scheme
```

This completes the definition and implementation of the Taylor scheme. Next, we study the discretization error in this scheme. (See also chapter 25 below.)

# 6.10 Computational Error Estimates

Here we see the main advantage in the Taylor scheme and its C++ implementation: the opportunity to compute error estimates.

The error term in the Taylor approximation is given by

$$\frac{h^{n+1}u^{(n+1)}(\xi)}{(n+1)!}\,.$$