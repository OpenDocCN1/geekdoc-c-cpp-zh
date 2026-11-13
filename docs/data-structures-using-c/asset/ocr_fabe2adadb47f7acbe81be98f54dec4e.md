Hence, the average number of comparisons done by the sequential search method in the case of a successful search is (n + 1)/2. An unsuccessful search is given by n comparisons. The number of comparisons is n and the complexity is denoted as O(n).

The worst case complexity is n, which means that the target data element is at the nth location and hence requires n comparisons. The best case element is 1, as the target data element is at the first location and requires only a single comparison. Sequential search is suitable when the data is stored in an unordered manner and also when there is no way to directly access the data elements. For example, to search the data record stored on a magnetic tape, it has to be searched sequentially from the first location till the nth location. The linear list implemented using a linked list cannot access any ith element directly except (i = 1). We need to search through the whole list to retrieve a target data. Hence, sequential search is used if the data is unsorted and if the storage does not provide direct access to the data.

# Pros and Cons of Sequential Search

The following lists detail the pros and cons of sequential searching:

# Pros

+   1. A simple and easy method
+   2. Efficient for small lists
+   3. Suitable for unsorted data
+   4. Suitable for storage structures which do not support direct access to data, for example, magnetic tape, linked list, etc.
+   5. Best case is one comparison, worst case is n comparisons, and average case is (n + 1)/2 comparisons
+   6. Time complexity is in the order of n denoted as O(n).

# Cons

+   1. Highly inefficient for large data
+   2. In the case of ordered data other search techniques such as binary search are found more suitable.

# Variations of Sequential Search

The time complexity of sequential search is O(n); this amounts to one comparison in the best case, n comparisons in the worst case, and (n + 1)/2 comparisons in the average case. The algorithm starts at the first location and the search continues till the last element. We can make a few changes leading to a few variations in the sequential search algorithm. There are three such variations:

+   1. Sentinel search
+   2. Probability search
+   3. Ordered list search