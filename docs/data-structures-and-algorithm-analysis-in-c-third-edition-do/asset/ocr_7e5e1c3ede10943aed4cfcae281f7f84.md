# 13.3.4 Other Spatial Data Structures

This section has barely sketched the surface of the field of spatial data structures. Dozens of distinct spatial data structures have been invented, many with variations and alternate implementations. Spatial data structures exist for storing many forms of spatial data other than points. The most important distinctions are between the tree structure (binary or not, regular decompositions or not) and the decomposition rule used to decide when the data contained within a region is so complex that the region be subdivided.

One spatial data structure is the Region Quadtree for storing images where the pixel values tend to be blocky, as a map of the countries of the world. The region quadtree uses a four-way regular decomposition scheme similar to the PR quadtree. The decomposition rule is simple to divide any node containing pixels of more than one color or value.

Spatial data structures can also be used to store line object, rectangle object, or objects of arbitrary shape (as polygons in two dimensions or polyhedra in three dimensions). A simple, yet effective, data structure for storing rectangles or arbitrary polygonal shapes can be derived from the PR quadtree. Pick a threshold c, and subdivide any region into four quadrants if it contains more than c objects. A special case must be dealt with when more than c objects intersect.

Some of the most interesting developments in spatial data structures have to be done with adapting them for disk-based applications. However, all such disk-based implementations boil down to storing the spatial data within some variant on either B-trees or hashing.

# 13.4 Further Reading

PATRICIA and other trie implementations are discussed in Information Retrieval: Data Structures & Algorithms, Knuth and Baeza-Yates, eds. [FBY92]. See Knuth [Kn97] for a discussion of the AVL tree. For further reading on spray trees, see “Self-adjusting Binary Search” by Sleator and Tarjan [ST85].

The world of spatial data is rich and rapidly evolving. For a good introduction, see Multidimensional and Metric Data Structures by Hanan Samet [Sam06]. This is also the reference for more information on the PR quadtree. The k-tree was invented by John Louis Bentley. For information on the k-tree, in addition to [Sam06], see [Ben75]. For information on using a quadtree to store arbitrary polygonal objects, see [SH92].

For a discussion on the relative space requirements for two-way versus multilevel branching, see “A Generalized Comparison of Quadtree and Bint Storage Requirements” by Shaffer, Juvvadi, and Heath [SJH93].

Closely related to spatial data structures are data structures for storing multidimensional data (which might not necessarily be spatial in nature). A popular