# Example:

```
Dataset: 5 2 9 1 5
Target: 1

Iteration 1: 5 (no match)
Iteration 2: 2 (no match)
Iteration 3: 9 (no match)
Iteration 4: 1 (match found at index 3)
```

# Binary Search:

Principle: Applicable to sorted datasets, binary search divides the dataset in half repeatedly, narrowing down the search range until the target element is found or determined to be absent.

# Process:

+   1. Start with the entire sorted dataset.
+   2. Compare the target element with the middle element.
+   3. If they match, the search is successful; otherwise, narrow the search range based on the comparison.
+   4. Repeat the process until the target is found or the search range becomes empty.

Time Complexity: O(log n) in the worst case, where n is the size of the dataset.

# Example:

```
Sorted Dataset: 1 2 5 5 9
Target: 5

Iteration 1: 5 (match found at index 2)
```

# Comparison and Selection:

Linear Search: Simple and applicable to any dataset, but less efficient for large datasets.

Binary Search: Efficient for sorted datasets, reducing the search space exponentially with each comparison.

# Choosing the Right Algorithm:

Linear Search: Suitable for unsorted datasets or scenarios where the dataset size is small.