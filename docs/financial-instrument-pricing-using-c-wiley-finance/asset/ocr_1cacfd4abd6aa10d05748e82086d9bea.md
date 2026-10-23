The analytical solution can be found by the method of Separation of Variables (Smith, 1978):

$$u(x,t)=\frac{8}{\pi^2}\sum_{n=1}^{\infty}\frac{1}{n^2}\left(\sin\frac{1}{2}n\pi\right)(\sin\,n\pi x)e^{-n^2\pi^2 t}.$$

Answer the following questions:

+   a) Implement the above solution using double and multiprecision data types. In particular, determine how many terms need to be taken in the series to achieve a given accuracy.
+   b) Parallelise the code in part a) by using the parallel reduction and aggregation code in Chapter 30.
+   c) Approximate the solution of the heat equation using the finite difference methods, starting in Chapter 13.

# 5. (Confluent Hypergeometric Function)

This function is defined as follows (Abramowitz and Stegun, 1965):

$$M(\alpha,\gamma,z)=\sum_{n=0}^{\infty}\frac{\Gamma(\alpha)\Gamma(\alpha+n)}{\Gamma(\alpha)\Gamma(\gamma+n)}\frac{z^{n}}{n!}$$

where $\Gamma(z)$ is the gamma function, that is $\Gamma(z)=\int_{0}^{\infty}t^{z-1}e^{-t}dt$.

Answer the following questions:

+   a) Implement this formula as a sum of terms, each of which is the following mix of C++ and Boost code:

```
template <typename T>
std::complex<T> CHFTerm(T alpha, T gamma, int n,
    const std::complex<T>& z)
{
    using boost::math::tgamma;
    using boost::math::factorial;

    T nt = static_cast<T>(n);
    T coeff = (tgamma(gamma) * tgamma(alpha + nt))
              / (tgamma(alpha) * tgamma(gamma + nt));

    // Write z^n in polar form
    T x = z.real(); T y = z.imag();
    T r = boost::multiprecision::sqrt(x*x + y*y);
    T rn  = boost::multiprecision::pow(static_cast<T>(r),
                static_cast<T>(n));
    std::complex<T> inTheta(static_cast<T>(0.0),
                static_cast<T>(n)*std::arg(z));
    std::complex<T> zn = rn*std::exp<T>(inTheta);
    T fac = 1.0 / factorial<T>(n);

    return coeff * zn * fac;
}
```