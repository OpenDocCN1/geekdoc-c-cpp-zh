
## Question 5 What complete binary tree does the following array represent?

| 5 | 1 | 2 | 8 | 6 | 10 | 3 | 9 | 4 | 7 |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

## Question 6 Does the array in the previous question represent a heap?

## 17.2.1 Algorithms for the Array-Based Heap Operations

Let's assume that our class of heaps has the following private data members:

The data members for an array-based implementation of a heap

- items: an array of heap items
- itemCount: an integer equal to the number of items in the heap
- maxItems: an integer equal to the maximum capacity of the heap

The array `items` corresponds to the array-based representation of a complete binary tree, such as the array shown in Figure 17-3b. We will assume that we are working with a maxheap of integers.

### Retrieving an item from a heap.

First consider the heap's `peekTop` operation. Where is the largest item in the heap? Because the item in every tree node is greater than or equal to the item in either of its children, the largest item must be in the root of the tree—that is, at the top of the heap. Thus, the `peekTop` operation needs to take only the following step:

peekTop's logic

```
// Return the item in the root
return items[0]
```

### Removing an item from a heap.

While the `peekTop` operation returns the largest item in the heap—which we know is in its root—the heap operation remove must remove it. Removing the root of the heap leaves two disjoint heaps, as Figure 17-4a indicates. Therefore, you do not want to actually remove the root. Instead, you remove the last node of the tree and place your item in the root, as Figure 17-4b shows. The result of this step is *not* necessarily a heap. It is, however, a complete binary tree whose left and right subtrees are both heaps. The only problem is that the item in the root usually is out of place. Such a structure is called a **semheap**.

remove's first step produces a semheap

You thus need a way to transform a semheap into a heap. One strategy allows the item in the root to `trickle down` the tree until it reaches a node in which it will not be out of place; that is, the item will come to rest in the first node where it would be greater than or equal to the item in each of its children. To accomplish this, you first compare the item in the root of the semheap to the items in its children. If the root's item is smaller than the larger of the items in its children, you swap the item in the root with that larger item. For convenience, we will refer to the child containing the larger item as the *larger child*. The result of this step is shown in Figure 17-4c. Although the value 5 trickles down in this example to its correct position after only one swap, in general more swaps may be necessary.

We need to remember that an array represents the original heap before we remove its root. The remove operation will simply move items within this array. Figure 17-5 shows the array for the heaps and semheap illustrated in Figure 17-4. The transformation from the heap in Figure 17-5a to the semheap in Figure 17-5b is accomplished by the following steps:

```
// Copy the item from the last node and place it into the root
items[0] = items[itemCount - 1]
// Remove the last node
itemCount--
```

### FIGURE 17-4 (a) Disjoint heaps after removing the heap's root; (b) a semheap; (c) the restored heap

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_535_0.png)

The transformation from the semheap in Figure 17-5b to the heap in Figure 17-5c is accomplished by the following recursive algorithm. Note that the algorithm will not work if it does not begin with a semheap.

```
// Converts a semheap rooted at index root into a heap.
heapRebuild(root: integer, items: ArrayType, itemCount: integer)
// Recursively trickle the item at index root down to its proper position by
// swapping with its larger child; if the child is larger than the item.
// If the item is a leaf, nothing needs to be done.
if (the root is not a leaf)
{
// The root must have a left child; assume it is the larger child
largerChildIndex = 2 * rootIndex + 1 // Left child index
if (the root has a right child)
{
rightChildIndex = largerChildIndex + 1 // Right child index
if (items[rightChildIndex] > items[largerChildIndex ])
largerChildIndex = rightChildIndex // Larger child index
}
// If the item in the root is smaller than the item in the larger child, swap items
if (items[rootIndex] < items[largerChildIndex])
{
Swap items[rootIndex] and items[largerChildIndex]
// Transform the semheap rooted at largerChildIndex into a heap
heapRebuild(largerChildIndex, items, itemCount)
}
}
// Else root is a leaf, so you are done
```

remove's final step transforms the semheap into a heap

Every nonleaf in a complete tree has a left child

Figure 17-6 illustrates heapRebuild's recursive calls.

### FIGURE 17-5

The array representation of (a) the heap in Figure 17-4a; (b) the semheap in Figure 17-4b; (c) the restored heap in Figure 17-4c

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_536_0.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_536_1.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_536_2.png)

### FIGURE 17-6

Recursive calls to heapRebuild

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_536_3.png)

Now the heap's remove operation uses heapRebuild as follows:

```
// Copy the item from the last node into the root
items[0] = items[itemCount - 1]
// Remove the last node
itemCount--
// Transform the semheap back into a heap
heapRebuild(0, items, itemCount)
```

Consider briefly the efficiency of remove. Because the tree is stored in an array, the removal of a node requires you to swap array entries rather than simply to change a few pointers. These swaps may concern you, but they do not necessarily indicate that the algorithm is inefficient. At most, how many array entries will you have to swap? After remove copies the item in the last node of the tree into the root, heapRebuild trickles this item down the tree until its appropriate place is found. This item travels down a single path from the root to, at worst, a leaf. Therefore, the number of array items that heapRebuild must swap is no greater than the height of the tree. The height of a complete binary tree with n nodes is always ⌊log(n + 1)⌋, as you know from Chapter 15. Because each swap requires three data moves, remove requires

3 × ⌊log₂(n + 1)⌋ + 1

data moves. Thus, remove is O(log n), which is in fact quite efficient.

### Adding an item to a heap.

The strategy for the add algorithm is the opposite of that for remove. A new item is inserted at the bottom of the tree, and it trickles up to its proper place, as Figure 17-7 illustrates. It is easy to trickle up a node, because the parent of the node in items[i] is always stored in items[(i - 1) / 2]—unless, of course, the node is the root.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_537_0.png)

The pseudocode for add follows:

```
// Insert newData into the bottom of the tree
items[itemCount] = newData
// Trickle new item up to the appropriate spot in the tree
newDataIndex = itemCount
inPlace = false
while ((newDataIndex > 0) and !inPlace)
{
   parentIndex = (newDataIndex - 1) / 2
   if (items[newDataIndex] < items[parentIndex])
inPlace = true
else
{
    Swap items[newDataIndex] and items[parentIndex]
    newDataIndex = parentIndex
}
itemCount++
```

**insert is O(log n)**

The efficiency of insert is like that of remove. At worst, insert has to swap array entries on a path to a leaf to the root. The number of swaps, therefore, cannot exceed the height of the tree. Because the height of the tree, which is complete, is always ⌊log₂(n + 1)⌋, insert is also O(log n).

- Question 7 Is the full binary tree in Figure 16-16 of Chapter 16 a semheap?
- Question 8 Consider the maxheap in Figure 17-1a. Draw the heap after you insert 12 and then remove 12.
- Question 9 What does the initially empty heap myHeap contain after the following sequence of pseudocode operations?
  ```
  myHeap.add(2)
  myHeap.add(3)
  myHeap.add(4)
  myHeap.add(1)
  myHeap.add(9)
  myHeap.remove()
  myHeap.add(7)
  myHeap.add(6)
  myHeap.remove()
  myHeap.add(5)
  ```

## 17.2.2 The Implementation

The header file for the class ArrayMaxHeap, which is an array-based implementation of the ADT heap, is in Listing 17-2. This heap is a maxheap.

```
LISTING 17-2 The header file for the class ArrayMaxHeap
/** Array-based implementation of the ADT heap.
@file ArrayMaxHeap.h */
#ifndef _ARRAY_MAX_HEAP
#define _ARRAY_MAX_HEAP
#include "HeapInterface.h"
#include "PrecondViolatedExcep.h"
template<class ItemType>
class ArrayMaxHeap : public HeapInterface<ItemType>
{
```
