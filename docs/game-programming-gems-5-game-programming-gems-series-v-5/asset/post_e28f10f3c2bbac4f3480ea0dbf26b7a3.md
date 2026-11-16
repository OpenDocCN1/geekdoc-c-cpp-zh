
## An Effective Cache-Oblivious Implementation of the ABT Tree

Sébastien Schertenleib, Swiss Federal Institute of Technology (EPFL), Virtual Reality Lab (VRlab)
Sebastien.Schertenleib@epfl.ch

Today, computer architectures describe multiple levels of memory becoming successively slower and larger. Those levels include registers, level-1 cache, level-2 cache, main memory, and disk. The access time increases from one cycle for registers to around 10, 100, and 100,000 cycles for cache, main memory, and disk, respectively (see Figure 1.14.1). According to the current and future CPUs and memory evolutions [Moore65], [Hennessy03], the penalty for algorithms that do not take benefit of this hierarchical memory representation will increase through many caches misses. For addressing this problem, cache-oblivious algorithms were introduced by [Frigo99]. The idea was to optimize the I/O model’s scheme without specific knowledge about the memory block size. They describe that basic problems can be solved using optimal algorithms being cache-oblivious [Frigo99]. First attempts were dedicated to matrix and FFT transformation. Later, [Bender00] gives additional proposals for B-tree and search tree representation. Cache-oblivious algorithms differ from cache-aware algorithms, as they adapt themselves to any architecture.

## Computer Memory Architecture

Most algorithms ignore memory architecture. Those driven by small data structures like binary trees suffer huge penalties in accessing their data. Each memory layer works in a similar fashion and is composed of cache blocks. Current architectures use cache lines of approximately 32–64 bytes. Notable improvement can be achieved by accessing data within the same cache line [Patterson97], [Hennessy03]. A cache line’s lifetime depends on hardware-specific heuristics [Smith87]. Decisions are made on a

![](img/672fe9a2d008ba627b1991e15d70f43e_201_0.png)

replacement and associative policy within the cache. Sometimes, cache misses are unavoidable [Hill02] such as in the following cases:

- **Compulsory**: A cache miss cannot be avoided; this occurs when some data is accessed for the first time.
- **Capacity**: The data fit in the cache in previous steps, but due to the renewal policy of the cache, the data was removed from this cache level.
- **Conflict**: Cache trashing due to data mapping to the same cache lines.

## Data Structure and Cache Coherence

Spatial alignments have an impact on the cache usage. Notably, data structures making intensive use of pointers are not good candidates. Pointers or data that will be accessed together should as well be stored together for optimizing memory access [Ericson03], [Ding04]. In some circumstances, they may not fulfill the object-oriented programming methodology.

## Van Emde Boas Layout

The van Emde Boas layout [van Emde Boas77] (see Figure 1.14.2) is the standard way of laying out a balanced tree in memory so that a root-leaf path can be traversed efficiently in the cache-oblivious model using O(4 * log_b(n)) B = NbElement/Cache Line memory transfers [Agarwal03].

![](img/672fe9a2d008ba627b1991e15d70f43e_201_1.png)

## ABT Tree

ABT trees are very similar to KD trees [Szécsi03]. At each step, two children may be created based on an axis-aligned splitter. One difference with KD trees is that the algorithm will minimize the resulting children’s AABBs and store all the geometry exclusively in the leaves. Thus, each node becomes a totally enclosed region in space where the internal nodes are used for rejecting the traversal of nonvisible parts of the environment.

### ABT Tree Creation

The creation of such a tree begins with the root node containing a reference to the whole scene AABB. The recursive building method subdivides the local current AABB into two parts along an axis-aligned splitter. Then, each face is assigned to one child depending on their median (see Figure 1.14.3).

![](img/672fe9a2d008ba627b1991e15d70f43e_202_0.png)

Once the distribution of all faces has occurred, each child recomputes its own AABB containing unique faces on this level. The ending criterion depends on the specific 3D environments and hardware envisaged. The splitting policy will try to minimize the following attributes:

- Space localization, as in Equation 1.14.1:
  
  \( f_1(n) = Min(Area(boxLeft) + Area(boxRight)) \quad (1.14.1) \)

- Tree balancing, as in Equations 1.14.2 and 1.14.3:
  
  \( f_2(n) = Min[\Delta(Area(boxLeft) - Area(boxRight))] \quad (1.14.2) \)
  
  \( f_3(n) = Min[\Delta(\Sigma(ExtendedArea) - \Sigma(Area))] \le \varepsilon \quad (1.14.3) \)

- Epsilon should stay below 5–10% before a noticeable performance penalty. In most cases, 90% of the faces will be contained in this 5% extended AABB

Scene complexity, as in Equations 1.14.4 and 1.14.5:

\( f_4(n) = Min[\Delta(\sum faces(boxLeft) - \sum faces(boxRight))] \quad (1.14.4) \)

\( f_5(n) = Min[\Delta(\int resources(boxLeft)dt - \int resources(boxRight)dt)] \quad (1.14.5) \)

The final equation becomes that shown in Equation 1.14.6:

\( f(n) = w_1 * f_1(n) + w_2 * f_2(n) + w_3 * f_3(n) + w_4 * f_4(n) + w_5 * f_5(n) \quad (1.14.6) \)

The weights will change during the traversal with regard to the engine bottlenecks and scene organization (scenegraph, special effects, etc.). The methodology will also differ for the preprocessing stage and during runtime.

At runtime, typically each point of view will do a full or partial traversal during the different rendering phases (culling, shadow, collision detection, etc.). Thankfully, ABT-tree traversals are really simple and fast to compute. Starting from the last local root, the recursive function tests if either of the two children is in the frustum and if so, continues the tree traversal. When a leaf is reached, all geometry contained can be sent to the next stage in the rendering pipeline. Since each face is unique, no additional tests are needed (like for collision detection). We can also keep a small vertex buffer by leaf and local materials. For reducing the number of vertex buffers used, we can benefit from the neighbor child's location. Therefore, a single vertex buffer could be shared within their limits (generally 65K of 16-bit indices) among leaves. This provides a more efficient branching when neighbors need to be proceeding altogether, improving the rendering performance [Wloka03].

ABT-trees can also be tuned dynamically by simply reordering each moving AABB among their subtrees. One downside with dynamic trees is that they tend to degenerate with time.

## Efficiency

All binary trees, notably BSP and KD trees, suffer from depth level. Even with ABT trees' abilities, it remains a significant issue. Assuming that the tree implementation is using pointers instead of implicit pointers, we can consider that every time the tree needs to follow a pointer, a CPU cache misses will occur. Relative to the depth level, the number of caches misses will increase accordingly up to a limit where they become more expensive than testing intersections. However, cache-oblivious trees reduce cache misses relative to the cache line size. The traversal then becomes less sensitive to memory access rather than CPU performance.

## Complexity

ABT trees, like all binary trees, have an O(log n) search time [Sedgewick90]. By using the van Boas cache-oblivious layout representation, the search time can be majored to O(4 * log_b(n)) where B = CoupleNodesByCacheLines [Brodal03] (see Figure 1.14.4).

![](img/672fe9a2d008ba627b1991e15d70f43e_204_0.png)

FIGURE 1.14.4 Searching time order.

Each node needs to store its local AABB and a pointer (or index) to its two children. Using a naïve implementation, the memory consumption becomes relatively important:

- AABB described by six floating-point values: 6 * 4 bytes
- Pointers to its two children: 2 * 4 bytes (32-bit CPU) or 2 * 8 bytes (64-bit CPU)

Total memory requirement per node is therefore 32 bytes (32-bit CPU) or 40 bytes (64-bit CPU).

However, [Gomez01] has shown that we only need to keep the relative extents for each child, which can be truncated to an 8-bit integer value. This conservative estimate will have a relative error of 1/255, or approximately 0.4%, which is covered by the average 5–10% AABB overlapping.

## Exploiting Redundancy

[Gomez01] has described practical ways for reducing the memory footprint. At each subdivision, 6 extents from the 12 defining the children's AABB come directly from
