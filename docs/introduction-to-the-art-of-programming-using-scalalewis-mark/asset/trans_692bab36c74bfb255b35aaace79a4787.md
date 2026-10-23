

```
this
}

def apply(n: Int): A = {
    if(n<0 || n>=num) throw new IndexOutOfBoundsException(n+" of "+num)
    var rover = end.next
    for(i <- 0 until n) rover = rover.next
    rover.data
}

def clear() {
    end.prev = end
    end.next = end
    num = 0
}

def insertAll(n: Int, elems: Traversable[A]) {
    if(n<0 || n>=num+1) throw new IndexOutOfBoundsException(n+" of "+num)
    if(elems.nonEmpty) {
        var rover = end.next
        for(i <- 0 until n) rover = rover.next
        for(e <- elems) {
            val newNode = new Node(e,rover.prev,rover)
            rover.prev.next = newNode
            rover.prev = newNode
            num += 1
        }
    }
}

def iterator = new Iterator[A] {
    var rover = end.next
    def hasNext = rover!=end
    def next:A = {
        val ret = rover.data
        rover = rover.next
        ret
    }
}

def length : Int = num

def remove(n: Int): A = {
    if(n<0 || n>=num) throw new IndexOutOfBoundsException(n+" of "+num)
    num -= 1
    var rover = end.next
    for(i <- 0 until n) rover = rover.next
    val ret = rover.data
    rover.prev.next = rover.next
    rover.next.prev = rover.prev
    ret
}

def update(n: Int, newelem: A) {
    if(n<0 || n>=num) throw new IndexOutOfBoundsException(n+" of "+num)
    var rover = end.next
    for(i <- 0 until n) rover = rover.next
    rover.data = newelem
  }

  override def toString = mkString("MutableDLLST(", ", ", ")")
}
```

其他方法在你看过单向链表之后应该相当直接。最大的变化是每个节点-节点链接需要分配两个指针，并且所有的特殊情况代码都消失了。总的来说，这个版本更短、更不复杂、更不容易出错，因为去除了特殊情况代码。读者应该画图来看看像 `rover.prev.next = rover.next` 这样的行的效果。*remove* 中的这一行特别利用了双向链表可以向前和向后遍历的事实，因此对我们要删除的节点的引用就足够了。我们不需要像单向链表那样拥有对前一个节点的直接引用。

## 通过继承使用哨兵

强制类型具有显式声明并仅仅为了在哨兵中存储一个数据值而创建一个小数组，从风格上讲是不理想的。有一种替代方案。使用继承，我们可以创建一个特殊的节点类型来表示哨兵，它本身不包含数据。以下是使用该方法编写的替代代码。

```
class MutableDLLST[A] extends mutable.Buffer[A] {
  private var num = 0
  private trait Node {
    var data:A
    var prev:Node
    var next:Node
  }
  private class DNode(var data:A, var prev:Node, var next:Node) extends Node
  private class ENode extends Node {
    def data:A = throw new IllegalArgumentException("Requested value of sentinel node.")
    def data_=(d:A) = throw new IllegalArgumentException("Value assigned to sentinel node.")
    var next:Node = this
    var prev:Node = this
  }
  private val end = new ENode
}
```

使用这种方法，`Node` 类型现在是一个 *trait*，其子类型为 `DNode` 和 `ENode`。节点定义了我们之前在 `Node` 中拥有的不同字段的抽象 `vars`。`DNode` 类型继承自它，并且在其他方面看起来与我们原来的 `Node` 类完全一样。这种方法不同之处在于用于哨兵的 `ENode`。该类对 `next` 和 `prev` 使用常规的 `var` 声明，但对 `data` 的处理则完全不同。不是声明一个 `var`，而是有两个 `def` 声明用于获取和设置 `data`。这两个都抛出异常而不是返回一个值。这之所以可行，是因为 `var` 声明实际上

编译成这些 getter 和 setter 方法，而 throw 表达式的类型是 Nothing，它是 Scala 中每种其他类型的子类型。

在这两种方法之间的选择大多是风格问题，但这里使用继承可能会导致编译后的代码稍慢一些。继承的方法使用虚拟函数调用，其开销比调用没有任何覆盖的 final 方法更大。编译器是否在这种情况下生成更慢的代码取决于编译器。在你自己的平台上测试这一点留给读者作为练习。

## 25.6 不可变单向链表

我们之前查看的两个链表实现都是可变链表。因此我们可以实例化一个列表然后以各种方式修改其内容。这与 Buffer trait 配合得很好，但事实证明我们在 Scala 中工作的第一个链表类是 List 类，它表示一个不可变链表。

不可变链表只有作为单向链表才有意义，因为不允许更改数据或链接。一旦列表创建，它必须完全保持完整和不变。添加到列表前端的操作，即我们用 :: 完成的操作，会在不以任何方式改变之前节点的情况下附加一个新节点。与可变链表不同，可变链表将列表包裹在节点周围并将其隐藏，在不可变链表中，节点就是列表。它们周围没有任何东西被包裹。

下面的代码给出了一个不可变单向链表的实现。这使用了与 List 类本身类似的设计。不是单个类，而是一个小型层次结构，我们通常用来引用列表的主要类是抽象的，并且有两个子类型来表示空节点和非空节点。

```
package scalabook.adt

import collection.immutable.LinearSeq

sealed abstract class ImmutableSLList[+A] extends LinearSeq[A] {
  def ::[B >:A](elem:B):ImmutableSLList[B] = new Cons(elem,this)
  override def iterator = new Iterator[A] {
    var rover:LinearSeq[A] = ImmutableSLList.this
    def hasNext = !rover.isEmpty
    def next = {
      val ret = rover.head
      rover = rover.tail
      ret
    }
  }
}

final class Cons[A](hd:A,tl:ImmutableSLList[A]) extends ImmutableSLList[A] {
  def length = 1+tl.length
  def apply(index:Int):A = if(index==0) hd else tl.apply(index-1)
  override def isEmpty = false
  override def head = hd
  override def tail = tl
}
```

```
object MyNil extends ImmutableSLList[Nothing] {
  def length = 0
  def apply(index:Int) = throw new IllegalArgumentException("Nil has no contents.")
  override def isEmpty = true
  override def head = throw new IllegalArgumentException("Nil has no head.")
  override def tail = throw new IllegalArgumentException("Nil has no tail.")
}
```

```
object ImmutableSLList {
  def apply[A](data:A*):ImmutableSLList[A] = {
    var ret:ImmutableSLList[A] = MyNil
    for(d <- data.reverse) {
      ret = new Cons(d,ret)
    }
    ret
  }
}
```

这段代码中有一些我们之前没有见过的内容，可能需要一些解释。从顶部开始，主要类被标记为 sealed 和 abstract。我们见过 abstract，但 sealed 是新的。这个关键字所暗示的是，该类的所有子类型都必须出现在当前文件中。这可以用来为模式匹配提供更好的类型检查。在这种情况下，它提供了我们知道其他程序员不能产生与我们对列表期望的行为不同的不良子类型的保障。通常我们可以用 final 来强制执行这一点，以确保没有任何东西继承自一个类。在这种情况下这不是一个选项，因为我们需要一些继承。

接下来是 ImmutableSLList 的类型参数。它是 +A 而不是只是 A。加号表示列表在类型参数上是协变的。这是一个在附录 B 中更详细讨论的话题。现在只需说这意味着如果 B 是 A 的子类型，那么 ImmutableSLList[B] 就是 ImmutableSLList[A] 的子类型。如果没有加号，类型参数是不变的，并且不同类型参数的类型的类在有效上是无关的。

类中的第一个方法是 ::，以模仿标准 List 类中使用的那个。这个奇怪之处在于类型参数的边界。这是我们第一次看到 >: 类型边界的使用。这表示我们可以使用任何类型 B，只要它与 A 相同或 A 的超类型。这一符号在 19.4.3 小节中提到过，但在现在之前我们没有用武之地。为了看看这会产生什么效果，考虑在 REPL 中使用标准 List 的以下代码。

```
scala> val nums = List(1,2,3)
nums: List[Int] = List(1, 2, 3)

scala> "hi" :: nums
res0: List[Any] = List(hi, 1, 2, 3)
```

注意 res0 的类型。它是 List[Any]。我们的列表也会以相同的方式表现。新的元素 "hi" 不是一个 Int，所以 Scala 必须找出一个类型 B 来使用。String 和 Int 的唯一超类型是 Any，所以那就是使用的类型。如果继承层次结构中更低位置存在一个共同超类型，则会改用它。

在 iterator 方法中，rover 的声明需要一个显式的类型，因为

