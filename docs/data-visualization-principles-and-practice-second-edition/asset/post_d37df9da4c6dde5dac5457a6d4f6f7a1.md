
helps users in understanding what the meaning of the $x$- and $y$-axes in a given view mean in terms of the original $K$-dimensional variables.

The small red-green icons under the bar charts indicate the *direction* of the attribute variation with respect to the screen axes. A green icon indicates that the respective attribute increases in the sense of the respective screen axis. A red icon indicates that the attribute decreases along that screen axis. Looking at these icons, we can see that *median house income* increases along the $y$-axis (which confirms the earlier finding obtained using color mapping along the same axis). However, we also see that *longitude* increases along the $z$-axis, while *latitude* decreases along the same axis—two findings which we could not have obtained so far.

The *z-axis legend*, shown top-right in Figure 11.33, shows the amount of information we do not see in the current view of our 3D scatter plot. Here, bar lengths show how much an attribute spreads along the $z$-axis. Since the $z$-axis is orthogonal to the screen plane, variations along it are never visible from the current viewpoint. In our example, we see that *households*, *population*, *#rooms*, and *#bedrooms* map well on the $z$-axis—and thus cannot be seen in the current 2D view.

Combining the above mechanisms, we can now read the plot in Figure 11.33 as follows:

- The studied dataset shows two large concentrations of housing records for two distinct geographical locations (the two peaks in the scatter plot).
- The spread on median house income is similar for both locations.
- For the entire dataset, median income and house values are well correlated.
- The largest variation in the data occurs for median house income, followed by geographical position.

Explanatory visualizations significantly enrich bare scatter plots used to display projected datasets, by adding information that lets users map back from the reduced $k$-dimensional plot space to the original $K$-dimensional data space. Additional details on the construction of such visualizations are given in [Brooksema et al. 13, Oeltze et al. 07]. However, as the number and complexity of dimensionality reduction methods grows, the challenge of making dimensionality reduction plots easy to use and widely accepted by the grand public remains open.

### 11.5.7 Assessing Projection Quality

As already outlined at the beginning of the previous section, the effectiveness of a dimensionality reduction plot resides in two factors: The ease of interpreting the final low-dimensional plot, and the quality of the projection itself. In the previous section, we have shown how explanatory visualizations can address the former aspect. In this section, we focus on how we can assess the quality of projections, with a focus on neighborhood preservation and group interpretation.

Given a relevant projection P defined as in Equation 11.8, the following questions are relevant:

- 1. False neighbors: For a point \( p_i \in D \) and its 2D projection \( P(p_i) \in \mathbb{R}^k \), a necessary condition for neighborhood preservation is that all points \( P(p_j) \in \mathbb{R}^k \) which are close to \( P(p_i) \) should be projections of points \( p_j \) which are close to \( p_i \) in \( A^K \). If not, i.e., we have a projection \( P(p_j) \) close to \( P(p_i) \) for which \( p_j \) is not close to \( p_i \), we will wrongly infer from the 2D projection that \( p_j \) is close to \( p_i \). We call point \( j \) a *false neighbor* of point \( i \). How can we visually find false neighbors?

- 2. Missing neighbors: The second necessary condition for neighborhood preservation is that all points \( p_j \), which are close to \( p_i \) in \( A^K \), whose projection is close to \( P(p_i) \) in \( \mathbb{R}^k \). If not, i.e., we have a point \( p_j \) close to \( p_i \) whose projection is not close to \( P(p_i) \), then we will underestimate the set of points similar to point \( i \). We call such a point \( j \) a *missing neighbor* of point \( i \). How can we visually find missing neighbors?

- 3. False and missing group members: An important task in projection visualization is to help users find groups of similar points, such as in the example discussed in Figure 11.32. For groups, the point-wise problems of false and missing neighbors generalize to the problems of false and missing group members, respectively. That is, given a *visual group* \( \Gamma \), i.e., a set of closely projected points, we want to find if all points located in \( \Gamma \) truly belong to the group in terms of attribute similarity (no false members). Second, we want to find if all points that are similar to the group elements in terms of attributes do indeed project in \( \Gamma \) (no missing members). How do we visually find false and missing members?

- 4. Comparing projections: Given two projections \( P_1 \) and \( P_2 \) of the same dataset \( D \), which projection preserves distances and neighborhoods better?

The stress function $\sigma$ (Equation 11.9) delivers only an aggregated, single scalar value, for an entire projection. The questions above, however, require more fine-grained answers. To address these, we can use several visualization methods, as follows.

*Aggregate point-wise error:* To begin with, we define the projection error of a point $i$ with respect to a point $j \neq i$ as

$$e_{ij} = \frac{\|P(p_i) - P(p_j)\|}{\max_{i,j}(\|P(p_i) - P(p_j)\|)} - \frac{d_{ij}}{\max_{i,j} d_{ij}}.$$ (11.15)

Here, $d_{ij} = \|p_i - p_j\|$ is the distance between points $i$ and $j$ in $A^K$ (Equation 11.10). Clearly, $e_{ij}$ can be estimated for both MDS methods that use only the distance matrix $M$, and also for projection-based methods that have access to the $K$-dimensional point coordinates. We see that $e_{ij} \in [-1, 1]$. Negative errors indicate points whose projections are too close (thus, false neighbors). Positive errors indicate points whose projections are too far apart (thus, missing neighbors). Zero values indicate projections which approximate optimally the distances in $A^K$.

We next define the aggregate error of a point $i$ as

$$e_i^{aggr} = \sum_{j \neq i} |e_{ij}|.$$ (11.16)

For a given point $i$, $e_i^{aggr}$ gives the projection error of that point with respect to all other points. Hence, low values of $e^{aggr}$ show points whose projections can be reliably compared with most other projections in terms of assessing similarity. These are also good candidates for the so-called representatives, or control points, for multilevel projection methods (Faloutsos and Lin 95, Pekalska et al. 99, Chalmers 96, Paulovich et al. 08). Large values of $e^{aggr}$ show points which are badly placed with respect to most other points. These are good candidates for manual projection optimization [Silva et al. 12, Paulovich et al. 11].

Figure 11.34(a) shows the aggregate error for the LAMP projection of the Segmentation dataset shown in Figure 11.32, using rainbow color mapping. Here, $e_{ij} \in [-0.67, 0.35]$. Rather than showing $e_i$ only at point locations, we used here Shepard interpolation to construct a continuous signal between the points (Equation 3.47). The advantage is that the visualized image exhibits lower frequencies and is also space-filling, thus it allows us to visually locate outliers easier than when visualizing a color-coded point cloud. The image shows that the aggregate error is relatively smoothly distributed over the entire projection, and also that this error is not zero (dark blue) for almost any significant zone in the image.

![](img/1274306e378c42ed8a0ad5669902d2a1_538_0.png)

Figure 11.34. Visualizing aggregate projection error (a), false neighbors (b), and missing neighbors shown with color mapping (c,d) and edge bundles (e,f). Markers in images (e–f) indicate selected points.

The blue areas close to the plot border show that points here are relatively better placed than points in the middle of the plot. We also locate a few small red spots (marked by circles in the image). These are high-error areas, which indicate that
