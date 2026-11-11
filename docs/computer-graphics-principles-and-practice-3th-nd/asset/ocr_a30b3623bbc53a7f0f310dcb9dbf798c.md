# Listing 31.2: Recursive ray tracing.

```
```
 1  foreach pixel (x, y):
 2      R = ray from eye point E through pixel
 3      image[x, y] = raytrace(R)
 4
 5  raytrace(R):
 6      P = raycast(R) // first scene intersection
 7      return lightFrom(P, R) // light leaving P in direction opposite R
 8
 9  lightFrom(P, R):
10      color = emitted light from P in direction opposite R.
11      foreach light source S:
12          if S is visible from P:
13              contribution = light from S scattered at
14                           P in direction opposite R
15              color += contribution
16      if scattering at P is specular:
17          R_sw = reflected or refracted ray at P
18          color += raytrace(R_sw)
19      return color
```
```

the image we’re computing, and we often use multiple samples per pixel, with some kind of averaging. But the broad idea remains: Cast rays from the eye; compute direct illumination; add in recursive rays. Ray tracing computes the contributions of paths of the form LD*SE.

The essential features of a ray tracer (and all the subsequent algorithms) are a ray-casting function (something that lets us shoot a ray into a scene and find the first surface it encounters), and a BRDF or bidirectional scattering distribution function (BSDF), which takes a surface point P and two rays ω_o and ω_i, and returns f_r(P, ω_o, ω_i). (In the pseudocode, that BRDF is hidden in the “light from S scattered at P in direction opposite R,” which has to be computed by multiplying the radiance from the light by a cosine and the BRDF to get the scattered radiance.) A slightly more sophisticated ray tracer removes the “if scattering is specular” condition, and if the scattering is nonspecular, the scattered radiance is estimated by casting multiple recursive rays in many directions, weighting the returned results by the BSDF according to the reflectance equation. It’s this form of ray tracing that we’ll refer to henceforth.

Later, in addition to the BRDF or BSDF, we’ll also want a function that takes a surface point P and a ray ω_o, and returns a random ray ω_i with probability density approximately proportional to the BRDF or BSDF, or cosine-weighted versions of these.

Following Kajiya, we can draw a highly schematic representation of ray tracing (see Figure 31.18). Rays are traced from the eye to the scene; at an intersection, we compute direct lighting and accumulate it as part of the radiance from the light to the eye along the leftmost segment of the path. We also cast recursive rays. In basic ray tracing, we do only so in the specular-bounce direction (if the surface is partly specular); in more sophisticated approaches, we may do so in many directions. When a recursive ray meets a different surface point, the direct lighting there is propagated back to the first intersection, and thence to the eye. This propagation involves two scattering operations. Further depths involve further scattering. In the end, we have a branching tree representing the gathering of light into a single pixel of the final image. The branching factor of the tree depends on the number of recursively cast rays at each scattering event.

![](bbox=[0.713, 0.508, 0.918, 0.665])

Figure 31.18: Each blue vertical line represents all of M, the set of points of the scene; a green path from the eye (at left) meets M at some point, and then recursively, multiple rays are traced; these meet the second copy of M, etc. Each branching at such an intersection is a scattering event. The red rays from the upper right to the ray-surface intersections represent light arriving from light sources, which in this schematic representation are placed infinitely far away so that all direct illuminations can be drawn parallel.