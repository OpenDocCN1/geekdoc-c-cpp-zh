
## Sec. 13.3 Spatial Data Structures

![](img/0ae21f56d72533acf0527c86ba21e1e6_473_0.png)

**Figure 13.14** Searching in the k-d tree of Figure 13.11. (a) The k-d tree decomposition for a $128 \times 128$-unit region containing several data points. (b) The k-d tree for the region of (a).

```cpp
// Print all points within distance "rad" of "coord"
void regionhelp(BinNode* root, int* coord,
	int rad, int discrim) const {
	if (root == NULL) return; // Empty tree
	// Check if root is in circle
	if (InCircle(root->val(), coord, rad)) {
		int count = (root->val())->coord(coord, rad); // Do what is appropriate
		int* curcoord = (root->val())->coord();
		if (curcoord[discrim] > (coord[discrim] - rad))
			regionhelp(root->left(), coord, rad, (discrim+1) % D);
		if (curcoord[discrim] < (coord[discrim] + rad))
			regionhelp(root->right(), coord, rad, (discrim+1) % D);
	}
}
```

**Figure 13.15** The k-d tree region search method.

Figure 13.15 shows an implementation for the region search method. When a node is visited, function **InCircle** is called to check the Euclidean distance between the node's region and the query point. It is not enough to simply check that the differences between the $x$- and $y$-coordinates are each less than the query distances because the record could still be outside the search circle, as illustrated by Figure 13.1.

### 13.3.2 The PR quadtree

In the Point-Region Quadtree (hereafter referred to as the PR quadtree) each node either has four children or is a leaf. That is, the PR quadtree is a full four branching (4-ary) tree. The PR quadtree represents a collection of data points in two dimensions by decomposing the region containing the data points into four equal quadrants, subquadrants, and so on, until leaf node contains more than a single point.

| | 0 | 127 |
|---|---|---|
| 0 | | C | nw sw se |
| | A | | B (40,45) (15,70) |
| | B | D | C D (70,10) (69,50) |
| | | E F | E F (55)(80,90) |

**Figure 13.16** Example of a PR quadtree. (a) A map of data points. We define the region to be square with origin at the upper-left-hand corner and sides of length 128. (b) The PR quadtree for the points in (a). (a) also shows the block decomposition by the PR quadtree for this region. In other words, if a region contains zero or one data points, then it is represented by a PR quadtree consisting of a single leaf node. If the region contains more than a single data point, the region is split into four quadrants. The corresponding PR quadtree then contains an internal node and four subtrees, each subtree representing a single quadrant of the region, which in turn be split into subarrays of the two-dimensional region. The four quadrants of the region (or equivalently, the corresponding subtrees) are designated (in order) NW, NE, SW, and SE. Each quadrant containing more than a single point would be recursively divided into subquadrants until each leaf of the corresponding PR quadtree contains at most one point.

For example, the region of Figure 13.16(a) and the corresponding PR quadtree in Figure 13.16(b). The decomposition process fixes a key range. In example, the region is assumed to be of size 128 × 128. Note that the internal nodes of the PR quadtree are used solely to decompose the region; internal nodes do not store data records. Because the decomposition lines are predetermined (i.e., key-space decomposition is used), the PR quadtree is a trie.

Search for a record point Q in the PR quadtree is straightforward. Beginning at the root, we continuously traverse the data contains Q until our search reaches a leaf node. If the root is a leaf, then check to see if the node's data records match point Q. If the root is an internal node, proceed to the child that contains the search coordinate. For example, the NW quadrant of Figure 13.16 contains points whose x and y values fall in the range 0 to 63.

| | | |
|---|---|---|
| | ●C | |
| ●A | | ●A |
| ●B | | ●B |
| (a) | | (b)|

**Figure 13.17** PR quadree insertion example. (a) The initial PR quadree containing two data points. (b) The result of inserting point C. The block containing A must be decomposed into four sub-blocks. Points A and $C$ would still be in the same block if only one subdivision takes place, so a second decomposition is required to separate them.

NE quadrant contains points whose $x$ value falls in the range 64 to 127, and $y$ value falls in the range 0 to 63. If the root's child is a leaf node, then that node is checked to see if $Q$ has been found. If the child is an internal node, the search process continues through the tree until a leaf node is found. If this leaf node stores a record whose matches $Q$ then the query is successful; otherwise $Q$ is not in the tree.

Inserting $P$ into the PR quadree is performed by first locating the leaf node that contains the location of $P$. If this leaf is empty, $P$ is stored at this leaf. If the leaf already contains $P$ (or a record with $P$'s coordinates), a duplicate record should be reported. If the leaf node already contains another record, the node must be repeatedly decomposed until the existing record and $P$ fall into different leaf nodes. Figure 13.17 shows an example of such an insertion.

Deleting a record $P$ is performed by first locating the node $N$ of the PR quadree that contains $P$. $N$ is then changed. The next step is to look at $N$'s three siblings, and $N$ and its siblings must be merged to form a single node $N'$ if only one point is contained among them. This merging process continues until some level is reached where at least two points are contained in the subtrees represented by $N'$ and its siblings. For example, if $C$ is to be deleted from the PR quadree representing Figure 13.17(b), the resulting node must be merged with its siblings, and that larger node again merged with its siblings to restore the PR quadree to the decomposition of Figure 13.17(a).

Region search is easily performed with the PR quadree. To locate all points within radius $r$ of query point $Q$, begin at the root. If the root is an empty leaf node, no do data points are found. If the root is a leaf containing a data record, the location of the data point is examined to determine if it falls within the circle. If the root is an internal node, then the process is performed recursively, but only on those subtrees containing part of the circle.

Let us consider how the PR quadtree affects the design of its node. The PR quadtree is actually a tri (defined in Section 3.1). Decomposition takes place at the mid-points for internal nodes, regardless of where the data points actually fall. The placement of data points determines whether a decomposition for a node takes place, but not where. Internal nodes of the quadtree are quite different from leaf nodes, in internal nodes have children (leaf nodes do not) and leaf nodes have data fields (do not). Thus, it is likely to be beneficial to represent internal nodes differently from leaf nodes. Finally, there is the fact that approximately half of the leaf nodes will contain no data field. Another possibility is to pass the coordinates in the recursive call. For example, consider the search process. Initially, the search visits the root node of the tree, which has origin at (0, 0), and whose width is the full size of the space being covered. When the appropriate child is visited, it is a simple matter for the search routine to determine the origin for the child, and the width of the square is simply half of the part. Not only passing in the size and position information for a node save considerable space, but avoiding storing such information in the nodes enables a good design choice for leaf nodes, as discussed next.

How should we represent leaf nodes? On average, half of the leaf nodes in a PR quadtree are empty (i.e., not store a data point). One implementation option is to use a NULL in internal nodes to represent empty nodes. This will solve the problem of excessive space requirements. A NULL pointer requires the PR quadtree processing methods to understand this convention. In other words, you are breaking encapsulation on the node representation because the tree now must know things about how the nodes are implemented. This is not too horrible for this particular application, because the node class can be considered private to the tree class, in which case the node implementation is completely invisible to the outside world. However, it is undesirable if there is another reasonable alternative. Fortunately, there is a good alternative. It is called the Flyweight design pattern. In the PR quadtree, a flyweight is a single leaf node that is reused in all places where an empty leaf node is needed. You simply have all of the internal nodes with
