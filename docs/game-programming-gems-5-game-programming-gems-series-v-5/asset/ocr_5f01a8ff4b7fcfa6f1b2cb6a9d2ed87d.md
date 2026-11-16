![](bbox=[0.35, 0.08, 0.78, 0.24])

replacement and associative policy within the cache. Sometimes, cache misses are unavoidable (Hil|02) such as in the following cases:

+   - **Compulsory**: A cache miss cannot be avoided; this occurs when some data is accessed for the first time.
+   - **Capacity**: The data fit in the cache in previous steps, but due to the renewal policy of the cache, the data was removed from this cache level.
+   - **Conflict**: Cache trashing due to data mapping to the same cache lines.

# Data Structure and Cache Coherence

Spatial alignments have an impact on the cache usage. Notably, data structures making intensive use of pointers are not good candidates. Pointers or data that will be accessed together should as well be stored together for optimizing memory access [Ericson03], [Ding04]. In some circumstances, they may not fulfill the object-oriented programming methodology.

# Van Emde Boas Layout

The van Emde Boas layout [van Emde Boas77] (see Figure 1.14.2) is the standard way of laying out a balanced tree in memory so that a root-leaf path can be traversed efficiently in the cache-obliviously model using O(4 * log_b(n)) B = NbElement/Cache Line memory transfers [Agarwal03].

![](bbox=[0.2, 0.73, 0.9, 0.96])