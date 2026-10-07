
# Data Clustering: Algorithms and Applications

to the respective outgoing segments by having similar slopes. The Visual-Clustering-approach [52] use curves in the same spirit as bundled edges [24]. Original line segments that go in the same direction are replaced by curves that draw close together. This reduces the visual space needed by the line segments, and consequently visual clutter is reduced. The curves are defined by introducing a few middle points at each segment between consecutive axes. The positions of all middle points are captured by minimizing a heuristic density function. This energy function balances two terms, one forcing the middle points to keep the original position and a counterpart for attraction forces between the curves. Both involve parameters that need to be heuristically set by the user. The energy minimizes over a large linear program using a simplex-based Ip-solver. Therefore, the layout computation is between minutes, which does not allow for interactive search of suitable parameter settings for the energy function.

A third use of curved segments is motivated by integrating parallel coordinates and scatterplots. The idea in [50] is to plot middle points between consecutive axes that define the curves as splines in such that the positions of middle points resemble the distances between data vectors in projections of the high-dimensional data space. Thus a curve connects two values of the data vector, and the middle point at this curve represents the data vectors relative distances in projected space. This integrates scatterplots represented by middle points and parallel coordinates represented by a single plot. Given $d$ the technique allows us to integrate at most $d-1$ of such scatterplots. The positions of the middle points are derived from distances of the data vectors in low-dimensional projection using multidimensional scaling (MDS) [36]. However, the visualization technique does not restrict this low-dimensional projected space to be the axis-parallel projection onto the two consecutive dimensions framing the scatterplot.

A much simpler embedding of scatterplots into parallel coordinates has been proposed in [25]. This integration shows the two-dimensional scatter plots between consecutive axes. Axes labels are effectively shared by rotating the scatterplots 45°. Figure 19.5 shows an example of Iris data.
The user presented in [25] also shows that the embedding of scatterplots into parallel coordinates is most helpful for users to detect clusters. This visualization performed significantly better with respect to response time and accuracy of the detected clusters than standard parallel coordinates, parallel coordinates with cluster enhancement by color and brightness as well as parallel coordinates with curves discussed above. The user also shows that animation techniques such as Grand Tour [6, 47] for parallel coordinates are less effective for cluster identification.

![](img/b94d85a2e934001944bcc21abd9a9943_516_0.png)

**FIGURE 19.5:** Scatterplots embedded into Parallel Coordinates showing the Iris data. The bold lines in the scatterplot show the directions of the sepal-width axis. Note, the intersections of the axes in the scatterplots are not the origin or the data mean.

# Concepts of Visual and Interactive Clustering

## 19.2.3 Discussion

Visualization of multidimensional data is an effective tool to explore and identify clusters, when the numbers of data vectors, clusters, and dimensions of the data are not large. Depending on the visualization technique a few hundred up to a few thousand data vectors can be processed. The number of clusters shown in the applications the cited papers exceeds ten. The dimensionality of the data is in almost all cases below 15.

Given this, visual interactive clustering without using an automated algorithm has the potential to allow effective exploration of the data and the identification of meaningful groupings that are useful in certain applications. This mainly complements automated algorithms that have their strengths in scalability to large data sets of high dimensionality comprising a large number of clusters.

## 19.3 Visual Interactive Clustering

A approaches have explored the possibility to combine an automated clustering algorithm with an interactive visualization technique. The proposed combination can be quite specific, which means that special properties of algorithm and/or the data visualization are required. The general design pattern of such combination is to replace some part of the algorithm with an interactive visual procedure that allows the user to influence the automated clustering algorithm during the computation of the cluster. A simple example is to replace the stopping criterion of an iterative clustering algorithm by visualizing the current state of the algorithm with respect to the given data and let the user decide whether the algorithm has reached a satisfying solution. Another example is to use interactive visualization techniques to build a hierarchical clustering. Depending on the underlying algorithm, the user decides, based on visualizations, which cluster found far could be split.

Another example is to influence iterative learning algorithms like self-organizing maps (SOM) during the initialization or during the learning procedure itself. The user can influence the algorithm by visually changing parts of the data structure, e.g some neurons in the SOM, that are otherwise automatically initialized or updated. That kind of interaction biases the algorithm into a some direction that the algorithm would possibly have not explored by following the internal learning procedure. In case of machine learning by optimization of some criterion, such user interaction could help the algorithm to break free of some local optima that would correspond to nonconforming clusters.

### 19.3.1 Visual Assessment of Convergence of Clustering Algorithm

Some clustering algorithms work in an iterative way by updating internal data structures. However, not all such algorithms are guaranteed to converge toward a nontrivial solution. Given a data set of multi-dimensional vectors and a predefined number of neurons (aka cluster centers), the topology learning neural algorithm cycles over random initialization of the neurons positions through the following steps:

- Randomly select a data vector.
- Move the neurons that are close to the selected data vector toward it.
- Add an edge with zero age between the two neurons that are the closest and closest ones. If such edge already exists, zero the age.
- Increase the ages of all existing edges by.
- Remove all edges with above some predefined threshold.

Depending on the data and the parameters for measuring closeness of neurons, adaption toward selected data points, and age threshold, the algorithms finds arbitrarily shaped clusters as connected components of the graph defined by neurons and the edges between them. However, it is obvious that trivial solutions—no edges except the most recently inserted ones—could appear, e.g, in case of too low age threshold.

An algorithm that is similar to the topology learning neural gas is combined with a visualization technique based on parallel coordinates [51]. In that algorithm the static data vectors take the role of neurons which is a special case of topology neural gas. The visual algorithm starts by drawing all data vectors in same color and same opacity into a parallel coordinates plot. It cycles through the following steps:

- Randomly select a data vector.
- Increase the opacity of complete polylines of the close neighbors of the selected data vector.
- Reduce the opacity of all data vectors by a given ratio.

Depending on the parameters, the algorithm produces a series of visualizations starting with a crowded parallel coordinates plot that fades during the run of the algorithm. Outliers, noise, and data vectors at the borders of clusters faster than data vectors to cluster center because the former are often less selected as neighbors, and therefore their opacity is less increased than the later ones. The user can reliably decide to stop the fading process when interested frames are visually selected. Alternatively, the full series of clusters as hierarchically nested clusters, larger clusters would show up first and then subclusters within larger clusters. Once a suitable visualization is found, the number of clusters needed for automatic processing can be determined. In the case that no clustering turns up in the visualization and the parallel coordinates plot just fades until all polylines have zero opacity, different parameters of the fading process could be.

## 19.3.2 Interactive Hierarchical Clustering

Three-dimensional projections of high-dimensional data are much less explored in information visualization than two-dimensional ones. One difficulty of three-dimensional projection is that points with different coordinates are plotted at the same position on two-dimensional screen. This ambiguity makes it difficult for the user to judge distances between points, and therefore clusters are less reliably detected. The ability to rotate the view helps the user to alleviate the ambiguity by identifying points with similar motion.

Another visual technique to turn three-dimensional visualizations into a useful tool for clustering is to use shapes that eagerly computed clusters [44]. The surfaces transform clusters from points to three-dimensional objects. The use of transparency, shading, and light reflection helps the user to resolve visual ambiguities in the visualization and to recognize the spatial extent of clusters. The goal of this approach is to produce distinguishable three-dimensional objects. The simplest approach that encompasses each cluster with a sphere or ellipsoid would produce visualizations with clusters that look uniform. Furthermore, details of the data distribution within a cluster could be deemphasized using only simple convex shapes. Therefore, a nonconvex shape—called BLOB—is constructed for each cluster by (1) placing spheres at border points of the cluster and (2) finding minimal radius of spheres that the cluster is still enclosed by the union of the spheres and the volume defined by that union does not break into disconnected regions. The method used in [43] does not guarantee finding the global
