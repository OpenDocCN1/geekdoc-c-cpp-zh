# 480 Appendix A Summary of Algorithmic Concepts

Parallelization—Quicksort, mergesort, and bucketsort can be parallelized.
External sorting—Because it moves through memory, mergesort performs external sorting well.

Counting—If items have a limited range, you may be able to count them instead of sorting them as countsort.

Partitioning—Bucketsort partitions items into buckets to simplify the problem.
Picking the right algorithm—Sorting algorithms provide a good example of when it is important to pick the right algorithm for the problem. Picking the right algorithm can mean the difference between solving a problem in seconds, minutes, or years.

# Chapter 7: Searching

A linear (exhaustive) search loops through all the possible items, looking for a target, giving it O(n) runtime. If the list is sorted, the algorithm can stop early if it passes the point where the item would be.

A binary search divides in half the area to be searched at each step, giving O(log n) runtime. This concept applies to many problems.

An interpolation search uses interpolation to guess where a target item is, giving it O(log n) runtime.

# Chapter 8: Hash Tables

Hashing requirements—Hashing requires a data structure to hold values, a hashing function to map values to the data structure, and a collision resolution policy.

Mapping—Hash tables use a hashing function to map values from one domain (names, employee IDs) to another domain (indices in an array). A good hashing function maps any input to a random distribution of output values.

Chaining—Using linked lists to hold bucket overflow.

Sorted counting—Sorting the linked lists improves performance in many algorithms.

Opening addressing—Mapping directly to arrays.
Marking items as deleted—Many data structures cannot easily remove items. Instead, you may be able to mark items as deleted and then reuse their spots later.

Clustering—In some algorithms, such as linear and quadratic probing, the probability of an item's landing in different places may not be equal. This can reduce the algorithm's efficiency.

Randomization—By randomizing data, you can sometimes avoid bad consequences.
Double hashing uses a second hash function to avoid clustering.

# Chapter 9: Recursion

Recursive metrics—For recursive algorithms, in addition to studying runtime and memory requirements, you must consider maximum depth of recursion and use of stack space.