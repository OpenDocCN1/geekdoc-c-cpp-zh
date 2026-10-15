these models [29, 126] (see Fig. 7.13). For example, a well can be drilled in the geological basement by applying the corefining operation (see Fig. 7.14).

# 7.3 Image Processing

*n*-Gmaps and *n*-maps can be used to describe partitions of labeled images into regions and thus efficient image processing algorithms can be conceived. This fits into **structural image processing** methods, as *n*-Gmaps and *n*-maps can be considered as natural extensions of graphs for describing regions of labeled images. Indeed, in 2D, a 2-map or a 2-Gmap is a representation of a planar graph.

# 7.3.1 Preliminary Notions

Each pixel of a 2D image is associated with a *label*, a value from a finite set of labels. Two pixels $(x,y)$ and $(x',y')$ are 4-adjacent if $|x-x'|+|y-y'|=1$, i.e. the two pixels share one edge of their boundaries. Two different pixels $(x,y)$ and $(x',y')$ are 8-adjacent if $\max(|x-x'|,|y-y'|)=1$, i.e. the two pixels share either an edge or a point of their boundaries. A list of pixels is a *k*-path (with $k=4$ or 8) if each pair of successive pixels in the path are *k*-adjacent. A set of pixels is *k*-connected if any pair of pixels of the set are linked by a *k*-path of pixels of the set. A *region* in a labeled image is a maximal set of 4-connected pixels having the same label. A lexicographic order exists on pixels: $(x,y)<(x',y')$ if $x<x'$ or $(x=x'$ and $y<y'$). This order is extended on regions: $R_i<R_j$ if $\min(R_i)<\min(R_j)$, $\min(R)$ being the minimal pixel of region $R$.

These notions are illustrated in Fig. 7.15(a). Pixel a is 4-adjacent to pixels b, c, d and e, and 8-adjacent to pixels b, c, d, e, f, g, h and i. There are 6 regions in this image, labeled from $R_1$ to $R_6$. An additional region is considered, labeled $R_0$ and called the infinite region, which is the complementary of the image.

The *interpixeI framework* [145, 143, 146, 141, 142] refers to pixels, linels which are unit segments separating each pair of 4-adjacent pixels and pointels which correspond to the extremities of linels (cd. Fig. 7.15(b)). Mainly, the interpixeI framework make it possible to define a topology for 2D images, similar to the classical topology. For instance, curves can be defined as particular sets of linels and pointels, and properties can be defined, similar to that of curves in Euclidean space.

Given a 2D labeled image, it is often necessary to describe the regions and the different adjacency relations between these regions. Indeed, this information is required by many image processings, such as region merging used in bottom-up segmentation algorithms. The first data structure proposed to