

- 在末尾添加，随机读取元素，随机设置元素，从末尾移除。
- 在随机位置添加，随机读取元素，随机设置元素，从随机位置移除。
- 在开头添加，随机读取元素，随机设置元素，从开头移除。
- 在随机位置添加，使用迭代器顺序读取元素，从随机位置移除。
- 4. 修改链表的代码，将使用 rover 遍历节点的操作抽取到一个单独的函数中，并在需要该行为的地方调用该函数。
- 5. 为链表测试代码添加更多测试。确保包含使用 remove 完全清空列表然后重新填充的情况。
- 6. 比较基于列表的栈与基于数组的栈在不同大小和不同使用模式下的速度。
- 7. 比较基于列表的队列与基于数组的队列在不同大小和不同使用模式下的速度。

### 25.8.3 Projects

本章的项目没有单独的描述。在所有项目中，你应该已经在使用某种形式的 Seq 或 Buffer 来存储重要数据。对于本项目，你需要将代码转换为使用你自己构建的链表类，而不是你一直在使用的 Scala 库类。

## Chapter 26 Priority Queues

- 26.1 Two Approaches ......................................................... 679
- 26.1.1 Searching by Priority ................................................... 680
- 26.1.2 Sorted Linked List ...................................................... 680
- 26.1.3 Problems with Arrays .................................................... 682
- 26.2 Project Integration: Discrete Event Simulation ................................ 683
- 26.2.1 Cell Splitting ........................................................... 683
- 26.2.2 Collision Handling ...................................................... 686
- 26.3 End of Chapter Material .................................................... 693
- 26.3.1 Summary of Concepts ..................................................... 693
- 26.3.2 Exercises ................................................................ 694
- 26.3.3 Projects ................................................................. 694

我们之前研究的队列抽象数据类型 ADT 可以被视为对服务线的建模。所有添加进去的实体都被视为相等，并且按到达顺序取出。并非所有系统都以这种公平的方式运作。在现实生活中，有 VIP 通道之类的东西。某些系统有充分的理由对实体进行不同对待。急诊室就是此类系统的例子。如果你带着纸割伤来到急诊室，你可以预期要等待很长时间。这是因为急诊室中人们被服务的顺序更多地基于病情的严重程度，而非到达时间。预约制的情况也是另一个例子。提前很久到达预约时间通常并不会让你显著提前就诊。

这类系统需要一种新的 ADT，即优先级队列。优先级队列具有与普通队列相同的方法，但 dequeue 和 peek 方法的行为不同，它们会给出队列中优先级最高的对象，并且只有当最高优先级项的优先级相等时才考虑在队列中的时间长短。

### 26.1 Two Approaches

本章我们将考虑两种不同的优先级队列实现方法，两者都使用链表进行存储。两者的区别在于是在向队列添加新项时做额外工作，还是将工作推迟到项被移除时。我们将讨论这两种方法并比较其效率，但只实现其中更好的那一种。与普通队列不同，优先级队列不可能对所有方法都获得 O(1) 性能。对于我们将讨论的实现，一些方法将是 O(n)。我们将在第 32 章讨论另一种可以改进这一点的实现。

所有优先级队列的实现都将扩展以下 trait。

```scala
package scalabook.adt

/**
 * This trait defines a mutable Priority Queue ADT.
 * @tparam A the type of data stored
 */
trait PriorityQueue[A] {
  /**
   * Add an item to the priority queue.
   * @param obj the item to add
   */
  def enqueue(obj:A)

  /**
   * Remove the item that has the highest priority or, in the case of a tie,
   * has been on the longest.
   * @return the item that was removed
   */
  def dequeue():A

  /**
   * Return the item that has the highest priority or, in the case of a tie,
   * has been on the longest without removing it.
   * @return the most recently added item
   */
  def peek:A

  /**
   * Tells whether this priority queue is empty.
   * @return true if there are no items on the priority queue, otherwise false.
   */
  def isEmpty:Boolean
}
```

### 26.1.1 Searching by Priority

一种使用链表创建优先级队列的方法是像普通队列一样将元素添加到尾部，但随后修改 dequeue 和 peek 中的代码，使其遍历元素以找到优先级最高的元素。在 dequeue 的情况下，该元素随后被移除。

我们可以通过查看每个方法所做的工作量来评估这种方法的质量。enqueue 和 isEmpty 方法将是 O(1)。然而，dequeue 和 peek 都必须搜索所有元素以找到优先级最高的元素。这需要 O(n) 时间。更深入地看，这个搜索特别昂贵，因为不可能在早期就知道我们在寻找什么，所以每次搜索都必须考虑每个元素。

### 26.1.2 Sorted Linked List

第二种方法是在元素添加时做额外工作，并保持列表有序，以便我们始终知道最高优先级项的位置并能高效地移除它。使用这种方法，dequeue、peek 和 isEmpty 方法都是 $O(1)$。**enqueue** 方法 however 必须执行搜索以找到正确的插入位置，因此是 $O(n)$。

这两种方法都至少包含一个 $O(n)$ 的方法。由于大多数应用程序对 **enqueue** 和 **dequeue** 的调用次数大致相等，且调用次数至少也是 $O(n)$，我们可以预期这两种实现整体性能为 $O(n^2)$。第二种方法对大多数应用程序更好，原因有几个。首先，**peek** 调用是 $O(1)$。虽然在逻辑上 **enqueue** 和 **dequeue** 的调用应该大致平衡，但 **peek** 的调用很容易比其他两个更多。此外，将项目放入有序列表不需要遍历整个列表。此过程类似于插入排序的内层循环。你只需要遍历列表直到找到放置新元素的位置即可。对于许多应用程序，新元素自然会比许多先前元素具有更低的优先级。这意味着代码在每次 **enqueue** 时平均只需与少于一半的元素进行比较，而另一种方法中 **dequeue** 和 **peek** 需要与所有元素进行比较。

以下是使用有序链表实现优先级队列的示例实现。

```scala
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
}
```
