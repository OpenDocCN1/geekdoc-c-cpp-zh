
Input Image

![](img/5f95dd954ac63cc68119f6f48ca99e18_195_0.png)

initial contour

![](img/5f95dd954ac63cc68119f6f48ca99e18_195_1.png)

2000 Iterations

![](img/5f95dd954ac63cc68119f6f48ca99e18_195_2.png)

Global Region-Based Segmentation

![](img/5f95dd954ac63cc68119f6f48ca99e18_195_3.png)

Figure 8.24 The original lion footprint image, the initial contour, the edges found by Chan-Vese, and the resulting segmentation. Matlab code from https://www.mathworks.com/matlabcentral/fileexchange/23445-chan-vese-active-contours-without-edges was used.

Input Image

![](img/5f95dd954ac63cc68119f6f48ca99e18_195_4.png)

initial contour

![](img/5f95dd954ac63cc68119f6f48ca99e18_195_5.png)

2000 Iterations

![](img/5f95dd954ac63cc68119f6f48ca99e18_195_6.png)

Global Region-Based Segmentation

![](img/5f95dd954ac63cc68119f6f48ca99e18_195_7.png)

Figure 8.25 The original color image of a stingray in sand, the initial contour, the final contour found by Chan-Vese, and the resulting segmentation. Matlab code from https://www.mathworks.com/matlabcentral/fileexchange/23445-chan-vese-active-contours-without-edges was used.

| 53 | 52 | 51 | 53 | 52 | 51 | 53 | 50 | 51 |
|---|---|---|---|---|---|---|---|---|
| 49 | 50 | 49 | 51 | 40 | 41 | 39 | 41 | 40 |
| 48 | 47 | 12 | 12 | 18 | 19 | 16 | 15 | 20 |
| 46 | 41 | 12 | 12 | 19 | 20 | 17 | 15 | 16 |
| 45 | 42 | 12 | 15 | 18 | 17 | 19 | 17 | 18 |
| 46 | 44 | 43 | 44 | 41 | 16 | 18 | 20 | 19 |

Figure 8.26 An image with three drains marked with shading, including the 5-pixel drain with brightness of 12, the 2-pixel drain with brightness of 15, and the 1-pixel drain with brightness of 16.

detector. This emphasizes the need for something additional. Perhaps a hybrid approach that could combine information from edges with region differences?

The concept introduced by Chan and Vese of describing the foreground (or interior) and the background (or exterior) by statistics continues to be a powerful idea. For example, Ramudu et al. [8.40] follow the same philosophy, but introduce a force (which they call an spf) equal to

```
spf(f(x, y)) = \frac{f(x, y) - \frac{1}{2}(\mu_1 + \mu_2)}{\max(f(x, y) - \frac{1}{2}(\mu_1 + \mu_2))} (8.60)
```

and show that using this force to move the contour often produces even better segmentations than Chan-Vese.

### 8.6 Watersheds: Segmentation Based on Brightness Surface

In this section, you will learn to think about moving up and down the brightness surface as water would move. We continue to consider the brightness function f(x, y) as if f represented vertical distance, and the brightness image is thought of as a surface.

Suppose we pour water onto that surface. Water runs downhill, and (assuming it isn't absorbed or evaporated) will eventually come to rest at some place that is a minimum of local elevation. In a digital (sampled and quantized) image, such a minimum is not necessarily a single pixel. It could be a set of neighboring pixels, all of which have the same brightness. We call that final, lowest set of points a drain. In general, there are many drains in an image. Given a single point (x, y) on the surface, place a single drop of water on the surface at that point, and follow it until it comes to rest at some drain. The collection of all surface points that flow to a single drain, say drain i, is referred to as the basin or catchment basin associated with that drain.

Some surprising problems occur when attempting to use basins to segment images. First, from a single point, water will flow in the direction of steepest slope, but it is certainly possible that there might be equal, steepest slopes in more than one direction. So the problem of tracking where that one drop of water flows could be challenging and have high computational complexity. But, instead of following water as it flows down, let's instead start at the drain, and find all the neighboring points that definitely flow into that drain. That calculation can be done locally. Then, we find the points that drain into those points, etc.

Figure 8.26 illustrates pixel brightnesses in the vicinity of a 5-pixel drain. Each pixel “looks at” its neighbors and says, “If you are my neighbor and are brighter than me, you

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

| 53 | 52 | 51 | 53 | 52 | 51 | 53 | 50 | 51 |
|---|---|---|---|---|---|---|---|---|
| 49 | 50 | 49 | 51 | 40 | 41 | 39 | 41 | 40 |
| 48 | 47 | 12 | 12 | 18 | 19 | 16 | 15 | 20 |
| 46 | 41 | 12 | 12 | 19 | 20 | 17 | 15 | 16 |
| 45 | 42 | 12 | 16 | 18 | 17 | 19 | 17 | 18 |
| 46 | 44 | 43 | 44 | 41 | 16 | 18 | 20 | 19 |

Figure 8.29 One more pass identifies all the basins and watersheds.

We emphasize that Γ+(q) is a set. Water at q can (and often will) go in multiple directions.

A point q is immediately upstream of p if p ∈ Γ+(q), and the set of immediately upstream points of p will be

Γ+(p) = {q | p ∈ Γ+(q)}. (8.61)

Examining Eq. 8.61, one observes that two searches are required to determine if q ∈ Γ+(p). First, find all the points q that are neighbors of p. Then, for each of those, determine if p is downstream of that q.

With the notation clarified, the segmentation algorithm is fairly straightforward:

- Find all the drains in an image, and construct a label image (see section 8.1) in which all the labels of a particular drain are identical, and are distinct from all other labels.
- Determine a structure containing every point in the image that is not the interior of a drain. Call that set V.
- Search V to find a point with minimum brightness and call that point p. (Initially, p will be an exterior point of a drain). Give p the label of that drain.
- Remove p from V.
- For all points q ∈ Γ+(p) that remain in V:
  - if q is not labeled, assign q the same label as p
  - if q is labeled and has a different label from p, give q a label indicating it is a pixel on the boundary of two basins (a watershed).
- If V is not empty, go back to step 3.

Step 4 has the effect of making the search in step 3 increasingly faster as the process continues.

A problem arises in this algorithm if plateaus exist. Plateaus are local collections of adjacent pixels that are equal in brightness, but have boundary pixels both greater or lesser in brightness. Such regions might not be local minima, since they could have neighboring pixels lower in brightness. To allow the algorithm above to work properly, an image must be distorted in such a way as to make the image lower complete. In a lower complete image, every non-minimum pixel has a lower neighbor. See [8.42] for an algorithm to make any image lower complete.

The observant student will notice that in Figures 8.26-8.29, there are no plateaus that are not minima. That is, this example was deliberately chosen to be a lower complete image.
