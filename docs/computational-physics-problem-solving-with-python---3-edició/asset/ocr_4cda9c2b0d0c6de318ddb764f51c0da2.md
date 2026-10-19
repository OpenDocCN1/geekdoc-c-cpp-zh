mean when we say that two functions are not correlated? Well, if the two tend to oscillate with their nodes and peaks in much the same places, then the two functions are clearly correlated. An analytic measure of the correlation of two arbitrary functions $y(t)$ and $x(t)$ is the correlation function

```
c(τ) = ∫_{-∞}^{+∞} dt y^*(t) x(t + τ) ≡ ∫_{-∞}^{+∞} dt y^*(t - τ) x(t) ,  (12.55)
```

where τ, the lag time, is a variable. Even if the two signals have different magnitudes, if they have similar time dependences except for one lagging or leading the other, then for certain values of τ the integrand in (12.55) will be positive for all values of t. For those values of τ, the two signals interfere constructively and produce a large value for the correlation function. In contrast, if both functions oscillate independently regardless of the value of τ, then it is just as likely for the integrand to be positive as to be negative, in which case the two signals interfere destructively and produce a small value for the integral.

Before we apply the correlation function to our problem, let us study some of its properties. We use (12.18) to express c, y^*, and x in terms of their Fourier transforms:

```
c(τ) = ∫_{-∞}^{+∞} dω'' C(ω'') \frac{e^{i ω'' t}}{√{2π}} ,    y^*(t) = ∫_{-∞}^{+∞} dω Y^*(ω) \frac{e^{-i ω t}}{√{2π}} ,  
 x(t + τ) = ∫_{-∞}^{+∞} dω' X(ω') \frac{e^{+i ω t}}{√{2π}} .  (12.56)
```

Because ω, ω', and ω'' are dummy variables, other names may be used for these variables without changing any results. When we substitute these representations into definition (12.55) of the correlation function and assume that the resulting integrals converge well enough to be rearranged, we obtain

```
∫_{-∞}^{+∞} dω C(ω) e^{i ω t} = ∫_{-∞}^{+∞} \frac{dω}{2π} ∫_{-∞}^{+∞} dω' Y^*(ω) X(ω') e^{i ω τ} 2π δ(ω' - ω)  
 = ∫_{-∞}^{+∞} dω Y^*(ω) X(ω) e^{i ω τ} ,  
 ⇒  C(ω) = √{2π} Y^*(ω) X(ω) ,  (12.57)
```

where the last line follows because ω'' and ω are equivalent dummy variables. Equation 12.57 says that the Fourier transform of the correlation function between two signals is proportional to the product of the transform of one signal and the complex conjugate of the transform of the other. (We shall see a related convolution theorem for filters.)