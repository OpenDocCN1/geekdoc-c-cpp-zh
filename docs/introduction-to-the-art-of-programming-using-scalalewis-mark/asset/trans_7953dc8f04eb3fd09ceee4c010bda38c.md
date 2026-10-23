

链表可以组织成常规或循环配置。在常规配置中，列表的末端（第一个或最后一个元素）由空引用表示。在循环配置中，这些引用会指向列表的另一端。

程序必须始终跟踪链表的至少一个元素。对于常规单链表，这必须是头。列表中的所有元素都可以通过头访问，但由于引用是单向的，如果你丢失了对头的引用，那么在你保留的节点之前的所有节点都将丢失。图示在列表的另一端显示了另一个引用到尾部。存储尾部通常不是必需的，但它可以使某些操作显著加快。特别是，如果不跟踪尾部，向可变列表末尾添加元素的时间复杂度为 O(n)，但如果跟踪尾部，则可以在 O(1) 时间内完成。因此，出于这个原因，我们将在最终的可变单链表中跟踪尾部，尽管这会给代码增加相当多的复杂性。

## 25.4 可变单链表

我们将实现的第一个链表形式是一个非常基础的可变单链表。我们将只包含上面列出的四个方法，即使这种最小实现并不太有用。从这里开始是有启发性的，这样其他方法的细节就不会妨碍你的理解。

下面的类展示了这样的链表可能是什么样子。get 和 set 方法已被更改为 apply 和 update 以利用 Scala 对这些特殊方法的语法规则，但它们内部的逻辑没有改变。

```scala
package scalabook.adt

/**
 * This is a very simple implementation of a basic linked list.
 * @tparam A the type stored in the list.
 */
class SinglyLinkedList[A] {
  private class Node(var data:A, var next:Node)
  private var head:Node = null

  /**
   * This method gets the value at a specified index. If the index is beyond the
   * length of the list a NullPointerException will be thrown.
   * @param index the index to get.
   * @return the value at that index.
   */
  def apply(index:Int) : A = {
    assert(index>=0)
    var rover = head
    for(i <- 0 until index) rover = rover.next
    rover.data
  }

  /**
   * Sets the value at a particular index in the list. If the index is beyond the
   * length of the list a NullPointerException will be thrown.
   * @param index the index to set the value at.
   * @param data the value to store at that index.
   */
  def update(index:Int, data:A) {
    assert(index>=0)
    var rover = head
    for(i <- 0 until index) rover = rover.next
    rover.data = data
  }

  /**
   * Inserts a new value at a particular index in the list. If the index is beyond
   * the length of the list a NullPointerException will be thrown.
   * @param index the index to set the value at.
   * @param data the value to insert at that index.
   */
  def insert(index:Int, data:A) {
    assert(index>=0)
    if(index==0) {
      head = new Node(data,head)
    } else {
      var rover = head
      for(i <- 0 until index-1) rover = rover.next
      rover.next = new Node(data,rover.next)
    }
  }

  /**
   * Removes a particular index from the list. If the index is beyond the length
   * of the list a NullPointerException will be thrown.
   * @param index the index to remove.
   * @return the data value that had been stored at that index.
   */
  def remove(index:Int) : A = {
    assert(index>=0)
    if(index==0) {
      val ret = head.data
      head = head.next
      ret
    } else {
      var rover = head
      for(i <- 0 until index-1) rover = rover.next
      val ret = rover.next.data
      rover.next = rover.next.next
      ret
    }
  }
}
```

该类采用一个名为 A 的类型参数，表示列表中数据的类型。该类包含一个名为 Node 的私有小类，用于存储对数据和对下一个节点的引用。链表类还通过一个名为 head 的变量跟踪列表的头。

该类中的四个方法都相当简单，并且包含非常相似的结构。让我们先看 apply 方法。它以一个 assert 开始，以确保索引不小于零。注释还说，如果提供超出列表长度的索引，将抛出 NullPointerException。虽然这对于我们当前的需求来说已经足够，但这并不是理想的行为。如果请求超出边界的索引，抛出一个包含请求内容和数量信息的适当异常会好得多。这个缺陷将在稍后更完整的实现中得到纠正。

此类中的所有方法都声明了一个名为 rover 的变量，用于遍历列表。对于数组，我们通过使用索引计数来遍历元素。节点不必在内存中连续，因此我们必须通过从一个节点跟随引用到另一个节点来遍历元素。这就是 for 循环内部的赋值 `rover = rover.next` 所做的。

> 问题：你如何从这个简单的链表实现中删除重复代码？

insert 和 remove 方法有一个 apply 和 update 中都没有的元素，即处理列表开头的特殊情况。insert 和 remove 都会更改列表中的引用，并且必须为第一个元素的情况包含特殊处理。正常情况会更改 next 引用，而特殊情况会更改 head。

读者还应注意到 insert 和 remove 中的 for 循环只运行 n−1 次。这是因为在单链表中，添加或删除一个节点需要更改其前一个节点的 next 引用。如果你想删除索引 3 处的节点，你必须拥有索引 2 处节点的引用，并将其 next 引用更改为指向当前索引 4 处的节点。这就是 `rover.next = rover.next.next` 行发生的情况。如果 rover 一直走到我们想要删除的节点，我们将无法访问需要修改的引用，因为单链表中无法向后移动。

为了说服自己这段代码有效，我们可以实现以下测试来进行一些最小检查。

```scala
package test.scalabook.adt

import org.junit._
import org.junit.Assert._
import scalabook.adt._

class TestSinglyLinkedList {
  var list:SinglyLinkedList[Int] = null

  @Before def setup {
    list = new SinglyLinkedList[Int]
  }

  @Test def appendOne {
    list.insert(0,10)
    assertEquals(10,list(0))
  }

  @Test def appendTwo {
    list.insert(0,10)
    list.insert(0,20)
```

```scala
def +=(elem: A): Buffer.this.type
def +=:(elem: A): Buffer.this.type
def apply(n: Int): A
def clear(): Unit
def insertAll(n: Int, elems: Traversable[A]): Unit
def iterator: Iterator[A]
def length: Int
def remove(n: Int): A
def update(n: Int, newelem: A): Unit
```

这意味着如果我们想扩展 mutable.Buffer 类型，我们必须实现这九个方法。回报是，mutable.Buffer 的大量其他方法将自动为我们工作。这是因为那些其他方法是以这九个抽象方法为基础实现的。所以花费九个方法就可以获得许多其他方法。

下面的代码展示了这样一个类的实现。此实现同时跟踪头和尾，分别称为 hd 和 tl，以便它们不与 Scala 序列中通用的 head 和 tail 成员冲突。该类还跟踪一个名为 num 的 Int，以便对 length 和边界检查都可以高效完成。

```scala
package scalabook.adt

import collection.mutable

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

  def +=:(elem: A) = {
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

