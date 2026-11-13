
visualization [Card et al. 99, Bederson and Shneiderman 03]. A good starting reference for the various problems and subtleties involved in the process of designing colormaps for visualizing scalar data is the paper of Bergman et al. [Bergman et al. 95], which also describes a rule-based mechanism and tool for assisting users with selecting effective colormaps for different types of datasets. For a discussion on the use of rainbow, diverging, heat map, and grayscale colormaps in scientific visualization, we refer to [Borland and Taylor 07, Moreland 09]. For an extensive discussion of issues involved in color mapping both continuous and categorical attributes, see the book of Colin Ware on information visualization [Ware 04]. For a general discussion of color science, beyond color mapping in data visualization, a good starting point is Stone's book on digital color [Stone 03]. For the design of colormaps that have a few (5–10) different colors, one can use the ColorBrewer tool resource [Brewer and Harrow 13]. Among other features, ColorBrewer can generate colormaps tuned for encoding sequential and qualitative value types and optimized for different types of output, such as monochrome or color printer, projector, laptop, and monitor.

## 5.3 Contouring

In the previous section, we described how 2D scalar fields can be visualized using the simple colormap technique. We also discussed how using too few colors in a colormap leads to undesired color-banding effects (see Figure 5.6). However, color banding is related to fundamental and widely used visualization technique called contouring. To understand contouring, think of the meaning of the sharp color transitions that separate the color bands in Figure 5.7(a).

Consider, for instance, the transition between the yellow and orange bands; that is, all points in the figure that are on the border separating these two colors. As can be seen from the associated color legend, points in the yellow band have scalar values s below 0.11, whereas the points in the orange band have scalar values s above 0.11 (see also Equation (5.1)). Hence, the points located on the color border itself have the scalar value s = 0.11. Note that, for this reasoning to hold, we must assume that our dataset does not exhibit a sudden “jump” located exactly on the extent of the border itself. This holds for all datasets that represent the sampling of a continuous signal.

Points located on such a color border, drawn in black in Figure 5.7(a), are called a contour line, or isoline. Formally, a contour line C is defined as all points p in a dataset D that have the same scalar value, or isovalue s(p) = x, or

```
C(x) = {p ∈ D|s(p) = x}.
(5.4)
```

![](img/1274306e378c42ed8a0ad5669902d2a1_176_0.png)

Figure 5.7. Relationship between color banding and contouring.

The name “isoline” also reflects this definition, as in Greek, *isos* means “the same” or “equal.” The name “contour line” stems from one of the first applications of this technique in cartography. Contour lines are drawn on land maps to explicitly indicate all points that have the same altitude. Note that Equation (5.4) can be applied also in higher dimensions than two. For 3D datasets, contours are 2D surfaces called *isosurfaces*. Several examples of isosurfaces are provided later in this section.

In Figure 5.7(b), we show the same scalar dataset as in Figure 5.7(a), visualized with the same rainbow colormap. However, this time the colormap has 256 entries, instead of only eight as in Figure 5.7(a). This is visible in the fact that the color legend itself exhibits a smoother hue variation as compared to the one in Figure 5.7(a). The right image is smoother, which is desirable, as it helps us distinguish more detail than in the left image. Yet, this image does not help us further if we are interested in easily and quickly distinguishing which are the points that have a specific scalar value of interest, e.g., s = 0.11. This task was easily done on the left image, because the colormap used there exhibited a clear hue transition from dark blue to cyan located precisely at this value. We can actually combine the advantages of contours and color mapping by simply drawing contours for all values of interest on top of a color-mapped image that uses a rich colormap. The result is shown in Figure 5.7(b), where we have drawn seven contours for scalar values equally spaced in [-0.165, 0.165].

Besides indicating points where the data has specific values, contours can also tell us something about the data variation itself. Assume that we have a set of contours for scalar values that are equally spaced in the scalar domain, such as in Figure 5.7(b). Clearly, the contours themselves are not equally spaced in the spatial domain. Areas where contours are closer to each other, such as in the center of the image, indicate higher variations of the scalar data. Indeed, the scalar distance between consecutive contours (which is constant) divided by the spatial distance between the same contours (which is not constant) is exactly the derivative of the scalar signal.

Contour properties. Contours have a number of important properties. Consider Figure 5.8, which shows a two-variable function z = f(x, y) with the familiar elevation plot technique. Over the function graph, three isolines are drawn, for three different values, v0 (blue), v1 (red), and v2 (yellow). The isolines are translated on the vertical (z) axis above the xy plane with their corresponding values vi instead of being drawn in the dataset domain (xy plane) as in Figure 5.7. In this situation, the isolines correspond with the intersection of the function graph with horizontal planes z = vi, i ∈ {0, 1, 2}.

Several properties of isolines are noticeable in Figure 5.8. First, isolines can be either closed curves, such as the yellow isoline, or open curves, such as the blue and red isolines. Isolines never stop inside the dataset itself—they either close upon themselves, such as the yellow one, or stop when reaching the dataset border, such as the blue and red ones. Second, an isoline never

![](img/1274306e378c42ed8a0ad5669902d2a1_177_0.png)

Figure 5.8. Isoline properties.

![](img/1274306e378c42ed8a0ad5669902d2a1_178_0.png)

Figure 5.9. The gradient of a scalar field is perpendicular on the field's contours.

intersects (crosses) itself, nor does it intersect an isoline for another scalar value. Hence, isolines for different values are “nested” inside each other, as we can see in Figure 5.7. These properties always hold for a (piecewise) continuous dataset as defined in Section 3.1. In other words, the scalar data does not have “jumps” between points that are close in the dataset domain. Finally, consider Figure 5.9, which shows the same scalar function and its isolines as in Figure 5.8, this time viewed from above along the z-axis. The vector field displayed in the image shows the gradient of the scalar function. This figure demonstrates an important property of the contours, namely that they are perpendicular to the gradient of the contoured function. This property is not surprising: The gradient of a function is the direction of the function’s maximal variation, whereas contours are points of equal function value, so the tangent to a contour is the direction of the function’s minimal (zero) variation. Another example showing how the gradient of a scalar field is perpendicular to its isolines is given in Section 9.4.7.

Computing contours. How can we compute contours, given a discrete, sampled dataset D? Since this dataset is defined as a set of cells carrying node or cell scalar data, plus additional basis functions (Chapter 2), it is natural to try to construct contours in the same discrete cell space. In the actual construction technique, presented next, we shall use an important property of isolines. We

![](img/1274306e378c42ed8a0ad5669902d2a1_179_0.png)

Figure 5.10. Constructing the isoline for the scalar value v = 0.48. The numbers in the figure indicate scalar values at the grid vertices.

have seen in Section 3.1 that the reconstruction of a sampled dataset with piecewise linear basis functions is a piecewise linear function itself. The graph of this function is piecewise linear, too. Being the intersection of the function graph with a horizontal plane, the isoline of such a dataset is, therefore, piecewise linear. Since an isoline has topological dimension 1, this is a polyline.

The basic algorithm for constructing an isoline is quite simple. The principle is illustrated by the simple $5 \times 5$ cell grid in Figure 5.10, where we construct the isoline for the value $v = 0.48$. For every cell $c$ of the dataset, we test whether the isoline intersects the respective cell, as follows. For every edge $e = (p_i, p_j)$ of the cell $c$, we test whether the isoline value $v$ is between the scalar vertex attributes $v_i$ and $v_j$ corresponding to the edge end points $p_i$ and $p_j$. If the test succeeds, the isoline intersects $e$ at a point

```
q = \frac{p_i(v_j - v) + p_j(v - v_i)}{v_j - v_i}. \quad (5.5)
```

This result is obtained by expressing $q$ as a linear interpolation of $p_i$ and $p_j$ with the same weights used to express $v$ as a linear interpolation of $v_i$ and $v_j$. We repeat the previous procedure for all edges of our current cell and finally obtain a set of intersection points $S = \{q_i\}$ of the isoline with the cell. For
