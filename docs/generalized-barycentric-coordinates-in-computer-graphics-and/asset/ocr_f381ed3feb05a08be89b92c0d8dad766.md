Green's third integral identity to harmonic functions, which is equivalent in 2D to Cauchy's integral formula [5]. The (real-valued) expressions for Green coordinates are more complicated, compared to (7.13), and working with complex numbers is a great advantage; however, in contrast to Cauchy coordinates, Green coordinates have a natural generalization to 3D where they lead to volumetric harmonic maps [42, 252].

# 7.2.2 General construction of complex barycentric coordinates

In the previous section we derived Cauchy's complex barycentric coordinates. Our construction was based on Cauchy's kernel, which reproduces holomorphic functions in the transfinite case. Holomorphic functions are extremely valuable in the context of planar shape deformation due to their relation to conformal maps. However, holomorphic maps form a rather small subspace out of the wide space of complex-valued maps. In particular, they do not allow for the Lagrange (interpolation) property to hold. Non-holomorphic complex barycentric coordinates clearly exist, since any real barycentric coordinates are also complex barycentric coordinates. As we will see next, there exist complex barycentric coordinates that are neither real nor holomorphic, and in contrast to Cauchy's coordinates, some of them possess the Lagrange property.

It is convenient to think about complex barycentric coordinates as a special type of complex basis functions that are associated with the cage's vertices. However, unlike arbitrary basis functions, the additional requirements (7.1) and (7.2) make it challenging to design such coordinates. To overcome this problem, we follow the same approach as in Section 1.1.2.

**Definition 7.1.** A set of complex-valued functions \(w_i : \Omega \to \mathbb{C}\), \(i = 1, \dots, n\) that satisfy

```
\(\sum_{i=1}^n w_i(z)(z_i - z) = 0 \quad (7.14)\)
```

at every point \(z \in \Omega\) are called *complex homogeneous coordinates*.

Normalizing these weight functions then gives complex barycentric coordinates.

**Proposition 7.2.** Let \(w_i(z)\) be complex homogeneous coordinates, such that their sum at every point \(z \in \Omega\) is nonvanishing. Then the normalized functions

```
\(\phi_i(z) = \frac{w_i(z)}{\sum_{j=1}^n w_j(z)} \quad (7.15)\)
```

are complex barycentric coordinates.

**Proof.** The partition of unity property (7.1) follows immediately from the normalization in (7.15). The linear precision property (7.2) is due to

```
\(\sum_{i=1}^n \phi_i(z)z_i = \sum_{i=1}^n \frac{w_i(z)z_i}{\sum_{j=1}^n w_j(z)} = \frac{1}{\sum_{j=1}^n w_j(z)} \sum_{i=1}^n w_i(z)z_i = \frac{1}{\sum_{j=1}^n w_j(z)} \sum_{i=1}^n w_i(z)z = z,\)
```