We won't give a derivation, but it turns out that the average-case running time for heapsort is also O(n log n), the same as the worst-case running time.

# Heapsort Running Time

The worst-case running time and the average-case running time for heapsort are both O(n log n).

# Self-Test Exercises for Section 13.3

+   15. How is the heapsort algorithm similar to the selectionsort algorithm? How is it different?
+   16. How would you modify the heapsort algorithm so that it sorts integers into decreasing order rather than increasing order?
+   17. What features of the mergesort and quicksort algorithms does the heapsort algorithm have?

# 13.4 SORTING AND BINARY SEARCH IN THE STL

# The Original C qsort Function

The original C Standard Library has a quicksort function that is still widely used. The prototype is part of <cstdlib>, along these lines:

```
void qsort(
   void* base,
   size_t number_of_elements,
   size_t element_size,
   int compare(const void*, const void*)
);
```

The first parameter is a pointer to an element of an array. The data type void* indicates that the type of elements in the array remains unspecified. It could be an array of integers, or an array of doubles, or some more complex type.

The second parameter is the number of elements in the array to be sorted (starting with the element that base points to).

The third parameter tells how many bytes of memory are required for each element of the array. In C++, this number can be obtained by applying the sizeof operator to the data type. For example, sizeof(int) is the number of bytes for one integer.

The final parameter, compare, is a function that is itself as described on page 507. As the name suggests, the compare function is used to compare two elements of the array. In particular, the two parameters to the compare function are pointers to elements in the array. The return value must be an integer such that: