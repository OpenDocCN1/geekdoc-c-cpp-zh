**3**  *(Discussion)* Compare the worst-case performance of a linear search on an unsorted trillion-element array with the worst-case performance of a binary search on a trillion element sorted array.

**Answer:** The linear search would have to perform about a trillion comparisons to determine that the search key doesn’t match an item in the unsorted array or matches an element close to the array’s end. The binary search would have to perform about 40 comparisons to determine that the search key either doesn’t match an item in the sorted array or matches an item on the last few comparisons.

# ## 21.5 Insertion Sort

Next, let’s implement a sorting algorithm. The insertion sort algorithm’s first iteration takes the array’s second element and, if it’s less than the first element, swaps it with the first element—that is, the algorithm inserts the second element in front of the first element. The second iteration looks at the third element and inserts it into the correct position with respect to the first two elements so all three elements are in order.

# ### First Iteration

Line 27 of Fig. 21.3 declares and initializes the array named `data` with the following values:

```
34   56   4   10   77   51   93   30   5   52
```

Line 36 passes the array to the `insertionSort` function, which receives the array in parameter `items`. The function first looks at items[0] and items[1], whose values are 34 and 56, respectively. These two elements are already in order, so the algorithm continues. If they were out of order, the algorithm would swap them.

# ### Second Iteration

In the second iteration, the algorithm looks at the value of items[2] (that is, 4). This value is less than 56, so the algorithm stores 4 in a temporary variable and moves 56 one element to the right. The algorithm then determines that 4 is less than 34, so it moves 34 one element to the right. At this point, the algorithm has reached the beginning of the array, so it places 4 in items[0]. The array is now:

```
4   34   56   10   77   51   93   30   5   52
```

# ### Third Iteration and Beyond

In the third iteration, the algorithm places the value of items[3] (that is, 10) in the correct location with respect to the first four array elements. The algorithm compares 10 to 56 and moves 56 one element to the right because it’s larger than 10. Next, the algorithm compares 10 to 34, moving 34 one element to the right. When the algorithm compares 10 to 4, it observes that 10 is greater than 4 and places 10 in items[1]. The array is now:

```
4   10   34   56   77   51   93   30   5   52
```

With this algorithm, after the *i*th iteration, the first *i* + 1 array elements are sorted. However, they may not be in their final locations because the algorithm might encounter smaller values later in the array.