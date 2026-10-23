
## Chapter 15: Towards High-Order Finite Elements

In this chapter, we describe quadratic and cubic finite elements, which may be used to improve the accuracy of the finite-element discretization. We show that the present object-oriented framework indeed provides the required tools to implement these methods. In particular, the "polynomial" object, along with its multiplication and integration functions, is most helpful in assembling the required stiffness matrix.

### 15.1 High-Order vs. Linear Finite Elements

So far, we have used only linear finite elements. This means not only that the elements are triangles with straight sides but also that the function that approximates the solution of the original PDE is continuous in the entire mesh and linear in each particular triangle in it. Indeed, this function can be written as a linear combination of the nodal basis functions, which are continuous in the entire mesh and linear in each triangle. More specifically, the nodal basis function φi assumes the value 1 only at the ith node and vanishes at all the other nodes. Thus, φi vanishes in all the triangles that don’t use node i as a vertex. In triangles that do use it as a vertex, on the other hand, φi decreases linearly away from node i until it hits the edge that lies across from it, where it vanishes. As a result, φi is indeed continuous and piecewise linear throughout the mesh, as required. The numerical solution obtained from the discrete stiffness system is the best continuous piecewise-linear function in terms of minimizing the quadratic functional associated with the original boundary-value problem (Chapter 11, Section 3).

In many applications, however, this approximation is insufficient. In fact, the solution of the original PDE may have sharp variation inside individual triangles as well. This behavior cannot be approximated well by linear functions. Although one can use a large number of small triangles to approximate the solution better in such areas, this can lead to a considerable increase in the number of nodes and, hence, the number of unknowns in the discrete stiffness system. It may be better to improve the quality of the approximation within each particular triangle.

For this purpose, one may switch to finite elements of higher order. The elements still have the same triangular shape as before. However, the functions that form the approximate solution can now be not only linear but also quadratic or even cubic (or, in general, polynomials of degree k > 1 in x and y) in each particular triangle. The approximate solution is now the best continuous piecewise-quadratic (cubic) function in terms of minimizing the quadratic functional associated with the original boundary-value problem.

Clearly, piecewise-quadratic or cubic functions have a better chance of approximating well a solution with large variation. This extra accuracy, however, comes at the price of increasing the number of degrees of freedom in each particular triangle. In fact, a quadratic polynomial in x and y is characterized by six coefficients and a cubic polynomial by ten coefficients, whereas a linear function is characterized by three coefficients only. Because the number of degrees of freedom is larger than before, the order of the stiffness matrix is also larger and the system is more difficult to solve. Still, the extra cost involved in solving the stiffness system may well be worth it for the sake of better accuracy.

In what follows, we describe the discretization method in more detail.

### 15.2 Quadratic Finite Elements

The quadratic finite elements considered here have the same triangular shape as before. They are quadratic only in the sense that the function that is used to approximate the solution of the original PDE is quadratic in each finite element and continuous in the entire mesh. Indeed, this function is a linear combination of the quadratic nodal basis functions described below.

In linear finite elements, the nodal basis function φi assumes the value 1 at node i and the value 0 at all other nodes. Furthermore, it decreases linearly away from node i and vanishes at the edges that lie across from it in triangles that use it as a vertex. Actually, the nodal basis functions at a particular finite element can be defined in terms of three typical (standard) nodal functions, defined in the reference triangle in Figure 12.2, which is mapped to the finite element under consideration. Each typical nodal function is linear in the reference triangle and assumes the value 1 at one vertex and 0 at the other two vertices. The typical nodal functions are useful in assembling the stiffness system.

In order to have an even better approximation, the quadratic finite-element method uses continuous functions that are not only linear but also quadratic in each particular finite element. In other words, the solution to the original PDE is now approximated by a linear combination of not only linear but also quadratic nodal basis functions. In order to define the quadratic nodal basis functions, it is sufficient to define typical nodal functions in the reference triangle in Figure 15.1 and use the mapping of this triangle to the finite element under consideration.

In the reference triangle, a quadratic function (polynomial of degree 2 in the spatial variables x and y) is determined by the six coefficients of the terms 1, x, y, x², xy, and y² in it. This means that the function has six degrees of freedom in its definition and hence can also be defined uniquely by its values at six distinct points in the triangle, e.g., the three vertices (numbered 1,2,3) and three midpoints of edges (numbered 4,5,6) in Figure 15.1. In fact, a typical nodal function in the reference triangle assumes the value 1 at one of these points and vanishes at the other five.

which contains the six required nodes in Figure 15.1. The entire mesh is then implemented as a `mesh<quadraticTriangles>` object.

Assembling the stiffness matrix is done in a similar way as that in Chapter 13, Section 5. The only difference is that here the gradient of a typical quadratic nodal function is no longer constant but rather a polynomial of degree 1 in the spatial variables x and y. The implementation of such polynomials, including their multiplication and integration, is available in Chapter 5, Sections 13 and 14.

### 15.3 Cubic Finite Elements

The cubic finite elements considered here have the same triangular shape as before. They are cubic in the sense that the function that approximates the solution to the original PDE can be not only quadratic but also cubic within each particular finite element. In other words, it can be written in each finite element as a polynomial of degree 3 in the spatial variables x and y. Thus, it has 10 degrees of freedom in it: the coefficients of the terms 1, x, y, x², xy, y², x³, x²y, xy², and y³. Therefore, it is determined uniquely in each particular finite element in terms of its values at 10 distinct points in it.

This is also true for the typical cubic nodal functions defined in the reference triangle in Figure 15.2, which is mapped onto the finite element under consideration. Each typical nodal function assumes the value 1 at one of the ten nodes in Figure 15.2 and 0 at the other nine. More explicitly, the typical cubic nodal functions are defined as follows:

![](img/1f293b0ceb2de964310ea7f941a1b580_427_0.png)

Figure 15.2. The reference triangle in the cubic finite-element method. The nodes are numbered 1,2,3,4,5,6,7,8,9,10. A typical cubic nodal function assumes the value 1 at one of these nodes and 0 at the others.

φ^(1) ≡ (9/2) y (y − 1/3)(y − 2/3),
φ^(2) ≡ (9/2)(1 − x − y)(2/3 − x − y)(1/3 − x − y),
φ^(3) ≡ (9/2) x (x − 1/3)(x − 2/3),
φ^(4) ≡ (27/2) y (y − 1/3)(1 − x − y),
φ^(5) ≡ (27/2) x (1 − x − y)(2/3 − x − y),
φ^(6) ≡ (27/2) x y (x − 1/3),
φ^(7) ≡ (27/2) y (1 − x − y)(2/3 − x − y),
φ^(8) ≡ (27/2) x (x − 1/3)(1 − x − y),
φ^(9) ≡ (27/2) x y (y − 1/3),
φ^(10) ≡ 27 x y (1 − x − y).

Note that the typical cubic nodal functions indeed satisfy
φ^(i)(j) = { 1 if j = i, 0 if j ≠ i. }

where i and j are integers between 1 and 10. The typical cubic nodal functions are useful in assembling the stiffness matrix, as in Chapter 12, Section 5. The solution of the resulting stiffness system produces the required approximate solution to the original PDE. This completes the definition of the cubic finite-element discretization method.

The implementation of cubic finite elements is similar to that of linear ones in Chapter 13. The only difference is that the "triangle" object used there is replaced by the "cubicTriangle" object defined by

```
typedef finiteElement<point,10> cubicTriangle;
```

which contains the 10 required nodes in Figure 15.2. The entire mesh is then implemented as a `mesh<cubicTriangle>` object.

Assembling the stiffness matrix is done in a similar way as that in Chapter 13, Section 5. The only difference is that here the gradient of a typical cubic nodal function is no longer constant but rather a polynomial of degree 2 in the spatial variables x and y. The implementation of such polynomials, including their multiplication and integration, is available in Chapter 5, Sections 13 and 14.

### 15.4 Pros and Cons

In Table 15.1, we give a brief summary of the pros and cons of linear and high-order finite elements. The comparison assumes that the same number of degrees of freedom (unknowns) is used in both methods.

High-order finite elements provide extra accuracy, particularly inside individual finite elements and near the boundary. However, this comes at the price of a more complicated assembling procedure, which must use the "polynomial" object in Chapter 5, Section 13. Furthermore, the resulting stiffness matrix is denser than the one obtained from linear finite elements. There is, thus, a trade-off between extra accuracy and extra computational cost.

Actually, one could also have extra accuracy with linear finite elements by just increasing the number of nodes and triangles in the mesh. Although this approach also increases the
