![](bbox=[0.156, 0.113, 0.469, 0.266])

Figure 10.7 Results of applying two different compactness measures to various regions. Since a circle has the minimum perimeter for a given area, it minimizes \( T_a \). A starfish on the other hand, has a large perimeter for the same area.

then extend the discussion to some invariant features like moments, chain codes, Fourier descriptors, and the medial axis.

# 10.4.1 Simple Features

In this section, we describe several simple features that can be used to describe the shape of a patch – the output of the segmentation process. Many of these features can be computed as part of the segmentation process itself. For example, since the connected component labeling program must touch every pixel in the region, it can easily keep track of the area. Following is a list of simple features that are likewise simple to calculate.

+   - **Average gray value** In the case of black and white “silhouette” pictures, this is simple to compute.
+   - **Maximum gray value** This is straightforward to compute.
+   - **Minimum gray value** This is straightforward to compute.
+   - **Area (A)** A count of all pixels in the region.
+   - **Perimeter (P)** Several different definitions exist. Probably the simplest is a count of all pixels in the region that are adjacent to a pixel not in the region.
+   - **Diameter (D)** The diameter is the length of a maximum chord; the distance between those two points in the region whose mutual distance is maximum [10.33, 10.35].
+   - **Thinness (also called Compactness”) (T)** Two definitions for compactness exist: \( T_a = \frac{P^2}{A} \) measures the ratio of the squared perimeter to the area; \( T_b = \frac{D^2}{A} \) measures the ratio of the diameter to the area. Figure 10.7 compares these two measurements on example regions.
+   - **Center of gravity (CG)** The center of gravity may be determined by

```
\(\hat{\mathbf{x}} = \frac{1}{N} \sum_{i=1}^N \mathbf{x}_i\) (10.48)
```

for all \( N \) points in a region.

3 Some authors [10.34] prefer not to confuse the mathematical definition of compactness with this definition, and thus refer to this measure as the isoperimetric measure.