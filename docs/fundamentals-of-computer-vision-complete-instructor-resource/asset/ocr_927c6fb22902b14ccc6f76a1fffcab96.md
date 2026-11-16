![](bbox=[0.19, 0.11, 0.71, 0.36])

Figure 10.24 Moving left to right, from a point on the manifold that represents one type of shark to another. The upper set of curves are vectors, all of which are part of a geodesic on the manifold. The lower set of curves moves in a straight line through the 256-dimensional Euclidean space. Clearly, the second set of vectors are not all closed curves.

With Eqs. 10.89 and 10.90 one can do a bit of algebra involving the sine and cosine of a sum and the properties of the sine and cosine of small numbers to find that

```
\Phi_1(\theta + h) = \Phi_1 + \frac{1}{2\pi} \int_0^{2\pi} h(s)ds
\Phi_2(\theta + h) = \Phi_2 - \int_0^{2\pi} \sin(\theta(s))h(s)ds
\Phi_3(\theta + h) = \Phi_3 + \int_0^{2\pi} \cos(\theta(s))h(s).ds.
```

Defining the small movements as

```
d\Phi_1 \equiv \frac{1}{2\pi} \int_0^{2\pi} h(s)ds
d\Phi_2 \equiv - \int_0^{2\pi} \sin(\theta(s))h(s)ds
d\Phi_3 \equiv \int_0^{2\pi} \cos(\theta(s))h(s).ds.
```

At this point, let’s switch from vectors of infinite length in a functional space to very long vectors with $d$ elements, where $d$ might be a thousand. There isn’t much practical difference, but it will allow a more convenient notation.

Observe that $d\Phi_1$ can be written as an inner product:

```
d\Phi_1 = \left\langle \frac{1}{2\pi} \mathbf{h} \right\rangle.
```