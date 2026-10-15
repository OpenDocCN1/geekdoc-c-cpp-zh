![](bbox=[0.12, 0.18, 0.35, 0.48])

![](bbox=[0.38, 0.12, 0.82, 0.45])

![](bbox=[0.86, 0.14, 0.96, 0.42])

# FIGURE 7.17

(a) 2-map.
(b) Its embedding in the interpixel matrix.
(c) Some links between darts and pairs (p,l).

with a pointel (darts belonging to the same vertex are necessarily associated with the same pointel). Edge embedding can be retrieved by iterating through true linels starting from the initial linel given by the pair (p,l), and following the true linels until obtaining either a true pointel or the initial linel (when the frontier is a cycle). At last, region embedding can be retrieved starting from a pixel inside the region, and applying a flood fill algorithm stopped by true linels. The initial pixel is retrieved thanks to the pair (p,l) associated with the external boundary of the region and taking into account that this boundary is oriented clockwise.

The model composed with the 2-map describing the 2D labeled image, together with the enclosure tree of regions, and its embedding in the interpixel matrix is called 2D topological map. Using these three components, it is possible to conceive efficient high level operations of 2D image processing.

# 7.3.3 Operations

# 7.3.3.1 Topological Map Construction

The first operation defined is the construction of a 2D topological map from a 2D labeled image. Algorithm 75 implements an incremental solution, which mainly consists in iterating through all the pixels of the image line by line, in creating a square associated with the current pixel and, depending on the local configuration, in removing the two edges to the left and to the up of the current pixel and the vertex to the left and up corner of this pixel. During the scan line of the image, last denotes the dart to the left of the current pixel and up the dart to the up. An important invariant is the fact that the 2-map describing the pixels smaller than the current pixel (according to lexicographic order) is already build. This invariant is required to 2-sew the square corresponding to the current pixel to the former 2-map.