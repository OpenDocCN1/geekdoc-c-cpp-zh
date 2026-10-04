# Long-Memory Processes 457

difference and FARMA models, discussed in Section 11.2, are useful tools for modeling Iff-type data. Notice that Definition 11.2 defines long-memory behavior at different frequencies from zero, that is, “cyclic long memory”. In Section 11.3, we discuss the Gegenbauer and GARMA models for cyclic long-memory behavior, and in Section 11.4, we discuss the k-factor Gegenbauer k-factor GARMA models for data with a variety of types of long-memory behavior. In Sections 11.5 and 11.6, we discuss estimation and forecasting for k-factor GARMA models, and in Section 11.7, we apply the results to atmospheric CO2 data.

# 11.2 Fractional Difference and FARMA Processes

A widely used tool for analyzing long-memory time series is the fractional difference, (1 − B)α, which real for the (noninteger) α is defined by

```
$$(1-B)^\alpha f(t) = \sum_{k=0}^{\infty}(-1)^k \binom{\alpha}{k}B^k f(t)\n= \sum_{k=0}^{\infty}(-1)^k \binom{\alpha}{k}f(t-k),$$ (11.1)
```

where

```
$$\binom{\alpha}{k} = \frac{\Gamma(\alpha+1)}{\Gamma(\\alpha-k+1)k!}$$ (11.2)
```

and $\Gamma(z) = \int_0^{\infty} t^{z-1}e^{-t} dt$ is the gamma function. Using the fact that $\Gamma(x+1)=x\Gamma(x)$ for real x, it follows that

```
$$(1-B)^\alpha f(t) = \sum_{k=0}^{\infty}(-1)^k \frac{\Gamma(\alpha+1)}{\Gamma(\\alpha-k+1)k!}f(t-k)\n= \sum_{k=0}^{\infty} \frac{(k-\alpha-1)(k-\alpha-2)\cdots(-\alpha)}{k!}f(t-k)\n= \sum_{k=0}^{\infty} \frac{\Gamma(k-\alpha)}{\Gamma(-\alpha+1)k!}f(t-k).$$ (11.3)
```

Remark: The fractional difference can be extended to the case where α is any real or complex number. For our purposes it suffices for α to be real.