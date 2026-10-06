```
// Converts a semiheap rooted at index root into a heap
heapRebuild(root: integer, items: ArrayType, itemCount: integer)
  // Recursively trick the item at index root down to its proper position
  // by swapping it with child. If the child is larger than the item.
  // If the item is a leaf, nothing needs to be done.
  if (root is not a leaf)
    // The root must have a left child; assume it is the larger child
    largerChildIndex = 2 * root + 1 // Left child index
    if (root has a right child)
      rightChildIndex = largerChildIndex + 1 // Right child index
      if (items[rightChildIndex] > items[largerChildIndex])
        largerChildIndex = rightChildIndex // Larger child index
    // If the item in the root is smaller than the item in the larger child, swap items
    if (items[root] < items[largerChildIndex])
      Swap items[root] and items[largerChildIndex]
```