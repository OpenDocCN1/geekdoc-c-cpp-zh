![](bbox=[0.141, 0.094, 0.581, 0.239])

**Figure 11.2** The cache manager’s view of RAM. Each 128-B cache line is read into one of four lines in cache.

For systems that use a data cache, this may well be the single most important programming consideration; continually referencing data that are not in the cache (*cache misses*) may lead to an order-of-magnitude increase in CPU time.

As indicated in Figures 10.3 and 11.2, the data cache holds a copy of some of the data in memory. The basics are the same for all caches, but the sizes are manufacturer dependent. When the CPU tries to address a memory location, the *cache manager* checks to see if the data are in the cache. If they are not, the manager reads the data from memory into the cache, and then the CPU deals with the data directly in the cache. The cache manager’s view of RAM is shown in Figure 11.2.

When considering how a matrix operation uses memory, it is important to consider the *stride* of that operation, that is, the number of array elements that are stepped through as the operation repeats. For instance, summing the diagonal elements of a matrix to form the trace

$$\operatorname{Tr} A = \sum_{i=1}^{N} a(i,i) \tag{11.7}$$

involves a large stride because the diagonal elements are stored far apart for large $N$. However, the sum

$$c(i) = x(i) + x(i+1) \tag{11.8}$$

has stride 1 because adjacent elements of $x$ are involved. Following is the basic rule in programming for a cache:

+   - Keep the stride low, preferably at 1, which in practice means:
+     - Vary the leftmost index first on Fortran arrays.
+     - Vary the rightmost index first on Python and C arrays.