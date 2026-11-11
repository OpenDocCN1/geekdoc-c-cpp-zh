The notions of “clockwise” and “counterclockwise” angles, and “the angle from ray 1 to ray 2” (which might be much larger than π) and of angles that “wrap around multiple times” can all be defined with careful adjustments of the definition above; in our study of light, though, we’ll have no need for these ideas, so we’ll simply use the definition of angle and measure above.

One common use of angles is the notion of the *angle subtended* by some shape, T, at a point P (see Figure 26.19). The shape T is projected onto the unit circle C around P, and the measure of the resultant angle is called the **angle subtended by T at P**. In equations, the angle subtended by T at P is

![](bbox=[0.71, 0.093, 0.948, 0.245])

*Figure 26.19: The angle subtended by T at P.*

{S(X − P) : X ∈ T}, (26.21)

We can now describe **solid angles** in R³ by analogy. A **solid angle** at a point P ∈ R³ is a (measurable) subset Ω of the unit sphere about P, or, equivalently, a measurable subset of S², the collection of all unit vectors in 3-space. The **measure of the solid angle** is the area of the set Ω (see Figure 26.20).

![](bbox=[0.71, 0.33, 0.94, 0.505])

*Figure 26.20: The solid angle Ω is a set on the surface of the unit sphere. The measure of the solid angle is the area of this set.*

When we want to treat points in a solid angle as unit vectors, we’ll use bold Greek letters, almost always using the letter ω. We’ll often write “Let ω ∈ Ω, . . . ,” and thereafter treat ω as a unit vector, writing expressions like ω · n to compute the length of the projection of a vector n onto ω. In fact, this use of a solid angle as a collection of direction vectors is almost the only one we’ll see.

The notion of subtended angle can also be extended to three dimensions: If T is a shape in R³ and P a point of R³ with P ∉ T, the **solid angle subtended by T at P** is the area of the radial projection of T onto the unit sphere at P, in exact analogy with the two-dimensional case. More precisely, the **solid angle subtended by T at P** is

{S(Q − P) : Q ∈ T},

in exact analogy with the 2D case.

This definition lets us speak of “solid angles” on other spheres (e.g., like the Earth) by defining their measure to be the measure of the solid angle they subtend at the center of the sphere. It’s easy to show that if U is a subset of a sphere of radius r about P, and the area of U is A, then the solid angle represented by U (i.e., the solid angle subtended by U at P) is A/r². When we speak of measuring a solid angle on some arbitrary sphere (like the Earth, or a spherical lightbulb), it is implicit that we mean “the solid angle subtended at the center of the sphere by this region.”

**Inline Exercise 26.10:** Estimate the solid angle measure of your country as a solid angle on the (roughly) spherical earth. Use 13,000 km (or 8000 mi) as the diameter of the Earth.

**Notation:** It’s conventional to use Ω to denote both a solid angle and the measure of that solid angle (just as we use θ to denote an angle and its measure in the plane). Just as we often use x as a variable of integration in calculus, it’s common to use the letter Ω to denote a solid angle, and ω to denote a member of Ω, so that ω is a unit vector.