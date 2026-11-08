# 25.6.6  Algorithms for Sorting and Fast Searching in Sorted Ranges

Searching and sorting are extremely important. Doing this skillfully is a good way to achieve fast programs. Sometimes, it is best to simply use an automatically sorted container like `multimap` or `set` or the `flat_set` adapters introduced in C++23. Very often, however, this is not the best method. First, put all elements, as they come, into any sequence container and then sort them all at once. `map` is not very memory-friendly, and the elements are scattered all over. A vector behaves much better in this regard and works excellently with the algorithms for sorting and `binary_search`. The `flat_` adapters around a vector are a compromise, but the best approach is to first collect the data, then sort:

+   - `sort`  
+     Usage: constant; iterators: ra  
+     Sorts the elements in the range; see for example Listing 25.2.
+   - `stable_sort`  
+     Usage: frequent; iterators: ra  
+     Like `sort`, but ensures that equal elements retain their relative order.
+   - `partial_sort`  
+     Usage: occasional; iterators: ra  
+     Like `partition`, uses the comparison with the middle element as the predicate.
+   - `partial_sort_copy`  
+     Usage: occasional; iterators: in/ra  
+     Like `partial_sort`, but copies the result into a target range.
+   - `is_sorted`  
+     Usage: frequent; iterators: fw  
+     Checks if a range is sorted.
+   - `is_sorted_until`  
+     Usage: occasional; iterators: fw  
+     Finds the first element in a range that breaks the sorting.
+   - `nth_element`  
+     Usage: occasional; iterators: ra  
+     Sorts the elements in the range, but only until the *n*-th element is determined.
+   - `lower_bound`  
+     Usage: constant; iterators: fw  
+     Identifies the first element within a sorted range.
+   - `upper_bound`  
+     Usage: frequent; iterators: fw  
+     Finds the last sought element in a sorted range.
+   - `equal_range`  
+     Usage: frequent; iterators: fw  
+     Corresponds to `lower_bound` and `upper_bound` simultaneously.