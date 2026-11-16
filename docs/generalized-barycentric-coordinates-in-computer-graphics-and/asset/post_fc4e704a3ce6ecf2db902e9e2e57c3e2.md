
## A Primer on Laplacians

**Max Wardetzky**

*Georg-August-University Göttingen, Germany*

## CONTENTS

- 5.1 Introduction .................................... 77
- 5.1.1 Basic properties .............................. 78
- 5.2 Laplacians on Riemannian manifolds .............. 79
- 5.2.1 Exterior calculus ............................. 79
- 5.2.2 Hodge decomposition ........................... 81
- 5.2.3 The spectrum .................................. 82
- 5.3 Discrete Laplacians ............................. 83
- 5.3.1 Laplacians on graphs .......................... 83
- 5.3.2 The spectrum .................................. 84
- 5.3.3 Laplacians on simplicial manifolds ............ 86
- 5.3.4 Strongly and weakly defined Laplacians ........ 87
- 5.3.5 Hodge decomposition ........................... 88
- 5.3.6 The cotan Laplacian and beyond ................ 88
- 5.3.7 Discrete versus smooth Laplacians ............. 90

IN THIS CHAPTER we review some important properties of Laplacians, smooth and discrete. We place special emphasis on a unified framework for treating smooth Laplacians on Riemannian manifolds alongside discrete Laplacians on graphs and simplicial manifolds. We cast this framework into the language of linear algebra, with the intent to make this topic as accessible as possible. We combine perspectives from smooth geometry, discrete geometry, spectral analysis, machine learning, numerical analysis, and geometry processing within this unified framework. The connection to generalized barycentric coordinates is established through harmonic functions that interpolate given boundary conditions.

### 5.1 INTRODUCTION

The Laplacian is perhaps *the* prototypical differential operator for various physical phenomena. It describes, for example, heat diffusion, wave propagation, steady state fluid flow, and it is key to the Schrödinger equation in quantum mechanics. In Euclidean space, the Laplacian of a smooth function \(u: \mathbb{R}^n \to \mathbb{R}\) is given as the sum of second partial derivatives along the coordinate axes,

```
\(\Delta u = - \left( \frac{\partial^2 u}{\partial x_1^2} + \frac{\partial^2 u}{\partial x_2^2} + \cdots + \frac{\partial^2 u}{\partial x_n^2} \right),\)
```

where we adopt the geometric perspective of using a minus sign.

### 5.1.1 Basic properties

The Laplacian has many intriguing properties. For the remainder of this exposition, consider an open and bounded domain \(\Omega \subset \mathbb{R}^n\) and the \(L^2\) inner product

```
\((f, g) = \int_\Omega fg\)
```

on the linear space of square-integrable functions on \(\Omega\). Let \(u, v: \Omega \to \mathbb{R}\) be two (sufficiently smooth) functions that vanish on the boundary of \(\Omega\). Then the Laplacian \(\Delta\) is a _symmetric_ (or, to be precise, a formally self-adjoint) linear operator with respect to this inner product, since integration by parts yields

```
(Sym) \((u, \Delta v) = \int_\Omega \nabla u \cdot \nabla v = (\Delta u, v).\)
```

Here \(\nabla\) denotes the standard gradient operator and \(\nabla u \cdot \nabla v\) denotes the standard inner product between vectors in \(\mathbb{R}^n\). The choice of using a minus sign in the definition of the Laplacian makes this operator positive semidefinite, since

```
(PSD) \((u, \Delta u) = \int_\Omega \nabla u \cdot \nabla u \ge 0.\)
```

If one considers only functions that vanish on the boundary of \(\Omega\), (PSD) implies that the only functions that lie in the kernel of the Laplacian (\(\Delta u = 0\)) are those functions that vanish on the entire domain. Moreover, properties (Sym) and (PSD) imply that the Laplacian can be diagonalized and its eigenvalues are nonnegative,

```
\(\Delta u = \lambda u \Rightarrow \lambda \ge 0.\)
```

Another prominent property of smooth Laplacians is the _maximum principle_. Let \(u: \Omega \to \mathbb{R}\) be _harmonic_; that is, \(\Delta u = 0\). The maximum principle asserts that

```
(MAX) \(u\) is harmonic \(\Rightarrow u\) has no strict local maximum in \(\Omega\),
```

where we no longer assume that \(u\) vanishes on the boundary of \(\Omega\). Likewise, no harmonic function can have a local minimum in \(\Omega\).

The maximum principle can be derived from another important property of harmonic functions, the _mean value property_. Consider a point \(\boldsymbol{x} \in \Omega\) and a closed ball \( B(\boldsymbol{x}, r) \) of radius \( r \) centered at \( \boldsymbol{x} \) that is entirely contained in \( \Omega \). Every harmonic function has the property that the value \( u(\boldsymbol{x}) \) can be recovered from the average of the values of \( u \) in the ball \( B(\boldsymbol{x}, r) \):

\( u(\boldsymbol{x}) = \frac{1}{\text{vol}(B(\boldsymbol{x}, r))} \int_{B(\boldsymbol{x}, r)} u(\boldsymbol{y}) d\boldsymbol{y}.\)

A simple argument by contradiction shows that the mean value property implies property (MAX).

The properties mentioned so far play an important role in applications; specifically, in the context of barycentric coordinates, they give rise to mean value coordinates (see Section 1.2.3) and harmonic coordinates (see Section 1.2.8). Below we discuss additional properties of Laplacians. For further reading we refer to the books [43, 140, 333] and the lecture notes [83, 109].

### 5.2 LAPLACIANS ON RIEMANNIAN MANIFOLDS

The standard Laplacian in \( \mathbb{R}^n \) can be expressed as

\( \Delta u = -\text{div } \nabla u,\)

where div is the usual divergence operator acting on vector fields in \( \mathbb{R}^n \). Written in integral form, the negative divergence operator is the (formal) adjoint of the gradient: if \( X \) is a vector field and \( u: \Omega \to \mathbb{R} \) is a function that vanishes on the boundary of \( \Omega \), then

\( \int_\Omega \nabla u \cdot X = \int_\Omega u (-\text{div } X).\)

This perspective can be generalized to Riemannian manifolds, which incorporate the notion of curvature. The Laplacian plays an important role in the study of these curved spaces.

### 5.2.1 Exterior calculus

Although gradient and divergence can readily be defined on Riemannian manifolds, it is more convenient to work with the differential (or exterior derivative) \( d \) instead of the gradient and with the codifferential \( d^* \) instead of divergence.

The differential \( d \) is similar to (but not the same as) the gradient. Indeed, given a function \( u: \Omega \to \mathbb{R} \), one has

\( du(X) = \nabla u \cdot X\)

for every vector field \( X \). In particular, the differential does not require the notion of a metric, whereas the gradient does. The codifferential \( d^* \) is defined as the formal adjoint to \( d \), in the same way as divergence is the adjoint of the gradient. In contrast to the divergence operator, which acts on vector fields, the codifferential \( d^* \) acts on 1-forms. A 1-form is a covector at every point of \( \Omega \); that is, if \( X \) is a vector field on \(\Omega\) and \(\alpha\) is a 1-form, then \(\alpha(X)\) is a real-valued function on \(\Omega\). In order to define the codifferential \(d^*\), consider a 1-form \(\alpha\) and a function \(u: \Omega \to \mathbb{R}\) that vanishes on the boundary of \(\Omega\). Then

\(\int_\Omega du \cdot \alpha = \int_\Omega u d^* \alpha,\)

where the dot product is the inner product between covectors induced from the inner product between vectors. Notice that different from the differential \(d\), the codifferential \(d\) does require the notion of a metric. The Laplacian of a function \(u\) can be expressed as

\(\Delta u = d^* du,\)

which is equivalent to the representation \(\Delta u = -\text{div}\nabla u\) given above.

In order to carry over this framework to manifolds, let \(M\) be a smooth orientable manifold with smooth Riemannian metric \(g\). Suppose for simplicity that \(M\) is compact and has an empty boundary. The Riemannian metric induces a pointwise inner product between tangent vectors on \(M\), which, analogously to the above discussion, induces an inner product between 1-forms. More generally, one works with \(k\)-forms for \(k \ge 0\). A 0-form, by convention, is a real-valued function on \(M\). A 1-form can be thought of as an oriented 1-volume in the sense that applying a 1-form to a vector field returns a real value at every point. Likewise, a \(k\)-form for \(k > 1\) can be thought of as an oriented \(k\)-volume in the sense of returning a real number at every point when applied to an ordered \(k\)-tuple (parallelepiped) of tangent vectors. As a consequence, \(k\)-forms can be integrated over (sub)manifolds of dimension \(k\). In the sequel we let \(\Lambda^k\) denote the linear space of \(k\)-forms on \(M\).

Analogous to the \(L^2\) inner product between functions on \(\mathbb{R}^n\), let

\((\alpha, \beta)_k = \int_M g(\alpha, \beta) \text{vol}_g\)

denote the \(L^2\) inner product between \(k\)-forms \(\alpha\) and \(\beta\) on \(M\), where, by slight abuse of notation, we let \(g(\alpha, \beta)\) denote the (pointwise) inner product induced by the Riemannian metric.

The differential \(d: \Lambda^k \to \Lambda^{k+1}\) maps \(k\)-forms to \((k+1)\)-forms for \(0 \le k \le \dim M\), where one sets \(d\alpha = 0\) for any \(k\)-form with \(k = \dim M\). One can define the differential acting on \(k\)-forms by postulating Stokes's theorem,

\(\int_U d\alpha = \int_{\partial U} \alpha,\)

for every \(k\)-form \(\alpha\) and every sufficiently smooth submanifold \(U \subset M\) of dimension \((k+1)\) with boundary \(\partial U\). If one asserts this equality as the defining property of the differential \(d\), then it immediately follows that \(d \circ d = 0\) since the boundary of a boundary of a manifold is empty (\(\partial(\partial U) = \emptyset\)).

The codifferential \(d^*\), taking \((k+1)\)-forms back to \(k\)-forms, is the (formal) adjoint of \(d\) with respect to the \(L^2\) inner products on \(k\)- and \((k+1)\)-forms. It is defined by requiring that

\((d\alpha, \beta)_{k+1} = (\alpha, d^*\beta)_k\)
