
![](img/5f95dd954ac63cc68119f6f48ca99e18_269_0.png)

Figure 10.22 A boundary with only nine points. The points may be listed as ordered pairs, using Cartesian (x, y), or polar (ρ, θ). If the sample points are equally spaced in arc length (they are not, in this drawing), following the idea of “go one step (of distance 1.0), turn through angle θi, and continue”. Following this convention, the list of coordinates is simply a list of the turning angles, scalars.

As discussed in section 10.2, rotation in 2D is accomplished by multiplying each point by a rotation matrix,

```
\(\begin{bmatrix} x'(s) \\ y'(s) \end{bmatrix} = \begin{bmatrix} \cos \theta & -\sin \theta \\ \sin \theta & \cos \theta \end{bmatrix} \begin{bmatrix} x(s) \\ y(s) \end{bmatrix}\)
```

Rotation matrices like this have the property that their columns are orthonormal vectors, and they are referred to as “orthonormal transformations”. We refer to the collection of such rotations as the “Special Orthogonal group,” SO(n), where n refers to the dimension of the operator. In the cases described in this section, we consider n = 2.

There is another group of possible operations that can be applied to a boundary without changing the shape. This involves moving the starting point and is called the “re-parameterization group,” D. The re-parameterization group also includes the possibility that the parameter may vary in its speed as it moves around the curve, but we are going to ignore that possibility here.

Now we have, for any single shape, an infinity of possible versions, all of which are in some sense equivalent. Since we are using the concept of vectors to represent each shape, and since the conditions of section 3.2.2 are easily shown to be true, we have defined a vector space.

## 10.7.3 Vector Spaces

Remember from section 3.2.2 that a vector space is a collection of vectors that satisfy the requirement that if two vectors are members of the same space, their sum is likewise in the same collection. Furthermore, if ω is a scalar, and V an element of the collection of vectors, then ωV is also a member of the collection. To be really complete in the definition,
![](img/5f95dd954ac63cc68119f6f48ca99e18_270_0.png)

Figure 10.23 A triangle drawn on a sphere does not have 180 degrees, so a sphere is not globally Euclidean, but it is locally Euclidean. Figure from https://en.wikipedia.org/wiki/Spherical_geometry.

we have to specify the properties of vector addition (associative, distributive, etc.), but let's not bother with that right now.

Since we can write shape as a vector, and we can add and multiply those vectors to produce new vectors that we can interpret as shapes, a single shape is an element of a vector space.

There are two special vector spaces that are important here: The first is the space of all square-integrable functions, L^2, that is, all functions f such that ∫ f^2(t)dt < ∞. The second is the space of all possible closed shapes, that we will call C. In a later section, we will present the properties that define C.

## 10.7.4 Manifolds

The special space, C defined above, has the property that it is locally Euclidean. To see what this means, think about the surface of a sphere. The sum of the interior angles of a triangle does not equal 180 degrees when the triangle is drawn on a sphere (see Figure 10.23). Yet, if the sphere is big enough, or the triangle small enough, the difference between the sum of the interior angles and 180 degrees becomes vanishingly small. Furthermore, the process through which it becomes vanishingly small is smooth. A sphere thus has a "locally Euclidean" geometry. Any surface with such a property is called a "manifold." We thus refer to C as the manifold of possible closed curves, and will not attempt to prove the Euclidean nature of the manifold here.

In the example of surface of the earth, the manifold is a 2-manifold, that is, any point is uniquely identified by two parameters, longitude and latitude. Furthermore, there are an infinite number of points in that manifold. It is continuous and differentiable. With just two parameters, we have no way to talk about points that are inside the earth, but when it becomes necessary to use such terminology, we talk about a manifold "embedded in" a higher dimensional space. For example, we think of the surface of the earth as embedded in a 3-space.

A manifold is merely a set of points with some continuity constraints. Most of the time, we think of it as a continuous surface, but it is really no big deal.

It will often be convenient to use terminology describing the manifold as a surface, so you will see terms like “on the manifold.”

Recall in section 8.4.2, we talked about equivalence relations? Here, we define a different equivalence relation as follows: two vectors v1 and v2 are equivalent if they both represent the same shape, independent of rotation and parameterization. With this definition, C is partitioned into equivalence classes, one for each distinct shape. Since there are an infinite number of possible 2D closed shapes with a particular perimeter, the number of equivalence classes is still infinite. All of the different elements of C corresponding to a particular shape (that is, all the elements of one particular equivalence class) defines an orbit. You may also see the set of equivalence classes referred to as the “quotient set.”

Let I denote the interval I = [0, 2π], and let β : I -> R^2 be a curve in the plane. Then, if s ∈ I is arc length we could describe curves not only in terms of their coordinates, but in terms of their directions, θ(s) as described above, or by their velocity vectors,

```
q(s) = \frac{\dot{\beta}(s)}{\sqrt{||\dot{\beta}(s)||}} (10.85)
```

We observe that this function, evaluated at any particular s, is tangent to β. Furthermore, \frac{\dot{\beta}(s)}{||\dot{\beta}(s)||} is the unit tangent vector at s.

## 10.7.5 Projecting onto the Manifold of Closed Curves

In this subsection, an illustration of the philosophy, the approach presented in [10.18] is followed. We will describe curves as continuous functions and also as very long vectors, and we will discuss (as we did earlier) how to go back and forth between the representations.

Two ways present themselves for representing curves.

- **In a function space** A single function, θ(s), where s is the usual arc length and θ is the angle the tangent to the curve makes with the x axis.

- **In a discrete vector space** A curve is a list of all the points around the curve. In this discrete form, s is uniformly sampled, and so θ(s) denotes the operation of traveling a distance Δs in the direction θ. Now instead of a continuous function, the curve is a high-dimensionality (e.g., 256 elements, not infinity) vector.

When thinking of a curve as a function, we denote the curve by θ(s), where θ is the direction of the tangent at point s.

When thinking of a curve as a vector, we denote it by a boldface symbol, such as θ. Since these vectors have an infinite number of elements (until we quantify them), the two representations are really the same.

We begin by using the continuous form.

We ask that you take the following three equations on faith until you take another math course. Any curve, \(\theta(s)\) must satisfy the following three equations if the curve is closed:

```
\(\Phi_1(\theta) \equiv \frac{1}{2\pi} \int_0^{2\pi} \theta(s) ds = \pi\)

\(\Phi_2(\theta) \equiv \int_0^{2\pi} \sin \theta(s) ds = 0\)

\(\Phi_3(\theta) \equiv \int_0^{2\pi} \cos \theta(s) ds = 0.\)

(10.86)
```

We begin to think now of the set of closed curves in the plane as being a manifold, and begin to use the term “manifold” where we really mean the manifold of closed curves in the plane.

Suppose we have two closed curves \(\alpha(s)\) and \(b(s)\). If we think of them as vectors, then by definition they lie on the manifold. Each of those curves consists of an infinite number of points, and we can still think of it as an ordered list of scalars, a vector. A straight line could be drawn between any two such points. Question: is every intermediate point also a closed curve? To find points on a straight line between two points¹ is pretty easy, as follows:

Call the first vector \(A\) and the second vector \(B\). Assuming \(s\) was fairly finely sampled, these vectors could have dimensions around a thousand or so. The point

```
\(C = \alpha A + (1 - \alpha) B\)

(10.87)
```

is a point on the straight line (a Euclidean straight line) between \(A\) and \(B\) if \(0 \le \alpha \le 1\). So just let \(\alpha\) range from 0 to 1 and you will generate intermediate vectors that lie on the straight line between \(A\) and \(B\). The lower set of curves in Figure 10.24 illustrates this, and clearly, the intermediate points are not closed curves. Given one of these intermediate points, say \(\theta\), we need to find the projection of that point onto the manifold. Here, “projection” will simply mean finding the point on the manifold closest to the point of interest. We approach this by finding a small step in the direction of the manifold. Let that step be named \(h(s)\), and we add it to \(\theta(s)\) at each value of \(s\).

```
\(\Phi_1(\theta + h) = \frac{1}{2\pi} \int_0^{2\pi} (\theta(s) + h(s)) ds = \Phi_1 + \frac{1}{2\pi} \int_0^{2\pi} h(s) ds\) (10.88)

\(\Phi_2(\theta + h) = \int_0^{2\pi} (\cos(\theta(s) + h(s)) ds\) (10.89)

\(\Phi_3(\theta + h) = \int_0^{2\pi} (\sin(\theta(s) + h(s)) ds.\) (10.90)
```

¹ Since a vector of dimension \(d\) represents a single point in a \(d\)-dimensional space, we use the words vector and point interchangeably here.
