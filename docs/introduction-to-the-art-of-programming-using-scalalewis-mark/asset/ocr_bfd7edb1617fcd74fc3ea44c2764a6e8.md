![](bbox=[0.15, 0.12, 0.85, 0.5])

FIGURE 32.2: This figure shows the same heap as in figure 32.1 with subscripts that number the nodes in breadth-first order. Below that is an array with the elements at those locations.

until it reaches the location that the new element belongs. As long as the new element has a higher priority than the parent of the bubble, the parent is copied down and the bubble moves up. An example of adding a new element with a priority of 9 to the example heap is shown in figure 32.3.

A call to dequeue should remove the element from the root of the tree as that will always have the highest priority. However, to keep the tree complete, the location that needs to be vacated is at the end of the last row. To deal with this, we pull the last element out of the heap and put it in a temporary variable then put a placeholder we will call a "stone" at the root. This stone then sinks through the heap until it gets to a point where the temporary can stop without breaking heap-order. When moving down through the heap there is a choice of which child the stone should sink to. In order to preserve heap-order, it has to move to the higher-priority child as we are not allowed to move the lower-priority child into the parent position above its higher-priority sibling. This process is illustrated in figure 32.4.

Code to implement these operations using an array-based binary heap is shown below. This extends the PriorityQueue[A] type that was created in chapter 26. Like the sorted linked-list implementation, a comparison function is passed in to provide the complete ordering of elements for instances of this class. The only data needed by this class is an array we call heap and an integer called end that keeps track of where the next element should be added. These are created with 10 elements to begin with, one of which will never be used as index zero is left empty, and the other is set to be 1.

```
package scalabook.adt
```