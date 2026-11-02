space without actual distance computation. A fast k-NN search algorithm by reducing the distance based on the structure is described. Consider the following sample data set:

1: (1, 2, 5), 2: (3, 8, 7), 3: (9, 10, 8), 4: (12, 9.2), 5: (8, 7, 20), 6: (6.6,23), 7: (0, 3, 27), 8: (2, 13.9), 9: (11, 11, 15), 10: (14, 17, 13), 11: (7, 14, 12), 12: (10, 12, 3).

As far as the first partition is concerned, we partition the points into three regions, R1(-∞, 3), R2(3, 6), R3(6, +∞).

R1 is partitioned into subregions R1,1(-∞, 2), R1,2(2, 8), R1,3(8, ∞); R2 is partitioned into subregions R2,1(-∞, 4), R2,2(4, 7), R2,3(7, +∞); and R3 is partitioned into subregions R3,1(-∞, 9), R3,2(9, 12), R3,3(12, +∞).

We next specify the points held by the partitions

R1,2(1); R2,1(2, 7); R3,1(8); R2,1(11); R2,2(5, 6); R2,3(3); R3,1(4); R3,2(12), (9); and R3,3(10).

The building of a persistent semi-dynamic OP-tree index is presented in References 74 and 75. We use serialization to compact the dynamically allocated nodes of the OP-tree in the main memory, which form linked lists, into a contiguous area. The index can then be saved onto disk as a single file and loaded into the main memory with a single data transfer. This is because disk positioning time to load the index one page at a time is high and is improving at a very slow rate, while the improvement in disk transfer rates is significant [11]. The prefetching effect of modern operating systems results in the loading of the whole index into the main memory in experimental studies with small indices. The original OP-tree is static, in which case the OP-tree has to be rebuilt in the main memory as new points are added. We propose and compare the performance and space efficiency of several methods, which support inserting points dynamically.

The SDI index uses a reduced number of dimensions at the higher levels of the tree to increase the fan-out, so that the tree height is reduced [100]. The number of dimensions increases level by level, until full dimensionality is attained at the lower levels. The SDI index differs from the Δ-tree in that it is a disk-resident index structure with fixed node sizes, while the Δ-tree is a main memory-resident index with variable node sizes and fixed fan-outs. The SDI-tree differs from the TV-tree in that it uses a single parameter, specifying the fraction of variance to be added to each level, without the risk of having a large number of active dimensions.

SDI trees are compared to variance approximate median (VAM) SR-trees and the VA-file indexes in Reference 100. The VAMSR-tree uses the same split algorithm as the VAMSplit R-tree [101], but it is based on an SR-tree structure, which is statically built in a bottom-up