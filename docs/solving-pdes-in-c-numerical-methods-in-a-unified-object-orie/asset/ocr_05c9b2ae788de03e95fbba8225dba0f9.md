Still, on the other hand, the above also means that both A and Q are singular matrices, so the original system Ax = f may have no solution at all. To avoid singularity, we therefore add a small positive number to the main diagonal, as in Chapter 10.

So far, we’ve assumed that Q is defined geometrically by rediscretizing the Laplacian on the coarse grid. Alternatively, Q could also be defined algebraically by the triple product

```
Q ≡ RAP,
```

as in Chapter 17, Section 17.8. This way, as shown in Chapter 10 in [68], Q approximates A well not only for positive-semidefinite or SPD problems but also for indefinite problems. This approach is indeed used in the present implementation.

# 23.8 Multiple Right-Hand Sides

One way to produce a sharp image is to distinguish between different pixels. At each particular pixel, it makes sense to use an image u^(i) that has little blur at this pixel, or has a rather large source or sink at this pixel. For this purpose, we need to pick the correct right-hand side f^(i) that has a rather large absolute value at that pixel. This f^(i) is the only one that should contribute to f at that pixel.

Recall that, in the fusion problem, A has been applied to the original images

```
u^(1), u^(2), ..., u^(m)
```

to produce the multiple right-hand sides

```
f^(1) = A u^(1), f^(2) = A u^(2), ..., f^(m) = A u^(m).
```

Each right-hand side discretizes the divergence of the gradient of the corresponding image, so it contains the sources and sinks in this image.

# 23.9 The Right-Hand Side

The multiple right-hand sides

```
f^(1), f^(2), ..., f^(j), ..., f^(m)
```

should thus be incorporated into a new right-hand side f with sources and sinks with maximal absolute value. For this purpose, let us first define the "max()" function that takes two N-dimensional vectors u and v to produce the new N-dimensional vector max(u, v) by picking the larger value (in magnitude) at each component (or pixel):

```
(max(u, v))_i ≡ { u_i if |u_i| ≥ |v_i|, v_i if |u_i| < |v_i| }
```

(1 ≤ i ≤ N). This function is then used in the inductive definition of f:

```
f ≡ max(f^(1), f^(2), ..., f^(m)) ≡ max(max(f^(1), f^(2), ..., f^(m-1)), f^(m)).
```

This way, each component (or pixel) in f is indeed the maximal component (in magnitude) in the f^(i)'s. This is why f is indeed used in the multigrid fusion algorithm below.