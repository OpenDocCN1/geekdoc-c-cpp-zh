```
Unsorted array:
[40, 17, 45, 82, 62, 32, 30, 44, 93, 10]

after pass 1: 17* 40 45 82 62 32 30 44 93 10
after pass 2: 17 40 45* 82 62 32 30 44 93 10
after pass 3: 17 40 45 82* 62 32 30 44 93 10
after pass 4: 17 40 45 62* 82 32 30 44 93 10
after pass 5: 17 32* 40 45 62 82 30 44 93 10
after pass 6: 17 30* 32 40 45 62 82 44 93 10
after pass 7: 17 30 32 40 44* 45 62 82 93 10
after pass 8: 17 30 32 40 44 45 62 82 93* 10
after pass 9: 10* 17 30 32 40 44 45 62 82 93

Sorted array:
[10, 17, 30, 32, 40, 44, 45, 62, 82, 93]
```

**Fig. 19.9** | Testing the insertion sort class. (Part 2 of 2.)

# Efficiency of the Insertion Sort

The insertion sort algorithm also runs in *O(n²)* time. Like selection sort, the implementation of insertion sort (lines 23–47 of Fig. 19.8) contains two loops. The for loop (lines 28–46) iterates `data.length − 1` times, inserting an element into the appropriate position in the elements sorted so far. For the purposes of this application, `data.length − 1` is equivalent to *n − 1* (as `data.length` is the size of the array). The while loop (lines 37–42) iterates over the preceding elements in the array. In the worst case, this while loop will require *n − 1* comparisons. Each individual loop runs in *O(n)* time. In Big O notation, nested loops mean that you must multiply the number of comparisons. For each iteration of an outer loop, there will be a certain number of iterations of the inner loop. In this algorithm, for each *O(n)* iterations of the outer loop, there will be *O(n)* iterations of the inner loop. Multiplying these values results in a Big O of *O(n²)*.

# 19.3.3 Merge Sort

**Merge sort** is an *efficient* sorting algorithm but is conceptually *more complex* than selection sort and insertion sort. The merge sort algorithm sorts an array by *splitting* it into two equal-sized subarrays, *sorting* each subarray, then *merging* them into one larger array. With an odd number of elements, the algorithm creates the two subarrays such that one has one more element than the other.