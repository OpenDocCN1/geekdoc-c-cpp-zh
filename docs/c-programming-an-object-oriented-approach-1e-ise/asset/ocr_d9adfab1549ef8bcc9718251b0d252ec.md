# ## 17.2 RECURSIVE SORT AND SEARCH

In computer science we often need to sort a list and search a list. When a list is sorted, the search can be very fast.

# ### 17.2.1 Quick Sort

To *sort* means to rearrange the elements of a list (such as an array) so that the values are in sequence. The sorting algorithm that we introduce in this section is called *quicksort* (a recursive algorithm). This is a fast and efficient algorithm that is used in most libraries. The quicksort algorithm uses a nonrecursive algorithm called *partition*, which we discuss next.

# ### Partition Algorithm

The partition algorithm rearranges an array around a *pivot*, one of the elements of the array, so that all elements larger than or equal to *pivot* move after it and all elements smaller than *pivot* move before it. The *pivot* is normally selected as the first element.

The following shows the partition algorithm.

```
```c
int partition (int arr[], int i, int j) // i and j are partition indexes
{
  int p = i; // p is the pivot
  while (i < j) // outer loop
  {
    while (arr[j] > arr[p]) // first inner loop
    {
      j--;
    }
    swap(arr[j], arr[p]);
    p = j;
    j--;
    while (arr[i] < arr[p]) // second inner loop
    {
      i++;
    }
    swap(arr[i], arr[p]);
    p = i;
    i++;
  }
  return p;
}
```
```

In each execution of the outer loop, we perform the following two sets of actions.

+   - We move *j* to the left as long as *arr[j]* is larger than the *arr[p]*. We then swap the values of *arr[j]* and *arr[p]* and set *p = j*. Then we move *j* one more element to the left.
+   - We move *i* to the right as long as *arr[i]* is smaller than *arr[p]*. We then swap the values of *arr[i]* and *arr[p]* and set *p = i*. Then we move *i* one more element to the right.

The *pivot* *p* is set to the first element, but it moves to its final position in the array. Note that after the second iteration, *i* moves to the right of *j* and the outer loop terminates.