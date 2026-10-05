# CHAPTER
17
Complexity Theory

An algorithm’s performance is always important when you try to solve a problem. An algorithm won't do you much good if it takes too long or requires too much memory or other resources to actually run on a computer.

Computational complexity theory, or just complexity theory, is the closely related study of the difficulty of computational problems. Rather than focusing on specific algorithms, complexity theory focuses on problems.

For example, the mergesort algorithm described in Chapter 6 can sort a list of N numbers in O(N log N) time. Complexity theory asks what you can learn about the task of sorting in general, not what you can learn about a specific algorithm. It turns out you can show that any sorting algorithm that sorts by comparisons must use at least N × log(N) time in the worst case.

# N LOG SORTING

To understand why any algorithm that uses comparisons to sort a list must use at least N log N in the worst case, suppose you have an array of N unique items. Because they are unique, there are N! ways you can arrange them. To look at this in a different way, depending on what the values in the array are, there are N! ways the algorithm might need to rearrange the items to put them in sorted order. That means the algorithm must be able to follow N! paths of execution to produce every possible result.

Continued