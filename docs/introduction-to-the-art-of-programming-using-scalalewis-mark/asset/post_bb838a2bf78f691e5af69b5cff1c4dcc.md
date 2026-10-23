
## Chapter 32: Binary Heaps

| 标题 | 页码 |
|------|------|
| 32.1 Binary Heaps | 793 |
| 32.1.1 Binary Heaps as Arrays | 793 |
| 32.2 Heaps as Priority Queues | 794 |
| 32.3 Heapsort | 801 |
| 32.4 End of Chapter Material | 802 |
| 32.4.1 Summary of Concepts | 802 |
| 32.4.2 Exercises | 803 |
| 32.4.3 Projects | 803 |

Back in chapter 26 we looked at the priority queue Abstract Data Type (ADT). In that chapter, the implementation that was written used a sorted linked-list. While it was easy to write, this implementation has the downside of an O(n) enqueue method. This gives overall performance that is O(n²) for the size of the queue. In this chapter we will look at a different implementation that provides O(log(n)) performance for both enqueue and dequeue, the heap.

### 32.1 Binary Heaps

There are quite a few different styles of heaps. A common theme is that they have a tree structure. The simplest, and probably most broadly used, is the binary heap. As the name implies, it is based on a binary tree type of structure where each node can potentially have left and right children. For a binary tree to be a binary heap it has to have two properties:

- Complete - The tree fills in each level from left to right. There are never gaps in a proper binary heap.
- Heap Ordering - Priority queues require that elements have a complete ordering. The rule for a binary heap is that parents always have a priority that is greater than or equal to their children.

The heap ordering means that the highest priority element is always at the root of the tree. An example is shown in figure 32.1.

![](img/157fcf510c119278e4b1267c62717fa8_829_0.png)

FIGURE 32.1: This figure shows an example of a binary heap. The numbers are priorities with higher values being higher priority. Note that there is no problem with duplicate priorities, unlike keys in a BST.

#### 32.1.1 Binary Heaps as Arrays

While we conceptually think of the heap as a binary tree, we do not implement it that way. It is far more efficient to implement it as an array. This only works because the heap is complete. Figure 32.2 shows the same heap as in figure 32.1 with subscripts that number the nodes in breadth-first order. Looking closely at the subscripts you should see that there is a nice mathematical relationship between parents and children. Specifically, if you divide an index by two, using integer division, the result is the index of the parent. The reverse relationship is that the children of a node have indices that are twice the node’s index and twice the node’s index plus one.

The figure shows the array leaving the 0 index spot empty. It is possible to implement a heap with all the elements shifted down one spot so that there is not a blank. However, this requires putting +1 and -1 in the code at many different points. This complicates the code making it harder to understand and maintain. While it removes a little waste in memory, it introduces an overhead in every call on the priority queue. For that reason, and to keep the code simpler, the implementation shown here will leave the first element of the array as a default value.

![](img/157fcf510c119278e4b1267c62717fa8_830_0.png)

FIGURE 32.2: This figure shows the same heap as in figure 32.1 with subscripts that number the nodes in breadth-first order. Below that is an array with the elements at those locations.

### 32.2 Heaps as Priority Queues

To use the binary heap as a priority queue we have to be able to implement enqueue, dequeue, peek, and isEmpty. The last two are simple, the highest priority element is always the root so peek simply returns it. The isEmpty method just checks if there is anything present on the heap. The enqueue and dequeue are a bit more complex because they have to change the structure of the heap.

We start with enqueue where an element is added to the queue. Adding to a Binary Search Tree (BST) was just a task of finding the proper place to put the new element. For a heap, the job is a bit different. The heap has to remain complete so when a new element is added, there is no question about what set of nodes have to be occupied. The next open space in the row that is currently filling in or the first in the next row when the lowest row is complete has to be filled. However, the new element might not belong there. The way we deal with this is to put a “bubble” in the position that has to be filled and let it move up until it reaches the location that the new element belongs. As long as the new element has a higher priority than the parent of the bubble, the parent is copied down and the bubble moves up. An example of adding a new element with a priority of 9 to the example heap is shown in figure 32.3.

![](img/157fcf510c119278e4b1267c62717fa8_831_0.png)

![](img/157fcf510c119278e4b1267c62717fa8_831_1.png)

![](img/157fcf510c119278e4b1267c62717fa8_831_2.png)

![](img/157fcf510c119278e4b1267c62717fa8_831_3.png)

FIGURE 32.3: Adding a new element with a priority of 9 to the heap shown in figure 32.1 goes through the following steps. A bubble is added at the next location in a complete tree. It moves up until it reaches a point where the new value can be added without breaking the heap-order.

A call to dequeue should remove the element from the root of the tree as that will always have the highest priority. However, to keep the tree complete, the location that needs to be vacated is at the end of the last row. To deal with this, we pull the last element out of the heap and put it in a temporary variable then put a placeholder we will call a "stone" at the root. This stone then sinks through the heap until it gets to a point where the temporary can stop without breaking heap-order. When moving down through the heap there is a choice of which child the stone should sink to. In order to preserve heap-order, it has to move to the higher-priority child as we are not allowed to move the lower-priority child into the parent position above its higher-priority sibling. This process is illustrated in figure 32.4.

![](img/157fcf510c119278e4b1267c62717fa8_832_0.png)

**FIGURE 32.4:** Calling **dequeue** on the heap at the end of figure 32.3 forces the tree to go through the following steps. The last element is moved to a temporary variable and a stone is placed at the top of the heap. This stone sinks down until it reaches a point where the temporary can stop without breaking heap-order. The stone always sinks in the direction of the higher-priority child.

Code to implement these operations using an array-based binary heap is shown below. This extends the PriorityQueue[A] type that was created in chapter 26. Like the sorted linked-list implementation, a comparison function is passed in to provide the complete ordering of elements for instances of this class. The only data needed by this class is an array we call heap and an integer called end that keeps track of where the next element should be added. These are created with 10 elements to begin with, one of which will never be used as index zero is left empty, and the other is set to be 1.

```scala
package scalabook.adt

class BinaryHeapPriorityQueue[A : Manifest](comp: (A,A)=>Int) extends
    PriorityQueue[A] {
private var heap = new Array[A](10)
private var end = 1

def enqueue(obj:A) {
    if(end>=heap.length) {
        val tmp = new Array[A](heap.length*2)
        Array.copy(heap,0,tmp,0,heap.length)
        heap = tmp
    }
    var bubble = end
    while(bubble>=1 && comp(obj,heap(bubble/2))>0) {
        heap(bubble) = heap(bubble/2)
        bubble /= 2
    }
    heap(bubble) = obj
    end += 1
}

def dequeue():A = {
    val ret = heap(1)
    end -= 1
    val temp = heap(end)
    heap(end) = heap(0) // Clear reference to temp
    var stone = 1
    var flag = true
    while(flag && stone*2<end) {
        var greaterChild = if(stone*2+1<end && comp(heap(stone*2+1),heap(stone*2))>0)
            stone*2+1 else stone*2
        if(comp(heap(greaterChild),temp)>0) {
            heap(stone) = heap(greaterChild)
            stone = greaterChild
        } else {
            flag = false
        }
    }
    heap(stone) = temp
    ret
}

def peek:A = heap(1)

def isEmpty:Boolean = end==1
}
```

The enqueue method begins with a check to see if there is space in the array for a new element. If not, a bigger array is created. As with other similar pieces of code written in this book, the size of the array is doubled so that the amortized cost of copies will be O(1). The rest of the enqueue method makes an Int called bubble that will walk up the heap to find where the new element should go. It is initialized to end, the first unused location in the array. The main work is done in a while loop that goes as long as the bubble is greater than 1 and the parent of bubble, located at index bubble/2, has a higher-priority than the new element. When the loop terminates, the new element is placed at the location of the bubble and end is incremented.
