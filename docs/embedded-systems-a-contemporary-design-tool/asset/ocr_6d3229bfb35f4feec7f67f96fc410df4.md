# 4.18 CACHING – AN ASSOCIATIVE MAPPING CACHE IMPLEMENTATION

Although simple, the direct mapped algorithm can have some negative effects on system performance, particularly if real-time constraints must be satisfied. It is easy to imagine a situation in which different portions of an algorithm are in different blocks 0’s in main memory. In such a circumstance, the two blocks would be repeatedly interchanged.

An alternative approach lets a new block be placed anywhere in the cache. An **associative search** is then executed to locate it. Such an algorithm searches by content rather than by address. The associative search asks, “given a target, is it in memory and if so, where?” The traditional access says, “here is an address; return the contents of that address.”

A mapping from main memory may now appear as illustrated in Figure 4.38.

![](bbox=[0.28, 0.27, 0.82, 0.63])

Figure 4.38 Mapping from Main Memory to Cache Memory

A new main memory block can be placed anywhere in the cache. As with the direct mapping algorithm, the tag table entry corresponding to the cache block will contain the address information identifying the main memory origin. However, a linear search of the tag table to locate a required block is not feasible.

A cache miss using an associative mapping scheme is handled in much the same way as was done in the direct mapping scheme. The two differ in how the new block is brought into the cache and in which block is to be replaced. As the new block is not constrained to a specific location, replacement offers more opportunities and becomes a bit more interesting. Any of three schemes is commonly used. Each has advantages and disadvantages; the choice for implementation is often governed by the requirements of the application.

+   **Least Recently Used (LRU) Most Recently Used (MRU)**

With an associative mapping algorithm, time is added as one of the components of the tag record. Two of the more commonly used algorithms applying temporal locality of reference as a metric are Least Recently Used (LRU) and Most Recently Used (MRU).