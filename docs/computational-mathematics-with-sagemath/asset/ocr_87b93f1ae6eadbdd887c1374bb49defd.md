where the numbers $δ_n$ have a small absolute value when compared to $y_n$; think for instance of the integration of the celestial mechanics ordinary differential equations to simulate the solar system: large values (of the distances, of the velocities) undergo very small perturbations in the long time [HLW02]. Even if it is possible to compute precisely the $δ_n$ terms, rounding errors when doing the additions $y_{n+1} = y_n + δ_n$ will introduce important errors.

As an example, consider the sequence defined by $y_0 = 10^{13}$, $δ_0 = 1$ and $δ_{n+1} = aδ_n$ with $a = 1 - 10^{-8}$. The standard, naive, programming way to compute $y_n$ is:

```
    sage: def iter(y,delta,a,n):
    ....:     for i in range(0,n):
    ....:         y += delta
    ....:         delta *= a
    ....:     return y
```

As we have chosen rational values for $y_0$, $δ_0$ and $a$, we can compute the exact value of the iterates with Sage:

```
    sage: def exact(y,delta,a,n):
    ....:     return y*delta*(1-a^n)/(1-a)
```

Now, let us compute again 100 000 iterates but with floating-point numbers in RDF (for instance), and let us compare the result with the exact value:

```
    sage: y0 = RDF(10^13); delta0 = RDF(1); a = RDF(1-10^(-8)); n = 100000
    sage: ii = iter(y0,delta0,a,n)
    sage: s = exact(10^13,1,1-10^(-8),n)
    sage: print("exact - classical summation: %.1f" % (s-ii))
    exact - classical summation: -45.5
```

Now, this is the *compensated summation* algorithm:

```
    sage: def sumcomp(y,delta,e,n,a):
    ....:     for i in range(0,n):
    ....:         b = y
    ....:         e += delta
    ....:         y = b+e
    ....:         e += (b-y)
    ....:         delta = a*delta # new value of delta
    ....:     return y
```

To understand the behaviour of this algorithm, let us look at the diagram below (we follow here the presentations of [Hig93] and [HLW02]), where the boxes represent the significand of the numbers. The position of the boxes represent the exponent (the more a box is to the left, the larger its exponent is):