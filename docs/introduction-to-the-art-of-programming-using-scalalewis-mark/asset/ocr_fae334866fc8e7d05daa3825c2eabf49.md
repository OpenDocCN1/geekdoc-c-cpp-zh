$O(1)$. The **enqueue** method, however, must perform a search to find the correct insertion locations, and is therefore $O(n)$.

Both of these approaches contain at least one method which is $O(n)$. As most applications will have roughly equal numbers of calls to **enqueue** and **dequeue**, and the number of calls will be at least $O(n)$ as well, we can expect either of these implementations to have an overall performance of $O(n^2)$. This second approach is better for most applications for a few reasons. The first is that calls to **peek** are $O(1)$. While there is a logical reason why calls to **enqueue** and **dequeue** should roughly balance, there could easily be more calls to **peek** than either of the other two. In addition, placing items into a sorted list does not require walking the full list. This procedure is like what happens in the inner loop of an insertion sort. You only have to walk through the list until you find the right place to put the new element. For many applications, new elements will have a naturally lower priority than many previous elements. This means that the code will do comparisons to fewer than half the elements, on average, for each **enqueue**, compared to comparisons of all elements for **dequeue** and **peek** in the other approach.

Here is a listing of a sample implementation of a priority queue using a sorted linked list.

```
```scalabook.adt
package scalabook.adt

class SortedListPriorityQueue[A : Manifest](comp: (A,A)=>Int) extends
PriorityQueue[A] {
 private class Node(var data:A, var prev:Node, var next:Node)
 private val end = new Node(new Array[A] (1) (0),null,null)
 end.next = end
 end.prev = end

 def enqueue(obj:A) {
   var rover = end.prev
   while(rover!=end && comp(obj,rover.data)>0) rover = rover.prev
   rover.next.prev = new Node(obj,rover,rover.next)
   rover.next = rover.next.prev
 }

 def dequeue():A = {
   val ret = end.next.data
   end.next = end.next.next
   end.next.prev = end
   ret
 }

 def peek:A = end.next.data

 def isEmpty:Boolean = end.next==end

 def removeMatches(f: A => Boolean) {
   var rover = end.next
   while(rover!=end) {
     if(f(rover.data)) {
       rover.prev.next = rover.next
       rover.next.prev = rover.prev
     }
     rover=rover.next
   }
 }
}```
```