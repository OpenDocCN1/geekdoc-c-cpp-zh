```
def +=(elem: A): Buffer.this.type
def +=(elem: A): Buffer.this.type
def apply(n: Int): A
def clear(): Unit
def insertAll(n: Int, elems: Traversable[A]): Unit
def iterator: Iterator[A]
def length: Int
def remove(n: Int): A
def update(n: Int, newelem: A): Unit
```

This means that if we want to extend the mutable.Buffer type we must implement these nine methods. The reward for doing this is that the large number of other methods that are part of mutable.Buffer will automatically work for us. This happens because those other methods are implemented in terms of the those nine abstract methods. So for the cost of nine you get many, many others.

The following code shows an implementation of just such a class. This implementation keeps track of both a head and a tail for the list. They are called hd and tl so that they do not conflict with the head and tail members that are part of the general Scala sequence. The class also keeps track of an Int named num so that calls to length and bounds checking can both be done efficiently.

```
package scalabook.adt

import collection.mutable
```

```
class MutableSList[A] extends mutable.Buffer[A] {
  private var hd:Node = null
  private var tl:Node = null
  private var num = 0
  private class Node(var data:A, var next:Node)

  def +=(elem: A) = {
    if(tl==null) {
      tl = new Node(elem,null)
      hd = tl
    } else {
      tl.next = new Node(elem,null)
      tl = tl.next
    }
    num += 1
    this
  }

  def +=(elem: A) = {
    hd = new Node(elem,hd)
    if(tl==null) {
      tl = hd
    }
    num += 1
    this
  }

  def apply(n: Int): A = {
    if(n<0 || n>=num) throw new IndexOutOfBoundsException(n+" of "+num)
    var rover = hd
```