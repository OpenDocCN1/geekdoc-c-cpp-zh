
with finite-precision arithmetic, introducing small-magnitude errors (see Figure 36.5). So we must explicitly phrase all applications of the visibility function and all intersection queries with some small offset. This is often called **ray bumping** because it “bumps” the origin of the visibility test ray a small distance from the starting surface. Note that the bumping must happen on the other end as well. For example, to evaluate V(Q, P), attempt to find a scene point X = Q + S(Q − P)t for ε < t < |P − Q| − ε. If and only if there is no scene point satisfying that constraint, then V(Q, P) = 1. Failing to choose a suitably large ε value can produce artifacts such as **shadow acne** (i.e., **self-shadowing**), speckled highlights and reflections, and darkening of the indirect components of illumination shown in Figure 36.4. The noisy nature of these artifacts arises from the sensitivity of the comparison operations to the small-magnitude representation error in the floating-point values.

![](img/f464cd0043eb5336aa0543fe20a0561b_1077_0.png)

Figure 36.4: (Top) Self-occlusion from insufficient numerical precision or offset values causes the artifacts of shadow acne and speckling in indirect illumination terms such as mirror reflections. (Bottom) The same scene with the shadow acne removed.

### 36.1.2 Primary Visibility

**Primary visibility** (a.k.a. **eye ray visibility**, **camera visibility**) is visibility between a point on the aperture of a camera and a point in the scene. To render an image, one visibility test must be performed per light ray sample on the image plane. In the simplest case, there is one sample at the center of each pixel. Computing multiple samples at each pixel often improves image quality. See Section 36.9 for a discussion of visibility in the presence of multiple samples per pixel.

A pinhole camera has a zero-area aperture, so for each sample point on the image plane there is only one ray along which light can travel. That is the **primary ray** for that point on the image plane. Consider three points on the primary ray: sample point Q on the imager, the aperture A, and a point P in the scene. Since there are no occluding objects inside the camera, V(Q, P) = V(A, P).

Since the visibility function evaluates intersections or intersection queries at all samples that share a common endpoint at the pinhole aperture, there are opportunities to amortize operations across the image. **Ray packet tracing** and **rasterization** are two algorithms that exploit this technique. For more details, see Chapter 15, which develops the amortized aspect of rasterization and presents the equivalence of intersection queries under rasterization and ray tracing.

### 36.1.3 (Binary) Coverage

**Coverage** is the special case of visibility for points on the image plane. For a scene composed of a single geometric primitive, the coverage of a primary ray is a binary value that is 1 if the ray intersects the primitive between the image plane and infinity, and 0 otherwise. This is equivalent to the visibility function applied to the primary ray origin and a point infinitely far away along the primary ray.

![](img/f464cd0043eb5336aa0543fe20a0561b_1077_1.png)

Figure 36.5: Finite precision leads to self-occlusions. “Bumping” the outgoing ray biases the representation error in a direction less likely to produce artifacts by favoring the points above the surface as the ray origin.

For a scene containing multiple primitives, primitives may occlude each other in the camera's view. The **depth complexity** of a ray is the number of times it intersects the scene. At any given intersection point *P*, the **quantitative invisibility** [App67] is the number of other primitive intersections that lie between the ray origin and *P*. Figure 36.6 shows examples of each of these concepts.

![](img/f464cd0043eb5336aa0543fe20a0561b_1078_0.png)

Figure 36.6: The quantitative invisibility of two points is the number of surface intersections on the segment between them. The quantitative invisibility of B with respect to A is 2 in this figure. The depth complexity of a ray is the total number of surface intersections along the ray. The ray from A through B has depth complexity 3 in this figure.

For some applications, backfaces—surfaces where the dot product of the geometric normal and the ray direction is positive—are ignored when computing depth complexity and quantitative invisibility. The case where the intersection of the ray and a surface is a segment (e.g., Figure 36.7) instead of a finite number of points is tricky. We've already discussed that the existence of such an intersection is already suspect due to limited precision, and in fact for it to occur at all with nonzero probability requires us to have explicitly placed geometry in just the right configuration to make such an unlikely intersection representable. Of course, humans are very good at constructing exactly those cases, for example, by placing edges at perfectly representable integer coordinates and aligning surfaces with axes in ways that could never occur in data measured from the real world. We note that for a closed polygonal model, it is common to ignore these line-segment intersections, but the definition of depth complexity and quantitative invisibility for this case varies throughout the literature.

In the case of multiple primitive intersections, we say that the coverage is 1 at the first intersection and 0 at all later ones to match the visibility function definition.

At the end of this chapter, in Section 36.9, we extend binary coverage to **partial coverage** by considering multiple light paths per pixel.

![](img/f464cd0043eb5336aa0543fe20a0561b_1078_1.png)

Figure 36.7: A ray tangent to an intersected surface.

### 36.1.4 Current Practice and Motivation

Most rendering today is on triangles. The triangles may be explicitly created, or they may be automatically generated from other shapes. Some common modeling primitives that are reducible to triangles are subdivision surfaces, implicit surfaces, point clouds, lines, font glyphs, quadrilaterals, and height field models.

Ray-tracing renderers solve exact visibility determination by **ray casting** (Section 36.2): intersecting the model with a ray to produce a sample. Data structures optimized for ray-triangle intersection queries are therefore important for efficient evaluation of the visibility function. Chapter 37 describes several of these data structures. **Backface culling** (Section 36.6) is implicitly part of ray casting.

Hardware rasterization renderers today tend to use **frustum culling** (Section 36.5), **frustum clipping** (Section 36.5), **backface culling** (Section 36.6), and a **depth buffer** (Section 36.3) for per-sample visible surface determination. Those methods provide correctness, but they require time linear in the number of primitives. So relying on them exclusively would not scale to large scenes. For efficiency it is therefore necessary to supplement those with conservative methods for determining occlusion and hierarchical methods for eliminating geometry outside the view frustum in sublinear time.

A handful of applications rely on the **painter's algorithm** (Section 36.4.1) of simply drawing everything in the scene in back-to-front order and letting the ordering resolve visibility. This is neither exact nor conservative⁴, but it has the benefit of extreme simplicity. It is used almost exclusively for 2D graphical user interface rendering to handle overlapping windows. The primary 3D application of the painter's algorithm today is for rasterization of translucent surfaces, although recent trends favor more accurate per-sample stochastic and lossy-volumetric alternatives [ESSL10, LV00, Car84, SML11, JB10, MB07].

Many applications combine multiple visibility determination algorithms. For example, a hybrid renderer might rasterize primary and shadow rays but perform ray casting for visibility determination on other global illumination paths. A real-time hardware rasterization renderer might augment its depth buffer with hierarchical occlusion culling or precomputed conservative visibility. Many games rely on those techniques, but they include a ray-casting algorithm for visibility determination used to determine line of sight for character AI logic and physical simulation.

## 36.2 Ray Casting

Ray casting is a direct process for answering an intersection query. As previously shown, it also computes the visibility function: $V(P,Q) = 1$, if $P$ is the result of the intersection query on the ray with origin $Q$ and direction $(P - Q)/|P - Q|$; and $V(P,Q) = 0$ otherwise. Chapter 15 introduced an algorithm for casting rays in scenes described by arrays of triangles, and showed that the same algorithm can be applied to primary and indirect (in that case, shadow) visibility.

The time cost of casting a ray against $n$ triangles in an array is $O(n)$ operations. If $V(P,Q) = 1$, then the algorithm must actually test every ray-triangle pair. If $V(P,Q) = 0$, then the algorithm can terminate early when it encounters any intersection with the open segment $PQ$. In practice this means that computing the visibility function by ray casting may be faster than solving the intersection query; hence, resolving one shadow ray may be faster than finding the surface to shade for one ray from the camera. For a dense scene with high depth complexity, the performance ratio between them may be significant.

Terminating on any intersection still only makes ray casting against an array of surfaces faster by a constant, so it still requires $O(n)$ operations for $n$ surfaces. Linear performance is impractical for large and complex scenes, especially given that such scenes are exactly those in which almost all surfaces are not visible from a given point. Thus, there are few cases in which one would actually cast rays against an array of surfaces, and for almost all applications some other data structure is used to achieve sublinear scaling.

Chapter 37 describes many spatial data structures for accelerating ray intersection queries. These can substantially reduce the time cost of visibility determination compared to the linear cost under an array representation. However, building such a structure may only be worthwhile if there will be many visibility tests over which to amortize the build time. Constants vary with algorithms and architectures, but for more than one hundred triangles or other primitives and a few

⁴ ... nor how artists actually paint—for example, sometimes the sky is painted *after* foreground objects—but the name is now both a technical term and appropriately evocative.
