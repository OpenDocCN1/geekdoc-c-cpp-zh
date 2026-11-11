The critical problem, when we want to include transparency into the rendering equation, is that a pair (P, ω) ∈ M × S² is no longer associated to a unique radiance value.

Because we are only doing surface rendering rather than volume rendering (i.e., we’re ignoring participating media), we only care about L(P, ω) for points P that are on some surface. That surface must have a surface normal n at P. We can therefore define L(P, ω, n) by the rule that if ω and n have a positive dot product, then L(P, ω, n) represents the radiance leaving the surface in direction ω; if their dot product is negative, then it represents the radiance arriving at the surface in direction ω. By using either the unit outward surface normal or its opposite as n, we can handle both reflection and transmission. In practice, this turns into an additional ± statement at every ray-surface interaction. A surface element has two sides (one with a normal pointing each way), and we treat the vector ω differently depending on whether it points in the same or the opposite half-space as the normal vector to the “side.” In mathematical terms, we can say that L is defined on the orientation double cover [Lee09] of the set of all scene surfaces.

The three-argument version of L is awkward to write. As an alternative, we can replace L altogether with two new functions: (P, ω) → L^in(P, ω) and (P, ω) → L^out(P, ω), which represent light arriving at P traveling in direction ω and light leaving P in direction ω, respectively; these are Arvo’s field and surface radiance functions. The reflectance equation then becomes a **scattering equation:**

L^out(P, ω_o) = ∫_{ω_i ∈ S²(P)} L^in(P, −ω_i) f_r(P, ω_i, ω_o) |ω_i · n_P| dω_i,    (29.10)

where five things have changed.

+   - The integral is now over all directions of incoming light.
+   - The result is now L^out rather than L^ref (recall that L^ref denotes light either reflected or transmitted).
+   - The BRDF f_r has been replaced with the BSDF f_s.
+   - The dot product now has an absolute value.
+   - The annotations “in” and “out” have been added to the radiance and scattered radiance.

The transport equation now links incoming and outgoing light. We write the equation in two forms, one suitable for use in ray tracing, the other for use in photon mapping. The distinction is simply one of tracing rays in the direction of photon propagation or in the opposite direction. The version used in raytracing is this:

L^in(P, −ω_i) = L^out(R(P, ω_i), −ω_i)    (29.11)

while the one that’s useful in photon mapping is this:

L^out(Q, ω_o) = L^in(R(Q, ω_o), ω_o)    (29.12)

Dividing the radiance field into two parts has further advantages. When we write the radiance field this way, it naturally extends to all points P rather than