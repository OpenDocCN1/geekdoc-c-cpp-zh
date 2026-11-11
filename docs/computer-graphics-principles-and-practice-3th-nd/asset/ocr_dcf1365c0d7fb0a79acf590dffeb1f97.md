An alternative is to say, “Let’s just compute n = u × v,” and use the previous solution; that’s an excellent choice, because the cross-product computation can be performed once, and stored for later reuse. The point here is that computing a ray intersection with the implicit form is computationally far easier than doing so with the parametric form of the plane.

# ### 7.8.2 Ray-Sphere Intersection

Once again, suppose we have a ray whose points are of the form P + t d, with t ≥ 0. We want to compute its intersection with a sphere given by its center, Q, and its radius, r.

The implicit description of this sphere is that the point X is on the sphere if the distance from X to Q is exactly r; this is equivalent to the squared distance (which is almost always easier to work with) being r², that is,

$$(X − Q) · (X − Q) = r²$$ (7.103)

where we’ve used the fact that the squared length of a vector v is just v · v.

Now let’s ask, “Under what conditions on t is P + t d on the sphere?” It must satisfy

$$((P + t d) − Q) · ((P + t d) − Q) = r².$$ (7.104)

Because the vector P − Q is going to come up a lot, we’ll give it a name, v; now we can simplify the expression above:

$$((P + t d) − Q) · ((P + t d) − Q) = r²$$ (7.105)
$$((P − Q) + t d) · ((P − Q) + t d) = r²$$ (7.106)
$$(v + t d) · (v + t d) = r²$$ (because v = P − Q) (7.107)
$$(v · v) + 2(t d · v) + (t d · t d) = r²$$ (7.108)
$$(v · v − r²) + t(2 d · v) + t²(d · d) = 0.$$ (7.109)

This last equation is a quadratic in t, which therefore has zero, one, or two real solutions.

> > **Inline Exercise 7.13:** Describe geometrically the conditions under which this equation will have zero, one, or two solutions, as in “If the ray doesn’t intersect the sphere, there will be no solutions; if …”

Fortunately, it’s easy to tell whether a quadratic c + bt + at² = 0 has zero, one, or two real solutions. The quadratic formula tells us that the solutions are

$$t = (−b ± √(b² − 4ac)) / (2a)$$ (7.110)

which are real if b² − 4ac ≥ 0; the two solutions are identical precisely if the square root is zero, that is, if b² = 4ac. In our case, this turns out to mean that there are two solutions if