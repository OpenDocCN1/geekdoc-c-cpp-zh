with finite-precision arithmetic, introducing small-magnitude errors (see Figure 36.5). So we must explicitly phrase all applications of the visibility function and all intersection queries with some small offset. This is often called **ray bumping** because it “bumps” the origin of the visibility test ray a small distance from the starting surface. Note that the bumping must happen on the other end as well. For example, to evaluate V(Q, P), attempt to find a scene point X = Q + S(Q − P)t for ε < t < |P − Q| − ε. If and only if there is no scene point satisfying that constraint, then V(Q, P) = 1. Failing to choose a suitably large ε value can produce artifacts such as **shadow acne** (i.e., **self-shadowing**), speckled highlights and reflections, and darkening of the indirect components of illumination shown in Figure 36.4. The noisy nature of these artifacts arises from the sensitivity of the comparison operations to the small-magnitude representation error in the floating-point values.

![](bbox=[0.706, 0.104, 0.958, 0.299])

Figure 36.4: (Top) Self-occlusion from insufficient numerical precision or offset values causes the artifacts of shadow acne and speckling in indirect illumination terms such as mirror reflections. (Bottom) The same scene with the shadow acne removed.

# ### 36.1.2 Primary Visibility

**Primary visibility** (a.k.a. **eye ray visibility**, **camera visibility**) is visibility between a point on the aperture of a camera and a point in the scene. To render an image, one visibility test must be performed per light ray sample on the image plane. In the simplest case, there is one sample at the center of each pixel. Computing multiple samples at each pixel often improves image quality. See Section 36.9 for a discussion of visibility in the presence of multiple samples per pixel.

A pinhole camera has a zero-area aperture, so for each sample point on the image plane there is only one ray along which light can travel. That is the **primary ray** for that point on the image plane. Consider three points on the primary ray: sample point Q on the imager, the aperture A, and a point P in the scene. Since there are no occluding objects inside the camera, V(Q, P) = V(A, P).

Since the visibility function evaluates intersections or intersection queries at all samples share a common endpoint of the pinhole aperture, there are opportunities to amortize operations across the image. **Ray packet tracing** and **rasterization** are two algorithms that exploit this technique. For more details, see Chapter 15, which develops the amortized aspect of rasterization and presents the equivalence of intersection queries under rasterization and ray tracing.

# ### 36.1.3 (Binary) Coverage

**Coverage** is the special case of visibility for points on the image plane. For a scene composed of a single geometric primitive, the coverage of a primary ray is

![](bbox=[0.112, 0.648, 0.632, 0.819])

Figure 36.5: Finite precision leads to self-occlusions. “Bumping” the outgoing ray biases the representation error in a direction less likely to produce artifacts by favoring the points above the surface as the ray origin.