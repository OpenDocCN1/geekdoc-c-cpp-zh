a binary value that is 1 if the ray intersects the primitive between the image plane and infinity, and 0 otherwise. This is equivalent to the visibility function applied to the primary ray origin and a point infinitely far away along the primary ray.

For a scene containing multiple primitives, primitives may occlude each other in the camera's view. The **depth complexity** of a ray is the number of times it intersects the scene. At any given intersection point *P*, the **quantitative invisibility** [App67] is the number of other primitive intersections that lie between the ray origin and *P*. Figure 36.6 shows examples of each of these concepts.

![](bbox=[0.709, 0.08, 0.941, 0.13])

Figure 36.6: The quantitative invisibility of two points is the number of surface intersections on the segment between them. The quantitative invisibility of B with respect to A is 2 in this figure. The depth complexity of a ray is the total number of surface intersections along the ray. The ray from A through B has depth complexity 3 in this figure.

For some applications, backfaces—surfaces where the dot product of the geometric normal and the ray direction is positive—are ignored when computing depth complexity and quantitative invisibility. The case where the intersection of the ray and a surface is a segment (e.g., Figure 36.7) instead of a finite number of points is tricky. We've already discussed that the existence of such an intersection is already suspect due to limited precision, and in fact for it to occur at all with nonzero probability requires us to have explicitly placed geometry in just the right configuration to make such an unlikely intersection representable. Of course, humans are very good at constructing exactly those cases, for example, by placing edges at perfectly representable integer coordinates and aligning surfaces with axes in ways that could never occur in data measured from the real world. We note that for a closed polygonal model, it is common to ignore these line-segment intersections, but the definition of depth complexity and quantitative invisibility for this case varies throughout the literature.

In the case of multiple primitive intersections, we say that the coverage is 1 at the first intersection and 0 at all later ones to match the visibility function definition.

At the end of this chapter, in Section 36.9, we extend binary coverage to **partial coverage** by considering multiple light paths per pixel.

![](bbox=[0.775, 0.344, 0.858, 0.471])

Figure 36.7: A ray tangent to an intersected surface.

# ## 36.1.4 Current Practice and Motivation

Most rendering today is on triangles. The triangles may be explicitly created, or they may be automatically generated from other shapes. Some common modeling primitives that are reducible to triangles are subdivision surfaces, implicit surfaces, point clouds, lines, font glyphs, quadrilaterals, and height field models.

Ray-tracing renderers solve exact visibility determination by **ray casting** (Section 36.2): intersecting the model with a ray to produce a sample. Data structures optimized for ray-triangle intersection queries are therefore important for efficient evaluation of the visibility function. Chapter 37 describes several of these data structures. **Backface culling** (Section 36.6) is implicitly part of ray casting.

Hardware rasterization renderers today tend to use **frustum culling** (Section 36.5), **frustum clipping** (Section 36.5), **backface culling** (Section 36.6), and a **depth buffer** (Section 36.3) for per-sample visible surface determination. Those methods provide correctness, but they require time linear in the number of primitives. So relying on them exclusively would not scale to large scenes. For efficiency it is therefore necessary to supplement those with conservative methods for determining occlusion and hierarchical methods for eliminating geometry outside the view frustum in sublinear time.

A handful of applications rely on the **painter's algorithm** (Section 36.4.1) of simply drawing everything in the scene in back-to-front order and letting the