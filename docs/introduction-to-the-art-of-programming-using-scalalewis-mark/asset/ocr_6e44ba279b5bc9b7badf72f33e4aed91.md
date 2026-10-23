# 25.5 Mutable Doubly-Linked List

Now we want to consider a doubly-linked list. The obvious advantage of a doubly-linked list over a singly-linked list is that it can be traversed in either direction. This comes with the cost of an extra reference per node and extra code to handle it. However, as we saw in the last section, the main source of additional code was not handling the next references, but dealing with the special cases for head and tail references. Fortunately, there is a way we can remove that special case code when we are using a doubly-linked list so that handling the previous reference is more than compensated for. The way we do this is through the introduction of a special node called a sentinel.

A sentinel is an extra node that does not store data, but which functions as both the beginning and end of the list. To make this possible the list needs to be circular. If we call the sentinel end then end.next is the head of the list and end.prev is the tail of the list. This alteration saves a significant amount of code because how the head and tail are just next and prev references, so adding and removing at those locations is no different from doing so at other locations.

Code for this implementing the Buffer trait is shown here. The declarations at the top of the class are very similar to those in the singly-linked list, except that there is one one node reference called end and initially the next and prev of that node are set to point back to it. There are two other points to note about the top part of this class. The end node has to be given a data value. This causes a bit of a problem because there is not any single value that can be used as the default for the type parameter A. To get around this we use the approach seen with our array-based stacks and queues of requiring the type have a manifest and then the data in end is set by making an array with one element and using that first element. There are other solutions to this that use inheritance, but they require more code and potentially obfuscate the purpose of this example.

```
package scalabook.adt

import collection.mutable

class MutableDLLIst[A : Manifest] extends mutable.Buffer[A] {
  private var num = 0
  private class Node(var data:A, var prev:Node, var next:Node)
  private val end = new Node(new Array[A](1)(0),null,null)
  end.next = end
  end.prev = end

  def +=(elem: A) = {
    val newNode = new Node(elem,end.prev,end)
    end.prev.next = newNode
    end.prev = newNode
    num += 1
    this
  }

  def +=:(elem: A) = {
    val newNode = new Node(elem,end,end.next)
    end.next.prev = newNode
    end.next = newNode
    num += 1
```