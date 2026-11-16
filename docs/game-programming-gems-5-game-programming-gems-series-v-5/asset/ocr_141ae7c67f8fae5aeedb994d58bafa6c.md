| | | Leaf Index | |
|---|---|---|---|
| | | | L |

+   - L7 Specify if it's a node or a leaf.
+   - In this configuration, 31 bits are used for referencing the leaf, the last 4 bytes aren't used for the tree itself, but can store extra information (like for streaming words).

FIGURE 1.14.8 ABT trees leaf data representation.

# Performance

For analyzing the performance of this approach, three different implementations were used (see Figure 1.14.9):

+   - **Intuitive:** 6 * 4 bytes for storing the AABB and 8 bytes for the children's pointers (32-bit CPU), or 64 bytes for a couple.
+   - **Using redundancy:** 8 bytes for the AABB, 8 bytes for children's pointers, or 48 bytes per couple.
+   - **Cache-Oblivious (64 byte cache lines):** 8 bytes per couple + 8/7 extra bytes needed for implicit pointers, giving an average of 9.14 bytes, The global memory requirement depends on the tree balancing (see Figure 1.14.7).

![](bbox=[0.28, 0.57, 0.87, 0.9])

FIGURE 1.14.9 Memory usage across implementation. The memory consumption for the cache-oblivious depends on the tree's balancing.