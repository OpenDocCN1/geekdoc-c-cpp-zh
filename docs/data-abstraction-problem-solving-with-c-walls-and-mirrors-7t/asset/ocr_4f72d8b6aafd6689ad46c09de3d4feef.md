# FIGURE 17-4 (a) Disjoint heaps after removing the heap's root; (b) a semiheap; (c) the restored heap

![](bbox=[0.2, 0.15, 0.6, 0.28])

![](bbox=[0.2, 0.29, 0.6, 0.41])

![](bbox=[0.2, 0.42, 0.6, 0.54])

The transformation from the semiheap in Figure 17-5b to the heap in Figure 17-5c is accomplished by the following recursive algorithm. Note that the algorithm will not work if it does not begin with a semiheap.

```
// Converts a semiheap rooted at index root into a heap.
heapRebuild(root: integer, items: ArrayType, itemCount: integer)

// Recursively trickle the item at index root down to its proper position by
// swapping with its larger child; if the child is larger than the item.
// If the item is a leaf, nothing needs to be done.
if (the root is not a leaf)
{
   // The root must have a left child; assume it is the larger child
   largerChildIndex = 2 * rootIndex + 1   // Left child index

   if (the root has a right child)
   {
      rightChildIndex = largerChildIndex + 1   // Right child index
      if (items[rightChildIndex] > items[largerChildIndex] )
         largerChildIndex = rightChildIndex   // Larger child index
   }
   // If the item in the root is smaller than the item in the larger child, swap items
   if (items[rootIndex] < items[largerChildIndex])
   {
      Swap items[rootIndex] and items[largerChildIndex]
```

remove's final step transforms the semiheap into a heap

Every nonleaf in a complete tree has a left child