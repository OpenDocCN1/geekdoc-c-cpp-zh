facet hits yet another microfacet, etc. Because we’re assuming that the surfaces on which these microfacets reside are globally flat (at least relative to the scale of individual microfacets), we can assume that each microfacet interacts with only a few neighbors, thus reducing the complexity of the rendering problem. When we get to limiting cases like light arriving at a glancing angle, when many facets might shadow a single one, this simplifying assumption can break down.

# 27.16　Exercises

+   **Exercise 27.1:** In Gouraud shading, we have color values at the three vertices of a triangle, and we interpolate those values across the interior of the triangle. Since this is typically done on a raster screen, one approach is to work from top to bottom, linearly interpolating values along each edge, and then within a single row of pixels linearly interpolating between the two ends. In a typical triangle, there will be a top vertex, a bottom vertex, and a middle vertex. As we pass the middle vertex, we’ll need to start traversing a different edge. Alternatively, we could do interpolation from the top to the middle row, and from the bottom to the middle row.
+   
+   (a) Show that if we compute the intersection of an edge with a row center exactly (rather than rounding to the nearest pixel center), the result is exactly the barycentric interpolation of the vertex values.
+   
+   (b) Show that as we move from one row to the next, working down from the top vertex to the middle vertex, the starting value for each pixel row differs from the starting value for the previous row by the same amount.
+   
+   (c) Use the idea of part (b) to develop a low-operation-count implementation of Gouraud shading in the 2D tested, using “pixels” that are each small, colored rectangles to visualize your results.
+   
+   (d) Suppose we were to apply the same idea to shade a convex quadrilateral: We work from top to bottom, computing interpolated values along the two edge points in each row, and then linearly interpolate along the row. If we rotate the quadrilateral (keeping the assigned color values at each vertex), does the interpolated shading appear to rotate as well?

+   **Exercise 27.2:** It’s very common to photograph either the moon or a lighthouse being reflected in fairly calm (but not completely flat) water. The usual depiction shows the bright reflection appearing as a wedge that grows wider as it approaches the viewer, with the wedge point either near the lighthouse or (in the case of the moon) near the horizon. Find such a photograph, describe the notable features of the reflection (such as the shape of the wedge), and explain them in terms of the physical models you’ve seen in this chapter.

+   **Exercise 27.3:** A bookshelf holds three books, one with a white binding and two with black bindings. The shelf itself is made of polished wood. Looking down at the shelf, you can see the reflection of the spines of the books. Near the bottom of the spines, the division between the white and black reflections appears quite sharp. But if you look at the reflections of a region near the top of the spines, the division is quite blurry. Explain why. Is it a Fresnel effect, because of the difference in viewing angle? Why or why not? How could you test this idea? Hint: Actually set up the experiment!

+   **Exercise 27.4:** In the Phong model, as typically expressed, there’s a diffuse color, expressed as an RGB triple, and a diffuse reflectance.