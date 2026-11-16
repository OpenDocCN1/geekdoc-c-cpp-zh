takes simplicial \(k\)-forms to square-integrable \(k\)-forms on the simplicial manifold, where we assume each simplex carries the standard Euclidean structure. The Whitney map is the right inverse of the so-called de Rham map,

```
\(\alpha(\sigma) = \int_\sigma W(\alpha)\)
```

for all discrete \(k\)-forms \(\alpha\) and all \(k\)-cells \(\sigma\). For details we refer to [426]. The Whitney map \(W\) is a chain map—it commutes with the differential (\(dW = W\delta\)) and thus factors to cohomology.

Dodzuki and Patodi [124] use the Whitney map in order to define an inner product on discrete \(k\)-forms (\(k\)-cochains) by

```
\((\alpha, \beta)_k = \int_M g(W\alpha, W\beta)\text{vol}_g,\)
```

where (in our case) \(g\) denotes a piecewise Euclidean metric on the simplicial manifold. From the perspective of the *Finite Element Method* (FEM), Whitney's construction is a special case of constructing stable finite elements; see [12].

For triangle meshes the resulting strongly defined Laplacian acting on 0-forms (functions) is given by

```
\(\mathbb{L} = \mathbb{M}_0^{-1} L,\)
```

where \(\mathbb{M}_0\) is the *mass matrix* given by

```
\((\mathbb{M}_0)_{ij} = \begin{cases} \frac{A_{ij}}{12}, & \text{if } i \sim j, \\ \frac{A_i}{6}, & \text{if } i = j, \\ 0, & \text{otherwise.} \end{cases}\)
```

Here \(A_{ij}\) denotes the combined area of the two triangles incident to edge \((i, j)\) and \(A_i\) is the combined area of all triangles incident to vertex \(i\). The corresponding weakly defined Laplacian \(L\) is the *stiffness matrix* with entries

```
\(L_{ij} = \begin{cases} -\frac{1}{2}(\cot \alpha_{ij} + \cot \beta_{ij}), & \text{if } i \sim j, \\ -\sum_{j \sim i} L_{ij}, & \text{if } i = j, \\ 0, & \text{otherwise,} \end{cases}\)
```

where \(\alpha_{ij}\) and \(\beta_{ij}\) are the two angles opposite to edge \((i, j)\). The matrix \(L\) is often referred to as the *cotan Laplacian*.

The cotan Laplacian has been rediscovered many times in different contexts [130, 134, 309]; the earliest explicit mention seems to go back to MacNeal [262], but perhaps it was already known at the time of Courant. The cotan Laplacian has been enjoying a wide range of applications in geometry processing (see [109, 242, 341] and references therein), including barycentric coordinates (see in particular Section 1.2.2 in this book), mesh parameterization, mesh compression,