```
void partition(int data[] , size_t n, size_t& pivot_index);
// Precondition: n > 1, and data is an array (or subarray) with at least n
// elements.
// Postcondition: The function has selected some "pivot value" that occurs
// in data[0].. data[n-1]. The elements of data have then been
// rearranged and the pivot index set so that
// - datapivot_index] is equal to the pivot;
// - each item before data[pivot_index] is <= the pivot;
// - each item after data[pivot_index] is > the pivot.
```

We will formulate our sorting algorithm as a recursive function called quicksort, which makes a call to the partition function. After the partitioning, the array and the pivot index look like this:

![](bbox=[0.27, 0.355, 0.83, 0.475])

After the partition, our quicksort function makes two recursive calls. The first recursive call sorts the elements before the pivot element, from data[0] to data[pivot_index - 1]. The second recursive call sorts the elements after the pivot element, from data[pivot_index + 1] to data[n - 1]. The recursive calls are part of the quicksort implementation in Figure 13.5. We still need to derive the code for the partition function.

# The Partition Function

Since we have no information about the values in the array, all values have an equal probability of being the value that belongs in the middle of the array. Moreover, we know that the algorithm will work no matter what value we use for the pivot element. So, we arbitrarily choose the first array element to use as the pivot element. (On page 661 we discuss why this is not always the best choice and propose a method to fix the problem.)

The partition function will move all the values that are less than or equal to this pivot element toward the beginning of the array, that is, toward positions with lower-numbered indices. All values that are greater than this pivot element are moved the other way, toward the tail end of the array, with higher-numbered indices. Because the pivot element is not necessarily the value that belongs at the exact midpoint position of the array, we do not know where the dividing line between the two array portions belongs. Hence, we do not know how far forward we need to move elements less than or equal to the pivot element, nor do we know how far toward the end of the array we must move elements that are greater than the pivot element. We solve this dilemma by working inward from the two