
which shows to reflect a vector x through a vector a, by the transform \(x \to axa^{-1}\). This is a useful formula, since it works in any dimension, and is the basis for rotation formulas that are dimension-independent.

![](img/672fe9a2d008ba627b1991e15d70f43e_252_0.png)

FIGURE 2.1.5 Reflection has a simple GA notation.

By reflecting twice over vectors a and b with an angle \(\theta/2\) between them, we can rotate the objects encoded in multivectors by an angle \(\theta\). The object \(R = ab\) is called a rotor, and performs rotation on any multivector X in any dimension, by the transformation \(X \to RXR^{-1}\). They are more efficient to compose than matrices and are numerically more stable. And they rotate multivectors, not just vectors (see the examples that follow). In 3D, expanding a rotor in terms of basis elements shows it is just a quaternion, as we would expect.

There are several equivalent ways to construct a rotor. It is useful to take a and b to be unit vectors, since \(R^{-1} = ba\) is easy to compute. In 3D, a way to construct a rotor that rotates by \(\theta\) around an axis c is to take \(R = \cos(\theta/2) - \sin(\theta/2)Ic\). With these different and concise formulas to construct rotations, GA provides a simpler way to work out computations. And in any dimension, composition of rotors is computed with the geometric product. It's even possible to do calculus on rotors to give velocities, accelerations, interpolations, minimizing paths, camera orientation, etc., but this will require more gems. As in all mathematics, this goes much deeper than there is space to present completely. Another advantage is that the rotor also keeps track of the direction of rotation, unlike a scalar-valued angle or rotation matrix, allowing subdivision and interpolation of rotations. In three dimensions, rotor interpolation is the usual SLERP, as shown in Equation 2.1.13

```
R(\lambda) = \frac{\sin((1-\lambda)\theta)R_1 + \sin(\lambda\theta)R_2}{\sin \theta}.
(2.1.13)
```

This simplifies for the midpoint between two rotations:

```
R(1/2) = \frac{\sin(\theta/2)}{\sin\theta}(R_1 + R_2).
```

## Linear Algebra Connection

Given a linear transformation \( f: V^n \to V^m \) (a matrix multiplication, for example), \( f \) acts naturally on \( k \)-blades as \( f(\alpha) = \alpha \). We add the rule on scalars \( f(\alpha) = \alpha \) and extend linearly to get a transform \( f: CV \to CV \) defined for any multivector in the geometric algebra. This extension plays nicely with our notions of geometry. For example, a linear transform moves lines to lines, planes to planes, etc. To see a linear transform move a line to another line, we apply \( f \) to both sides of the general line equation \( (\mathbf{x} - \mathbf{a}) \wedge \mathbf{u} = 0 \), resulting in Equation 2.1.14

```
f((\mathbf{x} - \mathbf{a}) \wedge \mathbf{u}) = f(0)
f((\mathbf{x} - \mathbf{a}) \wedge \mathbf{u}) = 0
(f(\mathbf{x}) - f(\mathbf{a})) \wedge f(\mathbf{u}) = 0
(\mathbf{x}' - \mathbf{a}') \wedge \mathbf{u}' = 0.
```

## The Dictionary

Before we show how GA can simplify the derivation of equations, we first list some common geometric relations and how these relations translate into GA. There is not space in this gem to derive and explain each one, so we merely list facts and simplifying computational rules that can be applied.

- 1. The geometric product is the most fundamental product; the others can be written in terms of it\(^2\). For example, consider Equation 2.1.15

```
\mathbf{a} \wedge \mathbf{b} = \frac{1}{2}(\mathbf{ab} - \mathbf{ba})
\mathbf{a} \cdot \mathbf{b} = \frac{1}{2}(\mathbf{ab} + \mathbf{ba})
\mathbf{a} \times \mathbf{b} = (\mathbf{a} \wedge \mathbf{b}) \mathbf{I}_3 = -\mathbf{I}_3(\mathbf{a} \wedge \mathbf{b}) = -(\mathbf{a} \wedge \mathbf{b}) \mathbf{I}_3
\mathbf{a} \lrcorner \mathbf{b} = (\mathbf{ab})_0.
```

- 2. The usual 3D cross product is \(\mathbf{a} \times \mathbf{b} = (\mathbf{a} \wedge \mathbf{b}) \mathbf{I}_3 = -\mathbf{I}_3(\mathbf{a} \wedge \mathbf{b}) = -(\mathbf{a} \wedge \mathbf{b}) \mathbf{I}_3\). This is easy to verify by choosing an orthonormal basis for the span of \(\mathbf{a} \wedge \mathbf{b}\), extending it to a 3D basis, and evaluating each expression.

- 3. Vectors are perpendicular if and only if the dot product is 0. This extends to the contraction product applied to k-blades!

- 4. Linear (in)dependence: the outer product of vectors is 0 if and only if the vectors are linearly dependent. Thus two vectors are parallel if and only if their outer product is 0. This allows simple line and plane equations.

- 5. The equation of a line through a point a and with direction u is \((x - a) \wedge u = 0\). This works in any dimension, so it is more concise than the dimension-dependent forms.

- 6. Similarly, a plane through a point a and parallel to the bivector \(u \wedge v\) is \((x - a) \wedge u \wedge v = 0\). Again, this is dimension-independent.

- 7. The orthogonal projection of a blade A onto a blade B is given by \(P_B(A) = (A \cdot B) B^{-1}\). This is nice since it is the same expression for any two spaces: points onto lines, lines onto planes, planes onto planes, etc., in any dimension.

- 8. Extending the projection, the expression \(A - P_B(A)\) must represent the perpendicular component of A with respect to B.

- 9. The pseudoscalar I commutes with all elements in odd-dimensional spaces.

- 10. Given a vector n, a plane perpendicular to it in 3-space is -nI, and given a plane defined by \(u \wedge v\), the normal vector is \(-(u \wedge v) I\). This is shown in Figure 2.1.6. Recall this plane has an orientation, so we include the minus signs to make this agree with the "dual."

![](img/672fe9a2d008ba627b1991e15d70f43e_254_0.png)

FIGURE 2.1.6 In 3D, perpendicular vectors are "dual" to plane elements.

- 11. Duality: the dual of a multivector A is defined by A* = A J. This is useful for exchanging "spanning" relations and "perpendicularity" relations. This generalizes the previous fact. In 3D, this exchanges bivectors with normal direction vectors, so it can be used to quickly find the normal to a plane. This is shown in 3D for a normal and plane in Figure 2.1.6.

- 12. The norm of a multivector generalizes the length of a vector and is written \(|A| = \sqrt{A \cdot A}\). It returns the area of a bivector, the length of a vector, etc.

- 13. Given two versors A and B, each defines a subspace of V; the intersection of these subspaces is called their meet and is denoted by M = A ∩ B. It can be computed via \(A \cap B = A' \rfloor B = (A \rfloor J) \rfloor B\). The dual concept is the join, which is the smallest subspace of V containing the two subspaces, written as \(J = A \cup B\). For example, the meet of two nonparallel planes in 3D is the line of their intersection, as shown in Figure 2.1.7. The meet of two versors can be thought of as the greatest common divisor of the defining vectors, and the join as the least common multiple. Knowing one allows easy computation of the other via the relations shown in Equation 2.1.16.

```
J = A \wedge (M^{-1} \rfloor B)
M = (B \rfloor J^{-1}) \rfloor A
(2.1.16)
```

![](img/672fe9a2d008ba627b1991e15d70f43e_255_0.png)

## Examples

In this section, we present several example computations that show GA in action. The point of this gem is to show that GA simplifies hand derivations and reduces code complexity. So when working through these examples, the reader should consider the coding complexity involved for each of two geometry engines: one with basic linear algebra routines and one supporting the geometric product. In each case, these derivations are short by hand and would only involve a few lines of code in the GA engine. However, the coding work for the linear algebra methods would involve quite a bit of code for most of the examples. Quod erat demonstrandum and touché, to mix languages!

- 1. Given vectors x and a, suppose we want to find the component \(x_\parallel\) of x that is perpendicular to the vector a, as illustrated in Figure 2.1.8. The perpendicular condition is \(x_\parallel \rfloor a = 0\), and magnitude conditions require another condition: the magnitude of the area spanned by a and x is the same as that by a and \(x_\perp\) (this just says the area of the parallelogram is base times height). Thus, \(x_\perp \wedge a = x \wedge a\). Adding these two equations gives the geometric product \(x_\perp \wedge a + x_\perp \cdot a = x \wedge a = a \wedge x + 0 = x \wedge a\), and this we can divide by x to get \(x_\perp = (x \wedge a) a^{-1}\). To see how this fits into standard linear algebra, we pick a basis such that a = ae, and \(x = b_\parallel e + b_\perp e_\perp\), plug in and expand, getting \(x_\perp = ((b_\parallel e + b_\perp e_\perp) \wedge ae) (e/a) = b_\perp e_\perp\) as we would expect.

![](img/672fe9a2d008ba627b1991e15d70f43e_256_0.png)

FIGURE 2.1.8 GA has a simple notation for decomposing objects into parallel and perpendicular components.

Now for the kicker. What if we want the vector component of x that is perpendicular to a plane given by a bivector A? We do the same math and obtain \(x_\perp = (x \wedge A) A^{-1}\). Elegant indeed! (Or we just project x to the normal \(-A_\perp\) of the plane, which is equivalent by duality).

- 2. Next, we reflect a point through a plane. In Figure 2.1.9, B is the side view of a plane, and a is a vector that we want to reflect through the plane. We do this with the reflection through a vector idea, getting a nice formula. Let n be the normal to the plane. From earlier, we know the reflection of a through n is just \(nan^{-1}\), and from Figure 2.1.8, the reflection of the point through the plane is \(-nan^{-1}\). To avoid making errors by believing nice pictures, note this formula still works with the "other" normal to the plane. Computing a concrete example is instructive. So given the point and plane, it is one line of code to project like this, and the equation works in any dimension as usual.

- 3. We demonstrate the meet of two blades by computing the intersection of two nonparallel planes through the origin, as shown in Figure 2.1.7. We take planes that we can easily visualize, and get the answer we expect, as shown in Equation 2.1.17.

*Actually, you need to know that for any vector x and bivector A, \(xA = x \cdot A + x \wedge A\) and \(x \cdot A = 0\) if and only if \(x \perp A\), both of which are easy to prove. The vector case inspires this.
