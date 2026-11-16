

![](img/672fe9a2d008ba627b1991e15d70f43e_257_0.png)

```
$(e_1 \wedge e_3) \cap (e_2 \wedge e_3) = (e_1 \wedge e_3) \lrcorner (e_2 \wedge e_3)$
$= ((e_1 \wedge e_3) \lrcorner I) \lrcorner (e_2 \wedge e_3)$
$= \langle e_1 e_3 e_1 e_2 e_3 \rangle_{3-2} \lrcorner (e_2 \wedge e_3)$
$= \langle -e_2 e_3 e_1 \rangle_{3-2}$
$= -e_3$
(2.1.17)
```

- 4. We prove a theorem of Euler stating that the product of two rotations is another rotation by obtaining a concrete formula for the resulting rotation. We view a quaternion in the normal way as a scalar \(\beta_0\) plus an axis of rotation \(\mathbf{q} = \beta e_i + \beta e_j + \beta e_k\), written \(\beta_0 + \mathbf{q}\). Assume that any single rotation can be represented as a quaternion. Recalling the pseudoscalar \(\mathbf{I} = e_1 \wedge e_2 \wedge e_3\) and using the previous definitions, we rewrite this quaternion representation with the GA version using the transformation \(\beta_0 + \mathbf{q} \rightarrow \beta_0 - \mathbf{Iq}\). Now multiply two quaternions, and one can easily read from Equation 2.1.18 both the scalar and the vector defining the resulting quaternion. This proves the theorem of Euler and also obtains a concrete answer for the resulting scalar and vector. Computing this relation is messy and ad hoc using usual quaternions but is straightforward using geometric algebra.

*We assume any rotation can be represented by a quaternion. I have a proof, but it won't fit in this margin.*

```
$(p_0 + \mathbf{p})(q_0 + \mathbf{q}) \to (p_0 - \mathbf{I}\mathbf{p})(q_0 - \mathbf{I}\mathbf{q})$
$= p_0 q_0 - p_0 \mathbf{I}\mathbf{q} - q_0 \mathbf{I}\mathbf{p} + \mathbf{I}\mathbf{p} \mathbf{I}\mathbf{q}$
$= p_0 q_0 - \mathbf{p}\mathbf{q} - \mathbf{I}\mathbf{q} \cdot q_0 - \mathbf{I}\mathbf{p} \cdot \mathbf{p}$
$= p_0 q_0 - \mathbf{p} \cdot \mathbf{q} - \mathbf{p} \wedge \mathbf{q} - p_0 \mathbf{I}\mathbf{q} - q_0 \mathbf{I}\mathbf{p}$
$= p_0 q_0 - \mathbf{p} \cdot \mathbf{q} - \mathbf{I} (p_0 \mathbf{q} + q_0 \mathbf{p} + \mathbf{q} \times \mathbf{p})$
$\to (p_0 q_0 - \mathbf{p} \cdot \mathbf{q}) + (p_0 \mathbf{q} + q_0 \mathbf{p} + \mathbf{q} \times \mathbf{p})$ (2.1.18)
```

- 5. A concrete rotation example is in order: the composition of rotation by $\pi/2$ around $\mathbf{e}_1$ preceded by a rotation of $\pi/2$ around $\mathbf{e}_2$ results in a $2\pi/3$ rotation around the vector $(\mathbf{e}_1 + \mathbf{e}_2 + \mathbf{e}_3)/\sqrt{3}$. The calculation uses the quaternion representation from the previous example. Recall that we divide angles by 2. The proof is provided in Equation 2.1.19.

  \(\left( \cos \frac{\pi}{4} + \mathbf{e}_1 \sin \frac{\pi}{4} \right) \left( \cos \frac{\pi}{4} + \mathbf{e}_2 \sin \frac{\pi}{4} \right) \to \frac{1}{\sqrt{2}}(1+\mathbf{e}_{32}) \frac{1}{\sqrt{2}}(1+\mathbf{e}_{13})\)
  \(= \frac{1}{2}(1+\mathbf{e}_{13}+\mathbf{e}_{32}+\mathbf{e}_{21})\)
  \(= \frac{1}{2} - \frac{\sqrt{3}}{2} \mathbf{I} \frac{(\mathbf{e}_1 + \mathbf{e}_2 + \mathbf{e}_3)}{\sqrt{3}}\)
  \(\to \cos \frac{\pi}{3} + \frac{(\mathbf{e}_1 + \mathbf{e}_2 + \mathbf{e}_3)}{\sqrt{3}} \sin \frac{\pi}{3}\) (2.1.19)

- 6. An example of the rotation of an entire multivector at once is given by rotating the plane defined by the bivector $\mathbf{B} = \mathbf{e}_1 \wedge \mathbf{e}_2$ by 60 degrees around the vector $\mathbf{a} = \mathbf{e}_1 + \mathbf{e}_3$. There is no need to decompose the plane into component vectors first. We start with the normalized rotor $\mathbf{R} = \cos(\pi/6) - \mathbf{I}\mathbf{a}/(\sqrt{2}) \sin(\pi/6)$. Then the rotated plane is as shown in Equation 2.1.20

  \(\mathbf{R}\mathbf{B}\mathbf{R}^{-1} = \left( \cos \frac{\pi}{6} - \frac{\mathbf{e}_{23} - \mathbf{e}_{13}}{\sqrt{2}} \sin \frac{\pi}{6} \right) (\mathbf{e}_1 \wedge \mathbf{e}_2) \left( \cos \frac{\pi}{6} + \frac{\mathbf{e}_{23} - \mathbf{e}_{13}}{\sqrt{2}} \sin \frac{\pi}{6} \right)\)
  \(= \frac{1}{2} \mathbf{e}_{12} + \frac{\sqrt{6}}{4} (\mathbf{e}_{13} + \mathbf{e}_{23}).\) (2.1.20)

*And this avoids the problem of applying a rotation to a plane and having to recompute the normal. Recall that the normal of a rotated plane is not the rotated normal of the plane! Usually a plane is defined by a point and normal, and rotating the plane requires getting two linearly independent vectors orthogonal to the normal, rotating these two vectors, computing a new normal, and obtaining a new point.*

- 7. Given vectors a, b, and c in the plane, we can find a vector x so that “a is to b as c is to x” as illustrated in Figure 2.1.10. If we were real numbers, we would solve x · c = b : a. GA behaves the same since we can now divide vectors by multiplying the ratios by c to obtain the answer x = ba⁻¹c.

![](img/672fe9a2d008ba627b1991e15d70f43e_259_0.png)

- 8. Again in the plane, we find the distance from a line with equation (x − a) ∧ u = 0 to the origin, shown in Figure 2.1.11. We find the vector d perpendicular to the line and passing through the origin, whose length is the distance. The same reasoning using the normal condition and area condition used in Example 2.1.1 gives d = (a ∧ u)u⁻¹, which gives the distance |d|. Does this work for the distance from a plane to the origin?

- 9. To show an example of the projection formula, we project the vector a = α₁e₁ + α₂e₂ + α₃e₃ onto the plane B = e₁ ∧ e₂, where we have picked the plane so we can easily verify the answer. Since the plane is in a nice orientation, we know the answer should be α₁e₁ + α₂e₂. Computation verifies this, as shown in Equation 2.1.21.

```
P_B(a) = (a · B)B⁻¹
= ⟨(α₁e₁ + α₂e₂ + α₃e₃)(e₁₂)⟩₂(e₂₁)
= (α₁e₂ − α₂e₁)(e₂₁)
= α₁e₁ + α₂e₂
(2.1.21)
```

- 10. We find a general formula for the intersection of two lines in the plane (which is just Cramer’s Rule, except we derive it completely intuitively and geometrically). See Figure 2.1.12; this is hard to see the first time around.

### FIGURE 2.1.11 Computing distance from a point to a line is simple.

We can write two given lines \((\mathbf{x}-\mathbf{a})\wedge\mathbf{u}=0\) and \((\mathbf{x}-\mathbf{b})\wedge\mathbf{v}=0\) in expanded form as \(\mathbf{x}\wedge\mathbf{u}=\mathbf{a}\wedge\mathbf{u}\) and \(\mathbf{x}\wedge\mathbf{v}=\mathbf{b}\wedge\mathbf{v}\). Set \(\mathbf{U}=\mathbf{a}\wedge\mathbf{u}\) and \(\mathbf{V}=\mathbf{b}\wedge\mathbf{v}\). It is clear the intersection is a linear combination of \(\mathbf{u}\) and \(\mathbf{v}\). To find the coefficients, we look at the picture. The area corresponding to \(\mathbf{V}\) divided by the area corresponding to \(\mathbf{u}\wedge\mathbf{v}\) gives the multiple of \(\mathbf{u}\) needed, and dividing \(\mathbf{U}\) by \(\mathbf{u}\wedge\mathbf{v}\) gives the \(\mathbf{v}\) multiple. However, since the orientation of the bivectors must be taken into account, we need to reverse \(\mathbf{u}\wedge\mathbf{v}\) in the \(\mathbf{v}\) direction. So the final answer must be

```
\(\mathbf{x}=\frac{\mathbf{V}}{\mathbf{u}\wedge\mathbf{v}}+\frac{\mathbf{U}}{\mathbf{v}\wedge\mathbf{u}}\cdot\mathbf{v}.\)
```

Someone fluent with geometric algebra would sketch the picture and be able to write out this equation instantly. With a GA engine, there is no need for a complicated line intersection routine—only the geometric product!

![](img/672fe9a2d008ba627b1991e15d70f43e_260_1.png)

### FIGURE 2.1.12 Here is a graphical way to visualize Cramer's Rule.

- 11. A do at home exercise; given a plane triangle with corners $(x_i, y_i)$, $i=1,2,3$, show the area is the absolute value of the determinant in Equation 2.1.22. Using only analytic geometry, this proof is a lot of work, but is very short using GA (about a half page). Hint: this is easy from using the outer product. Generalize to higher dimensions:

```
\(Area = \frac{1}{2} \begin{vmatrix} x_1 & y_1 & 1 \\ x_2 & y_2 & 1 \\ x_3 & y_3 & 1 \end{vmatrix}.\) (2.1.22)
```

- 12. As a final example, consider the problem of finding a rotation that will move one orientation to another, as shown in Figure 2.1.13.

![](img/672fe9a2d008ba627b1991e15d70f43e_261_0.png)

For example, we might want to align an AI-controlled spaceship with a player-controlled one. If we have stored orientations as quaternions, then this is just an invert and multiply, but if we only have three linearly independent vectors defining each orientation, finding this rotation is a lot of work. We don't require the vectors to be orthogonal, only linearly independent. Assume there is a rotation (rotor) \(\mathbf{R}\) such that \(\mathbf{b}_i = \mathbf{R}\mathbf{a}_i\mathbf{R}^{-1}\) for \(i=1,2,3\). We want to solve these three equations for \(\mathbf{R}\). Let \(\mathbf{R} = \alpha - \mathbf{B}\) for some bivector \(\mathbf{B}\) (thus \(\mathbf{R}^{-1} = \alpha + \mathbf{B}\)). The adventurous reader should attempt to solve this using linear algebra before proceeding. We define a reciprocal frame (which acts somewhat like an orthonormal frame) written with superscripts: set

