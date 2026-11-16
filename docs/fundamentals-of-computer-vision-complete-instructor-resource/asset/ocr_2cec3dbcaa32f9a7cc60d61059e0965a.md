| 53 | 52 | 51 | 53 | 52 | 51 | 53 | 50 | 51 |
|---|---|---|---|---|---|---|---|---|
| 49 | 50 | 49 | 51 | 40 | 41 | 39 | 41 | 40 |
| 48 | 47 | 12 | 12 | 18 | 19 | 16 | 15 | 20 |
| 46 | 41 | 12 | 12 | 19 | 20 | 17 | 15 | 16 |
| 45 | 42 | 12 | 15 | 18 | 17 | 19 | 17 | 18 |
| 46 | 44 | 43 | 44 | 41 | 16 | 18 | 20 | 19 |

Figure 8.27 Each pixel in the drain examines all of its neighbors (in this example, 4-connectedness is used). Any neighboring pixel that is brighter than the drain pixel is labeled as belonging to the same basin. The first drain to be processed is the darkest.

belong to my basin, unless you already belong to a different basin, but if you belong to a different basin already, you are a watershed pixel.” This assigning of labels to pixels may remind one of connected components, but an important difference is that here, pixels are sorted by brightness before making a neighborhood decision.

The watershed-based segmentation problem may be cast as finding the basin to which each point in the image belongs.

As each basin fills with water, at some points the water level will be so high that water from two neighboring basins may mix. The locus of points along which this happens is called the watershed lines or just watershed.

This is illustrated in a simple example in Figures 8.26–8.29, showing steps in developing the watershed-based segmentation of a simple example image. This set of figures starts identifying three minima in the first image, which are the initial drains.

There are a variety of ways to compute watersheds on discrete, sampled data. Researchers have learned that watershed methods frequently must be adjusted slightly to cope with peculiarities of data. For example, a lot of noise will create thousands of tiny, uninteresting watersheds. Here, we present the approach provided in Algorithm 4.3 of [8.42]. We present the algorithm first, and then discuss a critical assumption. First, some definitions are presented:

A point p is immediately downstream of a point q if p and q are neighbors, and if the slope (f(q)−f(p)) is maximal over the set of neighbors. Here, d(p, q) is the distance between p and q. If using 4-connected neighborhoods, d will always be 1.0. The set of points pq = {p1, p2, ...}, which are immediately downstream of q are denoted Γ+(q), and we use the notation p ∈ Γ+(q) to denote that p is immediately downstream of q. A point p1 is downstream of pn if there is a path of points (p1, p2, ..., pn) where pi ∈ Γ+(pi+1) ∀i.

| 53 | 52 | 51 | 53 | 52 | 51 | 53 | 50 | 51 |
|---|---|---|---|---|---|---|---|---|
| 49 | 50 | 49 | 51 | 40 | 41 | 39 | 41 | 40 |
| 48 | 47 | 12 | 12 | 18 | 19 | 16 | 15 | 20 |
| 46 | 41 | 12 | 12 | 19 | 20 | 17 | 15 | 16 |
| 45 | 42 | 12 | 15 | 18 | 17 | 19 | 17 | 18 |
| 46 | 44 | 43 | 44 | 41 | 16 | 18 | 20 | 19 |

Figure 8.28 Pixels are chosen in order of brightness, and the process of examining neighbors repeats. In this pass, several pixels are identified as belonging to two basins, and hence are marked (in orange) as watershed pixels.