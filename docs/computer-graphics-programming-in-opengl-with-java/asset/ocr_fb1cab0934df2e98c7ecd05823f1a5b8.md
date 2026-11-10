+   - When t_near is negative and t_far is positive, then the ray started inside the sphere and the first intersection point is at t_far.
+   - When both are positive, the first intersection point is at t_near. Note that this also handles the case of the ray skimming the surface of the sphere, when both t_near and t_far are positive and equal to each other (which occurs when the discriminant Δ is zero).

Finally, once the value of t has been determined, the corresponding point is easily calculated:

$collision\ point = r_s + t * r_d$

Later, we will need the surface normal at the collision point, hereafter called the *collision normal*, which is a vector from the center of the sphere to the intersection point:

$collision\ normal = normalize(collision\ point - s_p)$

noting that if the ray started inside the sphere, then the collision normal would need to be negated.

# ## 16.2.1 Axis-Aligned Ray-Box Intersection

Computing the intersection(s) of a ray with a box is similarly well-documented and derived using geometry, the most common approach having been derived by Kay and Kajiya [K86]. Again we describe only the solution, as adapted for GPU vector operations [H69]. And as for the sphere, a ray will intersect a box at 0, 1, or 2 points.

Program 16.2 assumes the box is aligned with the world axes (we handle other orientations later). We define the box using two points at diagonally-opposite corners; i.e., $(x_{min}, y_{min}, z_{min})$ and $(x_{max}, y_{max}, z_{max})$. In Program 16.2, those are $box\_mins$ and $box\_maxs$ at (2, -2, 0) and (-0.5, 1, 2), respectively. These two points are then used to identify the six X/Y/Z planes that comprise the box. For example, the two “X” planes are specified as the X values for the two box sides parallel to the YZ plane. Finding the distance t at which the ray intersects each of the six planes can be done efficiently with GLSL vec3 operations (see [S11] for a derivation):