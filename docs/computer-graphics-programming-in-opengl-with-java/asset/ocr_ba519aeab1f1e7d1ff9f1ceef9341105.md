intersect_box_object(), respectively), and returning the collision that has the shortest ray. If there is no colliding object, a special value of -1 is returned.

# ### 16.2.3 Ray-Sphere Intersection

Computing the intersection(s) of a ray with a sphere is derived using geometry and is well-documented [S16]. Although the derivation is relatively simple, here we describe only the solution. There are either 0, 1, or 2 intersection points, depending on if the ray misses the sphere, skims the surface, or enters on one side and exits out the other. Given the ray’s origin r_s and direction r_d, and the sphere’s position s_p and radius s_r, then finding the distance t along the ray at which the intersection(s) occur requires solving the following quadratic equation:

$$ (r_d • r_d)t² + 2(r_d • [r_s − s_p])t + [r_s − s_p]² − s_r² = 0    [1] $$

First, we compute its discriminant¹:

$$ Δ = (2r_d • [r_s − s_p])² − 4|r_d|²(|r_s − s_p|² − s_r²) $$

If Δ < 0, we can stop because the ray misses the sphere (and to avoid attempting to take the square root of a negative number). When Δ is not less than zero, there are then two solutions to equation [1]:

$$ t = ((-2r_d • [r_s − s_p]) ± √Δ) / (2(r_d • r_d)) $$

The smaller and larger of the two resulting values of t are denoted t_near and t_far, respectively.

+   - When both t_near and t_far are negative, the entire sphere is behind the ray and there is no intersection.

¹ In the code, we sometimes compute the square of the length of a vector V⃗ by computing V⃗ • V⃗, for performance reasons.