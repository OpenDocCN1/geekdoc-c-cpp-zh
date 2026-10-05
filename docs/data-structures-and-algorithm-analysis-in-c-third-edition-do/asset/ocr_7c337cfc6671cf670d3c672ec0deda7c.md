# 456

Chap. 13 Advanced Tree Structures

| | 0 | 127 |
|---|---|---|
| 0 | | C | nw sw se |
| | A | | B (40,45) (15,70) |
| | B | D | C D (70,10) (69,50) |
| | | E F | E F (55)(80,90) |

**Figure 13.16 Example of a PR quadtree.** (a) A map of data points. We define the region to be square with origin at the upper-left-hand corner and sides of length 128. (b) The PR quadtree for the points in (a). (a) also shows the block decomposition by the PR quadtree for this region.

than a single point. In other words, if a region contains zero or one data points, then it is represented by a PR quadtree consisting of a single leaf node. If the region contains more than a single data point, the region is split into four quadrants. The corresponding PR quadtree then contains an internal node and four subtrees, each subtree representing a single quadrant of the region, which in turn be split into subarrays of the two-dimensional region. The four quadrants of the region (or equivalently, the corresponding subtrees) are designated (in order) NW, NE, SW, and SE. Each quadrant containing more than a single point would be recursively divided into subquadrants until each leaf of the corresponding PR quadtree contains at most one point.

For example, the region of Figure 13.16(a) and the corresponding PR quadtree in Figure 13.16(b). The decomposition process fixes a key range. In example, the region is assumed to be of size 128 × 128. Note that the internal nodes of the PR quadtree are used solely to decompose the region; internal nodes do not store data records. Because the decomposition lines are predetermined (i.e., key-space decomposition is used), the PR quadtree is a trie.

Search for a record point Q in the PR quadtree is straightforward. Beginning at the root, we continuously traverse the data contains Q until our search reaches a leaf node. If the root is a leaf, then check to see if the node's data records match point Q. If the root is an internal node, proceed to the child that contains the search coordinate. For example, the NW quadrant of Figure 13.16 contains points whose x and y values fall in the range 0 to 63.