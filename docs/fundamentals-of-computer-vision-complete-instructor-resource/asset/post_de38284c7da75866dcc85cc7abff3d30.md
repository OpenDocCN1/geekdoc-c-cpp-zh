
method presented here is applicable to a line in any number of dimensions, and does not fail when the best fitting line happens to be vertical.

Other methods for fitting straight lines also exist. For example, [10.26] describes piecewise representations that preserve moments up to an arbitrarily specified order. Fitting functions to data occurs in many contexts. For example, Gorman [10.28] has looked at fitting not only straight edges, but points, straight lines, and regions with straight edges. By so doing, sub-pixel precision can be obtained.

### 10.3.3 Groups

This section covers a bit more terminology of transformations, moving from linear transformations to more general types.

As we discuss a bit more about the theory of transformations, one particular transformation, rotation in the plane, will be used as an example, as its properties are easy to visualize. Recall from section 10.2 that a rotation of a point in 2-space may be easily computed by a 2 x 2 matrix. This collection of such 2 x 2 matrices that rotations is named SO(2), the special orthogonal group in two dimensions. The columns of these matrices, when considered as vectors, are orthogonal, and the determinant is 1.0.

A group, in mathematics, is a set of transformations that satisfy four properties:

**Identity** The transformation that takes any member of the set to itself must itself be in the set. In SO(2), the transformation \(\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}\) does this.

**Inverse** If a transform is in the set, its inverse must also be in the set. For example, if \(\begin{bmatrix} 0.866 & 0.5 \\ -0.5 & 0.866 \end{bmatrix}\) is in the set of transformations, then \(\begin{bmatrix} 0.866 & -0.5 \\ 0.5 & 0.866 \end{bmatrix}\) must also be in the set.

**Associative** Let A, B, and C be transformations in the set, and let D be the composition \(D = B \circ C\), and \(E = A \circ B\), where \(\circ\) here denotes matrix multiplication. Then the following relation must hold: \(A \circ D = E \circ C\).

Said another way, \(A \circ (B \circ C) = (A \circ B) \circ C\), that has the form of the familiar associative property. Here, since SO(2) is a linear group, the composition of transforms, \(\circ\), may be computed by simple matrix multiplication.

**Closure** If A and B are in the set, then \(A \circ B\) is in the group. For example if \(A = \begin{bmatrix} 0.866 & 0.5 \\ -0.5 & 0.866 \end{bmatrix}\) and \(B = \begin{bmatrix} 0.9397 & -0.3420 \\ 0.3420 & 0.9397 \end{bmatrix}\), then \(A \circ B = \begin{bmatrix} 0.9848 & 0.1737 \\ -0.1737 & 0.9848 \end{bmatrix}\), and \(A \circ B\) is also an element of the group.

## 10.4 Features of Regions

In this section, we introduce some important features used to describe a region. We start from some simple properties of a region like perimeter, diameter, and thinness. We then extend the discussion to some invariant features like moments, chain codes, Fourier descriptors, and the medial axis.

![](img/5f95dd954ac63cc68119f6f48ca99e18_246_0.png)

Figure 10.7 Results of applying two different compactness measures to various regions. Since a circle has the minimum perimeter for a given area, it minimizes \( T_a \). A starfish on the other hand, has a large perimeter for the same area.

### 10.4.1 Simple Features

In this section, we describe several simple features that can be used to describe the shape of a patch – the output of the segmentation process. Many of these features can be computed as part of the segmentation process itself. For example, since the connected component labeling program must touch every pixel in the region, it can easily keep track of the area. Following is a list of simple features that are likewise simple to calculate.

- **Average gray value** In the case of black and white “silhouette” pictures, this is simple to compute.
- **Maximum gray value** This is straightforward to compute.
- **Minimum gray value** This is straightforward to compute.
- **Area (A)** A count of all pixels in the region.
- **Perimeter (P)** Several different definitions exist. Probably the simplest is a count of all pixels in the region that are adjacent to a pixel not in the region.
- **Diameter (D)** The diameter is the length of a maximum chord; the distance between those two points in the region whose mutual distance is maximum [10.33, 10.35].
- **Thinness (also called Compactness” (T)** Two definitions for compactness exist: \( T_a = \frac{P^2}{A} \) measures the ratio of the squared perimeter to the area; \( T_b = \frac{D^2}{A} \) measures the ratio of the diameter to the area. Figure 10.7 compares these two measurements on example regions.
- **Center of gravity (CG)** The center of gravity may be determined by

\(\hat{\mathbf{x}} = \frac{1}{N} \sum_{i=1}^N \mathbf{x}_i\) (10.48)

for all \( N \) points in a region.

3 Some authors [10.34] prefer not to confuse the mathematical definition of compactness with this definition, and thus refer to this measure as the isoperimetric measure.

![](img/5f95dd954ac63cc68119f6f48ca99e18_247_0.png)

- **X-Y aspect ratio** See Figure 10.8. The aspect ratio is the length/width ratio of the bounding rectangle of the region. This is simple to compute.
- **Minimum aspect ratio** See Figure 10.8. This is again, a length/width ratio, but much more computation is required to find the minimum such rectangle, also called a bounding box. The minimum aspect ratio can be a difficult calculation, since it requires a search for extremal points.

A very good approximation to the minimum aspect ratio can usually be obtained if we think of a region as represented by an ellipse-shaped distribution of points. In this case, as we showed in Figure 10.5, the eigenvalues of the covariance of points are measures of the distribution of points along the major and minor orthogonal axes. The ratio of those eigenvalues is quite a good approximation of the minimum aspect ratio. Furthermore the eigenvectors of the covariance are invariant to rotation and translation, and robust against noise.

- **Number of holes** One feature that is very descriptive and reasonably easy to compute is the number of holes in a region. Connected components will yield an answer with minimal effort.

- **Triangle similarity** Consider three points on the boundary of a region, P1, P2, and P3, let d(P1, P2) denote the Euclidean distance between two of those points, and let S = d(P1, P2) + d(P2, P3) + d(P3, P1) be the perimeter of that triangle. The 2-vector

\(\begin{bmatrix} d(P_1, P_2) \\ d(P_2, P_3) \end{bmatrix} / S\) (10.49)

is simply the ratio of side lengths to perimeter. It is invariant to rotation, translation, and scale change [10.7].

- **Symmetry** In two dimensions, a region is said to be “mirror-symmetric” if it is invariant under reflection about some line. That line is referred to as the axis of symmetry. A region is said to have rotational-symmetry of order n if it is invariant under rotation of about some 2π/n point, usually of center of gravity of the region. There are two challenges in determining the symmetry of regions. The first is simply determining the axis. The other is to answer the question “how symmetric is it?” Most papers prior to 1995 that analyzed symmetry of regions in Computer Vision applications treated symmetry as a predicate: either the region is symmetric or it is not. Zabr sky et al.

![](img/5f95dd954ac63cc68119f6f48ca99e18_248_0.png)

Figure 10.9 Convex hull of a region. The shaded area is the convex discrepancy.

[10.19, 10.43] present a measure called the symmetry distance that quantifies *how* symmetric a region is.

- **The Convex Discrepancy** If one were to stretch a rubber band around a given region, the region that would result would be the convex hull (Figure 10.9). The difference in area between a region and its convex hull is the convex discrepancy. See Shamos [10.33] for fast algorithms for computing the convex hull, and [10.14] for such algorithms for parallel machines.

If we are fortunate enough to have a convex region to analyze, we can find the diameter in $O(n \log n)$ time, by finding the convex hull first. Furthermore, finding the convex hull provides us with another simple feature, the convex discrepancy, as illustrated in Figure 10.9.

### 10.4.2 Moments

The moments of a shape are easily calculated, and as we shall see, can be made robust to similarity transforms. A moment of order $p + q$ may be defined on a region as

$m_{pq} = \int x^p y^q f(x,y) dx dy$ (10.50)

where the integral is over the entire region, not just the boundary. If the function $f$ is 1 inside the region and 0 outside, the area of the region is then $m_{00}$, and we find that the center of gravity is

$m_x = \frac{m_{10}}{m_{00}}, m_y = \frac{m_{01}}{m_{00}}$. (10.51)

### Invariance to Translation

Although the results of Eqs. 10.50 and 10.51 are totally dependent on the coordinate system in which the measurements are made, it is possible to derive a set of moment-like measurements that are invariant to translation to the center of gravity.

$\mu_{pq} = \int (x - m_x)^p (y - m_y)^q f(x,y) dx dy$. (10.52)

These are called the *central moments*.

Since the central moments are calculated relative to the center of the region, the central moments are obviously invariant to translation.
