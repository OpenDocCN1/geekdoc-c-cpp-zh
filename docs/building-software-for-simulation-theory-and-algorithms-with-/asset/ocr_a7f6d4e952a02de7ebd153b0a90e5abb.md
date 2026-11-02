![](bbox=[0.18, 0.12, 0.83, 0.38])

**FIGURE 4.10** Maximum number of compare and swaps required by *percolate_up* and *percolate_down* as a function of the number of models in the heap. The x axis has a logarithmic scale; the heap’s ability to manage a large number of models is readily apparent.

use < and so it is important to keep in mind this peculiar requirement of our event schedule (see, e.g., Weiss' *Data Structures and Algorithm Analysis in C* [145]).^5

The time required to place a model in or remove a model from the heap is determined chiefly by the *percolate_up* and *percolate_down* methods. The number of iterations of the *for* loops of these methods is, at most, equal to the height of the heap. If it holds *N* atomic models, then the height is at most ⌊log₂ *N*⌋. This is deduced by first observing that the number of nodes in a heap of height *h* is between 2^h and 2^{h+1} − 1 (a heap with a single element has a height of zero), that is, that *N* ∈ [2^h, 2^{h+1} − 1]. For a given *N*, the smallest integer value of *h* that satisfies this expression is ⌊log₂ *N*⌋, and hence the bound on the execution time.

To insert or move a model within the heap requires one call to *percolate_up* or *percolate_down*, and so the cost of an insertion or adjustment is bounded by ⌊log₂ *N*⌋. To remove a model requires one call to *percolate_up* and a second call to *percolate_down*, and so it is twice as expensive as an insertion or adjustment. Nonetheless, the heap's operations in general have an execution time proportional to ⌊log₂ *N*⌋, which is plotted Figure 4.10.

The only exception to this rule is the *enlarge* method. Its time is spent chiefly in allocating a new array, copying the old array to the new, and then deallocating the old. The memory allocation is itself quite slow, and compounding this are the memory assignments required to transfer the array contents. Fortunately, the heap is very rarely enlarged. In a long-running simulation, *enlarge* is called early to grow the heap to some size that is generally smaller than *N*, and calls later in the run are

⁵ Another solution is to use −1, or some other time of next event that is invalid, to remove a model from the heap. This requires that the sentinel value be less than −1, or whatever other value is used for removal.