amplitude. It turns out regarding the Fourier transform is a specialized case of the Laplace transform. Laplace replaced the met restrictions regarding the constant amplitudes of the sinusoidal components, which allows for many more types. In theory, the input signal could have a definite beginning, middle and end, and its frequency components could go and over time. The Laplace transform replaces the Fourier kernel e^(-jwt) with a more general version e^(-σ+jω)t that allows the sinusoidal components to exponentially increase, remain flat (as in Fourier) or exponentially decay in time. The real coefficient σ governs the behavior of the sinusoid's shape in time.

The Laplace transform is:

```
F(s) = \int f(t)e^{-st}dt
s = σ + jo  (1.12)
```

The discrete version of the Laplace transform is the z-Transform. In the z-Transform, you let z = e^ST where T is the sample period; we need to do this to get out of the continuous time domain t and into the discrete domain nT. This yields:

```
F(z) = \int f(t)z^{-t}dt\ns = \sum f(n)z^{-n} (1.13)
```

The z-Transform is a kind of keeping-or substitution transform that is clever—by making the simple substitution of z = e^ST arrive at a sum involving a rational function in z instead of the irrational e^ST. This means the z-Transform produces a simple polynomial or ratio of polynomials in z that obey all the laws of polynomial math, making it easier to work with. It can also operate over a fixed duration rather than an infinite period.

![](bbox=[0.198, 0.483, 0.802, 0.663])

Figure 1.21: Two sinusoids with one delayed by n samples.

Consider the z⁻n terms—what do they mean? Using polynomial math:

```
z^n = e^{sn}
z⁻¹ = (e^{ST})^{-¹} = e^{-ST}
z⁻² = (e^{ST})^{-2} = e^{-2ST}
etc... (1.14)
```

The T, 2T and 3T values represent 1, 2 and 3 sample intervals. The negative signs denote them as past sample intervals; a positive sign indicates future sample intervals that are not realizable in real-time, so you won't see them in this book. When we use the z-Transform to design and evaluate filters in Chapter 4, we will let the real part σ = 0. samples of delay, multiplying a signal against it will delay that signal by n-samples. This is astonishing because multiplication by a simple term T⁻