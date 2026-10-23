
## FIGURE 35.3: This figure shows two arrays and possible tree representations for them. The second was arrived at by adding the letter 't' at index 5 of the first. In the tree, each node has the value, a letter, drawn large with a preceding number that is the size of the node and a following number that is the index.

Both the BST and the AVL tree have been used to implement the map ADT. The type we are describing here is a sequence. This is significant because the map ADT needs a key value that has an ordering by which data can be accessed. In a sequence, things are accessed by an index, not a key. What is more, the index of an element can change if other items are inserted or removed before it. The key for a map has to be immutable. Using mutable keys is a great way to produce errors with a map. So how does this work, and what does the size augmentation have to do with it?

Assume a binary tree where we say that the index is the key. This is much like a sequence where you look up values by the index. Figure 35.3 shows what this might look like. Letters have been used as the data here. On the left there is a sequence with nine characters in it and a balanced tree that has the same nine characters with numeric annotations. The number before the letter is the size of the node. The number after it is the index. On the right the letter 't' has been inserted at index 5. Note how this changes the index values of all the letters which had indexes greater than or equal to 5.

To use the tree as a sequence, we have to have an efficient way of finding nodes based on index. That would allow us to to direct access, as well as finding nodes or positions for inserting and removing. The key to associating index with nodes is in the size. The first indication of this is that the size of the node for 'o' is the same as the index of the root, 'h'. This is not coincidence. The size of 'o' is the number of nodes that are "before" the root in the sequence. Since indexes begin at 0, the index of the root should be the size of the left child. This logic holds throughout the tree so having the size allows us to do a binary search through an index.

To see this, assume that we want to find the item at index 6. We start by looking at the size of the left child. It is 4, which is less than 6. This tells us that what we are looking for is on the right side of the tree. This is the signature of a binary search. We do one comparison and it allows us to throw out half the data. So we go to the right child. We are not looking for index 6 on the right child though. Instead, we are looking for index 1. The left child was the first 4 and the root itself was another. So we have thrown out the first 5 elements and we subtract that from the index we are looking for.

So after one comparison we are on the subtree with ‘z’ at the top looking for index 1. The size of the left child is 2. This is larger than the index we are looking for, so we go to the left. When we move to the left, the index stays the same because we are not jumping past any elements. After two comparisons we are on ‘c’ looking for index 1. The left child of ‘c’ is empty and therefore has a size of zero. That is smaller than the index we are looking for so we go to the right and subtract 1 from the index we are looking for because we skipped the node with ‘c’. We are now on the node with ‘q’ looking for index 0. The left child of ‘q’ is empty, giving it size zero, the same as the index we are looking for, and therefore ‘q’ is the value we are looking for.

This process illustrates how storing the size only can let us find values at indexes in a number of operations proportional to the height of the tree. That is slower than for an array, but significantly faster than what a linked-list would provide.

What would happen if we looked at index 6 again after adding the ‘t’? Again, we start at ‘h’ and see the left child has size 4. Then we move to ‘z’ on the right looking for index 1. The left child has size 3 so we move to the left, still looking for index 1. The left child of ‘c’ has a size of 1 meaning that ‘c’ is the node we are looking for.

This same type of searching could be done with an index annotation. However, an index annotation can not be maintained efficiently. To see this, look closely at the differences between the numbers annotating the nodes in figure 35.3. The size values only changed for the nodes with ‘c’, ‘z’, and ‘h’. That is the path from the new node up to the root, a path that will have length $O(\log(n))$ in a balanced tree. The index annotation has changed for ‘c’, ‘q’, ‘z’, and ‘p’. The is everything after the inserted value. In this case the difference is 3 to 4, but you can picture putting the new value at index 1 to see that the number of indexes that need to change scales as $O(n)$. This tells us that we want to augment our nodes with size, not index values.

The code below is an implementation of an order-statistic tree that extends the `mutable.Buffer` trait. This class uses internals classes for `Node` and `INode` as well as an internal object declaration for `Empty`. While this mirrors some of the style of the immutable tree in the last section, this tree is mutable and everything in `INode` is a `var`. While this uses a similar class structure to the immutable AVL tree, it has a very different implementation with more overloaded methods and a lot fewer uses of `match`.

The code for the `Buffer` methods themselves are generally short, as are the methods in `Empty`. The majority of the code is in `INode`, specifically in the methods for removing and rotating. The use of `Empty` with methods for `+`, `+:`, and `insert` keep the insertion code short. The recurring theme we see in this code is comparing an index to the size of the left child.

```
package scalabook.adt

import collection.mutable

class OrderStatTreeBuffer[A] extends mutable.Buffer[A] {
  abstract private class Node {
    def size: Int
    def height: Int
    def +(elem: A): Node
    def +::(elem: A): Node
    def apply(n: Int): A
```

```
def remove(n:Int):(A,Node)
def removeMin:(A,Node)
def update(n:Int, elem:A):Unit
def insert(n:Int, elem:A):Node
def rotate:Node
}
```

```
private class INode(var data:A, var left:Node, var right:Node) extends Node {
 var size = 1+left.size+right.size
 var height = 1+(left.height max right.height)

 private def setSizeAndHeight {
 size = 1+left.size+right.size
 height = 1+(left.height max right.height)
 }

def +(elem:A):Node = {
 right += elem
 setSizeAndHeight
 rotate
 }

def ++:(elem:A):Node = {
 left += elem
 setSizeAndHeight
 rotate
 }

def apply(n:Int):A = {
 if(n==left.size) data
 else if(n<left.size) left(n)
 else right(n-left.size-1)
}

def remove(n:Int):(A,Node) = {
 val ret = if(left.size==n) {
 val d = data
 if(right==Empty) (data,left)
 else if(left==Empty) (data,right)
 else {
 val (newData,r) = right.removeMin
 right = r
 data = newData
 setSizeAndHeight
 (d,this)
 }
 } else if(left.size>n) {
 val (d,l) = left.remove(n)
 left = l
 setSizeAndHeight
 (d,this)
 } else {
 val (d,r) = right.remove(n-left.size-1)
 right = r
 setSizeAndHeight
```

```
(d,this)
}
(ret._1,ret._2.rotate)
}

def removeMin: (A,Node) = if(left==Empty) (data,right) else {
  val (d,l) = left.removeMin
  left = l
  setSizeAndHeight
  (d,rotate)
}

def update(n:Int, elem:A) {
  if(n==left.size) data = elem
  else if(n<left.size) left(n) = elem
  else right(n-left.size-1) = elem
}

def insert(n:Int, elem:A):Node = {
  if(n<=left.size) left = left.insert(n,elem)
  else right = right.insert(n-left.size-1,elem)
  setSizeAndHeight
  rotate
}

def rotate:Node = {
  if(left.height>right.height+1) {
    left match {
      case lNode:INode => // Always works because of height.
        if(lNode.left.height>lNode.right.height) {
          rotateRight
        } else {
          left = lNode.rotateLeft
          rotateRight
        }
      case _ => null // Can't happen.
    }
  } else if(right.height>left.height+1) {
    right match {
      case rNode:INode => // Always works because of height.
        if(rNode.right.height>rNode.left.height) {
          rotateLeft
        } else {
          right = rNode.rotateRight
          rotateLeft
        }
      case _ => null // Can't happen.
    }
  } else this
}

private def rotateLeft:INode = right match {
  case rNode:INode =>
    right = rNode.left
    rNode.left = this
```
