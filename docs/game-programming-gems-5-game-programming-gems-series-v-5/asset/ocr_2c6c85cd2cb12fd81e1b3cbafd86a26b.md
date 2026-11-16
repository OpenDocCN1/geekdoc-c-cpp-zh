```
a^1 = \frac{a_2 \wedge a_3 I}{a_1 \wedge a_2 \wedge a_3 I}
```

which is a vector (easily checked), and similarly define **a**<sup>2</sup> and **a**<sup>3</sup>. Note **a**<sup>i</sup>·**a**<sub>j</sub> = \(\delta^i_j\). Then we compute (carefully) the expression in Equation 2.1.23, which allows us to isolate **R**. Next, we solve for **R** in terms of the **a**<sup>i</sup> and **b**<sub>j</sub>. To get rid of the unknown \(\alpha\), we normalize: set **T** = 1 + \(\sum_i\) **b**<sub>i</sub>**a**<sup>i</sup>, and then **R** = **T**/|**T**| gives the desired rotor. The derivation is a bit of work to check, but the final answer is short, easy to compute, and takes very little code in a GA engine. Programming this given only linear algebra routines is a lot of work! As a final note on this example, one may need to check the sign of the final rotation, as shown in Equation 2.1.23, and watch out for 180 degree rotations.

```
\sum_i \mathbf{b}_i \mathbf{a}^i = \sum_i \mathbf{R} \mathbf{a}_i \mathbf{R}^{-1} \mathbf{a}^i
= \sum_i \mathbf{R} \mathbf{a} (\alpha + \mathbf{B}) \mathbf{a}^i
= \mathbf{R} (3\alpha + \mathbf{B})
= -\mathbf{R} (\alpha - \mathbf{B} - 4\alpha)
= -\mathbf{R} (\mathbf{R}^{-1} - 4\alpha)
= -1 + 4\alpha \mathbf{R}
(2.1.23)
```

# Conclusion and Future Directions

We have presented the definition of geometric algebra and given rules for hand computations, which can be turned into libraries for doing the work on a computer. Basic geometric ideas like projections and rotations were presented, and many examples were given to show how to use GA for geometric calculations. It should be clear GA unifies many ideas into a single framework and provides a much more concise and powerful framework than linear algebra. So what’s next?

Well, there is a lot more math, computer science, and physics already developed and written in the language of GA. There is a complete description of classical mechanics in GA [Hestenes86]; GA seems very well suited for physics. You can perform calculus on GA objects, allowing minima and maxima problems to be solved and allowing differential equations to be written to describe motions, interactions, and physical properties. We saw that GA incorporates quaternions, complex numbers, projections, intersections, linear (in)dependence, and more. It also encompasses Plückerspace and unites all of the following geometries into a single framework: Euclidean, affine, projective, spherical, inverse, hyperbolic, and conformal. This unification makes moving from one system to another much easier and provides quicker access to the methods in each area.