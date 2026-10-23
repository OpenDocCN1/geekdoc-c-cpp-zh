In this case the time variable is still continuous. We can discretise it in time using the BTCS (implicit Euler) scheme:

```
\frac{U(t + k) - U(t)}{k} = A U(t + k)
```

or

```
(I - kA)U(t + k) = U(t)
```

or

```
U(t + k) = (I - kA)^{-1} U(t).
```

This is now a first-order approximation to the exact solution. As with the previous examples we can define two approximate solutions on meshes of size k and 2k to get a second-order accurate solution extrapolation algorithm:

```
U^{(1)}(t + 2k) = (I - 2kA)^{-1} U(t)
U^{(2)}(t + 2k) = (I - kA)^{-1} (I - kA)^{-1} U(t)
U(t + 2k) = 2 * U^{(2)} - U^{(1)}.
```

Richardson extrapolation of the BTCS has a number of advantages:

+   It is second-order accurate in time.

+   It is an L-stable method (Lawson and Morris, 1978) which makes it suitable for stiff equations and equations with discontinuous initial conditions. The Crank–Nicolson method is only A-stable and it can produce oscillations. A workaround is to apply the method described in Rannacher (1984) in which the BTCS scheme is employed for the first few time steps and then Crank–Nicolson is used when initial oscillations have subsided.

+   It can be parallelised; the schemes on mesh size k and k/2 can run in parallel.

We shall discuss the implementation of this method in Chapter 21.

# 20.10 SUMMARY AND CONCLUSIONS

In this chapter we have introduced one-factor PDEs and we defined how they are incorporated into an IBVP that we then approximate using the finite difference method. We have attempted to give an overview of major mathematical and numerical topics that need to be understood before designing the related algorithms and their subsequent implementation in C++. In particular, in Section 20.6 we proposed 18 attention points that you should be acquainted with when working with FDM. For a more detailed account of the finite difference method, see Duffy (2006).