
```cpp
#include "ArrayMaxHeap.h"
#include "PriorityQueueInterface.h"

template<class ItemType>
class Heap_PriorityQueue : public PriorityQueueInterface<ItemType>,
                           private ArrayMaxHeap<ItemType>
{
public:
   Heap_PriorityQueue();
   bool isEmpty() const;
   bool add(const ItemType& newEntry);
   bool remove();
   /** @pre  The priority queue is not empty. */
   ItemType peek() const throw(PrecondViolatedExcep);
}; // end Heap_PriorityQueue

#include "Heap_PriorityQueue.cpp"
#endif
```

Each of the method definitions in Listing 17-4 calls the corresponding method in ArrayMaxHeap. Notice how the method peek handles the exception thrown by the heap's peekTop method, so that the message given mentions the priority queue and not the underlying heap.

```cpp
LISTING 17-4 An implementation of the class Heap_PriorityQueue
/** Heap-based implementation of the ADT priority queue.
@file Heap_PriorityQueue.cpp  */

#include "Heap_PriorityQueue.h"

template<class ItemType>
Heap_PriorityQueue<ItemType>::Heap_PriorityQueue()
   : ArrayMaxHeap<ItemType>()
{  // end constructor

template<class ItemType>
bool Heap_PriorityQueue<ItemType>::isEmpty() const
{
   return ArrayMaxHeap<ItemType>::isEmpty();
}  // end isEmpty

template<class ItemType>
bool Heap_PriorityQueue<ItemType>::add(const ItemType& newEntry)
{
   return ArrayMaxHeap<ItemType>::add(newEntry);
}  // end add

template<class ItemType>
bool Heap_PriorityQueue<ItemType>::remove()
{
   return ArrayMaxHeap<ItemType>::remove();
}  // end remove

template<class ItemType>
ItemType Heap_PriorityQueue<ItemType>::peek() const throw(PrecondViolatedExcep)
{
   try
   {
      return ArrayMaxHeap<ItemType>::peekTop();
   }
   catch (PrecondViolatedExcep e)
   {
      throw PrecondViolatedExcep("Attempted peek into an empty priority queue.");
   } // end try/catch
} // end peek
```

### The heap implementation requires knowledge of the priority queue's maximum size

### A heap versus a binary search tree as a priority queue
How does a heap compare to a binary search tree as an implementation of a priority queue? If you know the maximum number of items in the priority queue, the heap is the better implementation.

### A heap is always balanced
Because a heap is complete, it is always balanced, which is its major advantage. If the binary search tree is balanced, both implementations will have the same average performance for n items: They both will be O(log n). The height of a binary search tree, however, can increase during the insertion and removal of entries, greatly exceeding log n and degrading the implementation's efficiency to O(n) in the worst case. The heap implementation avoids this decrease in performance. In Chapter 19, you will see how to keep a search tree balanced, but the operations that do this are far more complex than the heap operations.

### A heap of queues
Finite, distinct priority values. If you have a finite number of distinct priority values, such as the integers 1 through 20, many items will likely have the same distinct priority value. You could place items whose priority values are the same in the order in which you encounter them.

A heap of queues accommodates this situation, one queue for each distinct priority value. To insert an item into the priority queue, you add a queue for the item's priority value to the heap, if it is not already there. Then you insert the item into the corresponding queue. To remove an item from a priority queue, you remove the item at the front of the queue that corresponds to the highest priority value in the heap. If this removal leaves the queue empty, you remove the queue from the heap. Programming Problem 7 at the end of this chapter treats distinct priority values further.

### Question 11
Consider a heap-based implementation of the ADT priority queue. What does the underlying heap contain after the following sequence of pseudocode operations, assuming that pQueue is an initially empty priority queue?

```
pQueue.add(5)
pQueue.add(9)
pQueue.add(6)
pQueue.add(7)
pQueue.add(7)
pQueue.add(3)
pQueue.add(4)
pQueue.remove()
pQueue.add(9)
pQueue.add(2)
pQueue.remove()
```

## 17.4 Heap Sort

As its name implies, the heap sort algorithm uses a heap to sort an array of items that are in no particular order. Suppose that we have a heap and an empty array whose size is the number of items in the heap. A call to peekTop gets the largest item in the heap, and we can place that item at the end of the array. A call to remove then removes that item from the heap. By repeatedly calling peekTop and remove, we can move the items from the heap in descending order and place them into sequentially decreasing positions in the array. The result is an array sorted in ascending order.

While this approach would work, it uses more memory and time than is necessary. Let's start over with an array of unsorted values. Our first step would be to transform the array into a heap. Recall the private method heapCreate from our implementation of the ADT heap in Section 17.2.2. This method transformed the array items, which is a data member of the class of heaps, into a heap. The body of heapCreate is simply the following loop:

```
for (int index = itemCount / 2; index >= 0; index--)
heapRebuild(index);
```

As members of the class ArrayMaxHeap, both heapCreate and heapRebuild have access to the class's data members, including the array items and its number of entries, itemCount. To use heapRebuild in a heap sort, we must revise it so that it has the array and its size as parameters. Let's declare heapRebuild as a function outside of ArrayMaxHeap, as follows:

```
void heapRebuild(int index, ItemType& anArray[], int n)
```

After transforming the array into a heap, heap sort partitions the array into two regions—the Heap region and the Sorted region—as Figure 17-10 illustrates. The Heap region is in anArray[0..last], and the Sorted region is in anArray[last + 1..n - 1]. Initially, the Heap region is all of anArray and the Sorted region is empty.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_545_0.png)

Each step of the algorithm moves an item I from the Heap region to the Sorted region. During this process, the following statements are true—they are the algorithm's invariant:

- The Sorted region contains the largest values in anArray, and they are in sorted order—that is, anArray[n - 1] is the largest item, anArray[n - 2] is the second largest, and so on.
- The items in the Heap region form a heap.

So that the invariant holds, I must be the item that has the largest value in the Heap region, and therefore force I must be in the root of the heap. To accomplish the move, you exchange the item in the root of the heap with the last item in the heap—that is, you exchange anArray[0] with anArray[last]—and then decrement the value of last. As a result, the item just swapped from the root into anArray[last]

### Building a heap from an array of items

### This version of heapRebuild is not in ArrayMaxHeap

### Invariant for heap sort

becomes the smallest item in the Sorted region (and is in the first position of the Sorted region). After the move, you must transform the Heap region back into a heap because the new root may be out of place. You can accomplish this transformation by using heapRebuild to trickle down the item now in the root so that the Heap region is once again a heap.

The following algorithm summarizes these steps:

```
// Sorts anArray[0..n-1].
heapSort(anArray: ArrayType, n: integer)
// Build initial heap
for (index = n / 2 down to 0)
{
   // Assertion: The tree rooted at index is a semiheap
   heapRebuild(index, anArray, n)
   // Assertion: The tree rooted at index is a heap
}
// Assertion: anArray[0] is the largest item in heap anArray[0..n-1]
// Move the largest item in the Heap region--the root anArray[0]--to the beginning
// of the Sorted region by swapping items and then adjusting the size of the regions
Swap anArray[0] and anArray[n - 1]
heapSize = n - 1 // Decrease the size of the Heap region, expand the Sorted region
while (heapSize > 1)
{
   // Make the Heap region a heap again
   heapRebuild(0, anArray, heapSize)
   // Move the largest item in the Heap region--the root anArray[0]--to the beginning
   // of the Sorted region by swapping items and then adjusting the size of the regions
   Swap anArray[0] and anArray[heapSize - 1]
   heapSize-- // Decrease the size of the Heap region, expand the Sorted region
}
```

If we begin with the array shown in Figure 17-9, the first steps of heap sort are the same as those shown in the figure, and they transform the array into a heap. Figure 17-11 traces the heap sort from that point on. The C++ implementation of heap sort is left as an exercise.

### Heap sort is O(n * log n)

The analysis of the efficiency of heap sort is similar to that of merge sort, as given in Chapter 11. Both algorithms are O(n * log n) in both the worst and average cases. Heap sort has an advantage over merge sort in that it does not require a second array. Quick sort is also O(n * log n) in the average case but is O(n^2) in the worst case. Even though quick sort has poor worst-case efficiency, it is generally the preferred sorting algorithm.

### Question 12
Trace the heap sort as it sorts the following array in ascending order: 25 30 20 80 40 60
