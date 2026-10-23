

rover.tail 是父类型的一个方法。同样值得注意的是，rover 被初始化为当前节点。这是以下事实带来的副作用：在这种实现中，节点并非隐藏在一个列表中，它们本身就是列表。实际上，每个节点要么作为空列表，要么作为某个列表的头部来表示一个列表。

主类的定义之后是两个子类型。第一个表示非空节点，在这里被称为 Cons，它保存该节点中的数据元素以及列表中其余部分对应的节点。为了完成 LinearSeq，该类必须实现 length 和 apply。为了使实现对标准用法更高效，我们还重载了 isEmpty、head 和 tail。这些相同的方法也放在表示空列表的对象 MyNil 中。它是一个对象，因为我们只需要存在一个这样的对象。它扩展了 ImmutableSLList[Nothing]，从而可以成为任何列表类型的子类型。这就是 ImmutableSLList 相对于 A 的协变性变得重要的地方。如果没有这一点，每种列表类型都需要一个单独的空列表对象。

代码最后是一个带有 apply 方法的伴生对象。这使我们能够使用习惯上用于 List 的相同语法来创建新的列表类型。

一些测试代码可以很好地展示我们列表的用法。你可以看到，它在功能上与普通的 List 类型非常相似。

```
package test.scalabook.adt

import org.junit._
import org.junit.Assert._
import scalabook.adt._

class TestImmutableSLList {
    @Test def nilIsEmpty {
        assertTrue(MyNil.isEmpty)
    }

    @Test def buildCons {
        val lst = 1 :: 2 :: 3 :: MyNil
        assertEquals(3,lst.length)
        assertEquals(1,lst.head)
        assertEquals(2,lst(1))
        assertEquals(3,lst(2))
    }

    @Test def buildApply {
        val lst = ImmutableSLList(1,2,3)
        assertEquals(3,lst.length)
        assertEquals(1,lst.head)
        assertEquals(2,lst(1))
        assertEquals(3,lst(2))
    }
}
```

我们的代码不会做的一件事是在 :: 上进行模式匹配。要实现这一点需要更高级的技术，这些技术留待附录介绍。

实际的 scala.collection.immutable.List 代码比我们这里编写的代码更复杂，但主要是为了引入更高的效率。这个类完全不可变，也就是说，任何节点一旦创建就永远不能改变。这迫使我们在希望获得任何效率时，只能通过将新节点添加到头部来构建列表。这一点出现在我们代码的末尾：在 for 循环中，apply 方法的输入被反转。这是一种开销，真正的库版本设法绕过了这种开销。

## 25.7 基于链表的栈和队列

回顾一下，ADT 的主要特征是它告诉我们不同的方法是做什么的，而不是它们如何实现。链表是一种实际实现，正如我们所见，它可以用来实现列表 ADT。它也可以用作其他 ADT 的存储机制。特别是，对于目前所考虑的仅有的其他 ADT——栈和队列，它也能很好地工作。与基于数组的实现一样，我们要求这些集合上的所有操作都是 O(1)，因为它们在根本上是简单的。

### 25.7.1 基于链表的栈

为了用链表实现栈，我们可以把在前面某一节中编写的某个列表的实例作为成员放入这个类中，并对其进行操作。从软件工程的角度来看，这种方法是有价值的，因为代码复用可以显著提高生产力。然而，本章的重点是链表的性质和结构。为此，从头构建，并在这个类中包含一个节点类型以及直接操作它的代码，是有价值的。这种方法还有助于我们更好地控制所写代码的效率。

下面展示了一个使用单向链表实现的栈。Node 类型使用 case class 创建，因为其中的值不会改变。这为创建不可变节点提供了一种简便方法。

```
package scalabook.adt

class ListStack[A] extends Stack[A] {
    private case class Node(data:A, next:Node)
    private var top:Node = null
    
    def push(obj:A) {
        top = Node(obj, top)
    }
    
    def pop():A = {
        assert(!isEmpty, "Pop called on an empty stack.")
        val ret = top.data
        top = top.next
        ret
    }
    
    def peek:A = top.data
    
    def isEmpty:Boolean = top==null
}
```

top 成员是一个 var，充当链表的头部。这些方法的实现非常直接了当。如你所见，这是一个非常短的类，即使我们在这里重新实现了一个单向链表。这种简洁性是可能的，因为栈 ADT 本身很简单。不需要循环或复杂逻辑，因为所有访问（添加和删除）都发生在栈顶。

这个类的测试代码与 ArrayStack 的测试代码完全相同，只是把 Array 一词换成了 List。在这些替换中，只有一处是功能性的而非表面性的，即 @Before 方法中栈的实例化。

### 25.7.2 基于链表的队列

可以使用相同的过程来创建一个使用链表存储数据的队列。对于栈，我们只需要维护链表的一端，既可以添加也可以删除。对于队列，我们需要跟踪链表的两端。其中一端是 front，另一端是 back。哪一端是 head、哪一端是 tail，取决于我们需要实现的功能。新元素应从 back 添加，从 front 移除。我们刚刚看到，head 可以高效地完成这两种操作。那么 tail 呢？

对于单向链表，我们只能高效地在 tail 处添加，却不容易从那里删除。这又回到了那个问题：要从单向链表中删除某个节点，你需要知道被删除节点前面的那个节点，而我们不能反向遍历链表。因此，如果我们要保持 O(1) 性能，队列的 back 必须是链表的 tail。

下面展示了基于链表的队列代码。有一些额外的特殊情况需要处理，这使得该代码比栈的代码长一些。特别是，当向空队列添加元素，或者删除操作取走队列中最后一个元素时，需要对 back 进行调整。

```
package scalabook.adt

class ListQueue[A] extends Queue[A] {
  private class Node(val data:A,var next:Node)
  private var front:Node = null
  private var back:Node = null

  def enqueue(obj:A) {
    if(front==null) {
      front = new Node(obj,null)
      back = front
    } else {
      back.next = new Node(obj,null)
      back = back.next
    }
  }

  def dequeue():A = {
    assert(!isEmpty,"Dequeue called on an empty queue.")
    val ret = front.data
    front = front.next
    if(front==null) back = null
    ret
  }

  def peek:A = front.data

  def isEmpty:Boolean = front==null
}
```

## 25.8 章末材料

### 25.8.1 概念总结

- 比栈或队列稍微复杂一点的 ADT 是 List/Seq ADT。这个 ADT 提供了随机访问元素的方法。
- 我们一直在使用的数组以单一内存块的形式存储，可以容纳所需数量的引用。这意味着当你知道内存块的位置时，你就知道每个元素的位置。然而，插入和删除很慢。
- 链表是以顺序方式存储值的一种替代方法。它不是使用一个大内存块，而是由节点组成，每个节点链接到一个或两个其他节点。链表至少跟踪一个节点，然后可以从该节点到达其他节点。这使得随机访问变慢，但插入和删除可以通过 O(1) 次内存移动完成。
- 在单向链表中，每个节点保存对位于它前方的那个节点的引用，链表必须跟踪第一个节点。它也可以跟踪最后一个节点。这些边界成为特殊情况，使代码更复杂。
- 双向链表的节点保存对下一个元素和前一个元素的引用。它们最好使用哨兵节点来实现，该节点不存储数据，实际上就是链表中的第一个和最后一个节点。哨兵节点使双向链表的代码保持简短，无需处理特殊情况。
- 虽然链表的随机访问很慢，但迭代器允许高效的线性访问。
- 单向链表也可以写成不可变的。List 类型正是这样做的。在这类代码中，节点本身表示一个列表，并且有一个专门表示空列表的对象。
- ADT 不规定具体实现方式这一事实，可以通过使用链表作为数据存储机制重新实现栈和队列 ADT 来加以说明。

### 25.8.2 练习

1. 编写列表 ADT 的基于数组的实现。你可以选择只实现本章第一节列出的四个方法，或者实现 Buffer trait。
2. 使用下面一组操作，比较你的基于数组的列表和链表的速度。
3. 比较使用两种不同节点类型的双向链表的速度。

