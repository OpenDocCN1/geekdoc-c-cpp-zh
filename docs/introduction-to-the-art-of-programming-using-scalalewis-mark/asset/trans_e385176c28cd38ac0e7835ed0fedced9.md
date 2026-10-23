

```
```
 raf.seek(pos)
 pos = raf.readLong()
 i += 1
}
reader(raf)
}

def clear() {
 raf.seek(ltail)
 raf.writeLong(localFirstFree)
 localFirstFree = lhead
 lhead = -1
 ltail = -1
 length = 0
}

def insertAll(n:Int, elems:Traversable[A]) {
 if(n>length) throw new IllegalArgumentException("Insert at index "+
 " of "+length)
 var i = 0
 var (prev,next) = if(n==0) (-1L,lhead) else {
 var (pp,nn) = (lhead,-1L)
 while(i<n) {
 raf.seek(pp)
 if(i<n-1) pp = raf.readLong()
 else nn = raf.readLong()
 i += 1
}
 (pp,nn)
}
 if(prev != -1L) raf.seek(prev)
 for(elem <- elems) {
 val npos = newNodeePosition
 if(prev == -1L) {
 lhead = npos
 prev = npos
 } else raf.writeLong(npos)
 raf.seek(npos+8)
 writer(raf,elem)
 raf.seek(npos)
}
 if(next == -1L) ltail = raf.getFilePointer()
 raf.writeLong(next)
 length += elems.size
}

def iterator = new Iterator[A] {
 var pos = lhead
 def hasNext = lhead > -1L
 def next = {
 raf.seek(pos)
 pos = raf.readLong()
 reader(raf)
}
}
```
```

```
```
def length:Int = localLen.toInt
```

```
```
def remove(n:Int):A = {
  if(n>=length) throw new IllegalArgumentException("Remove index "+n+
  " of "+length)
  var i = 0
  var pos = lhead
  var last,next = -1L
  while(i<=n) {
    raf.seek(pos)
    if(i==n) {
      next = raf.readLong()
    } else {
      last = pos
      pos = raf.readLong()
    }
    i += 1
  }
  val ret = reader(raf)
  if(last == -1L) {
    lhead = next
  } else {
    raf.seek(last)
    raf.writeLong(next)
  }
  if(pos == ltail) {
    ltail = last
  }
  length -= 1
  ret
}
```
```

```
```
def update(n:Int, elem:A) {
  if(n>=length) throw new IllegalArgumentException("Updating index "+n+
  " of "+length)
  var i = 0
  var pos = lhead
  while(i<=n) {
    raf.seek(pos)
    pos = raf.readLong()
    i += 1
  }
  writer(raf,elem)
}
```

```
def close() = raf.close()
}
```

阅读这段代码，你会注意到有很多地方先调用了 **seek**，然后是 **readLong** 或 **writeLong**。这是因为每个节点的前八个字节用于存储下一个值的位置。

与普通的链表一样，这段代码有很多 **while** 循环遍历列表进行计数。它还有处理头部和尾部引用的边界情况的开销。这些特殊情况，再加上文件访问更加冗长

![](img/157fcf510c119278e4b1267c62717fa8_855_0.png)

![](img/157fcf510c119278e4b1267c62717fa8_855_1.png)

# FIGURE 33.3: Part A on the top shows the tree from figure 33.2 with the addition of a record whose key value is 75.

上图 Part A 显示了图 33.2 中的树，并添加了一个键值为 75 的记录。

Part A on the top shows the tree from figure 33.2 with the addition of a record whose key value is 75. The 75 is simply placed in sorted order in a leaf because there is still space left in that node. For part B of this figure, a record with a key value of 82 has been added. It would go right after the 75 record, but there is no more space in that node. Of the five records that would be in the node, the 75 is the median so it is moved into the parent and the other records are split into two different nodes. This process can propagate to higher levels in the tree if the parent is also full. A new level is created when the root node fills and has to split.

只要该叶子仍有空位，该新记录就会按正确位置插入，添加操作就完成了。这在图 33.3-A 中有所说明。如果新记录所属的叶节点已满，则需要创建一个新节点。这是通过将该节点拆分为两个，将中值记录推入父节点，并在两侧放置指向两个子节点的链接来实现的。这在图 33.3-B 中显示。
实际的 B 树在每个节点中通常包含的记录数远多于这些图中所示的记录数。它们的平均分裂因子非常高，这意味着它们可以用很少的层级容纳极大量的记录。来看一个例子，假设一个 B 树每个节点有 200 条记录，且大致半满。这意味着每个节点大约有 100 条记录，每个内部节点大约有 100 个子节点。² 所以顶层将容纳 100 条记录。下一层将容纳 10,000 条。下一层将容纳 1,000,000 条。这仍然是 O(log(n)) 的行为，但从技术上讲是 O(log₁₀₀(n))，增长非常缓慢。一个包含十亿条记录的树仅会勉强超过五层。这很重要，因为在查找记录时，每一层最终都会变成一次查找和一次读取。

## 33.3 End of Chapter Material

### 33.3.1 Summary of Concepts

- 直接访问，或随机访问文件允许你从一个位置跳转到另一个位置，进行读写。
- 这种功能使它们可以用作类似数组的数据结构，具有极大的容量。
- 处理所有记录长度相同的文件最容易，因为这样我们可以轻松计算出文件中的任何给定记录的位置。
- 也可以使用可变记录长度，但需要更多的簿记。通常这是通过使用固定记录长度的索引来告诉我们数据文件中元素的位置来实现的。
- 我们可以使用文件位置来模拟引用，从而在文件中创建链接数据结构。
  - 在文件中放置头信息使我们能够跟踪诸如列表的头或尾，或树的根等内容。
  - 可以为每条记录存储额外信息以包含对数据结构中其他节点的引用。
  - 虽然我们可以在直接访问文件中编码链表，但它非常低效，因为它需要大量的磁盘访问。
  - 存在其他链接结构专门用于解决访问速度慢的问题。B 树就是一个例子。

### 33.3.2 Exercises

- 1. 编写代码来比较不同文件支持的序列（类似数组和类似链表）之间的速度，并将其与内存支持的序列进行比较。
- 2. 为 VariableRecordSeq 编写一个紧凑方法。此方法应被调用以消除数据文件中的空白空间。它通过创建新的数据文件并一次移动一条记录从旧文件到新文件，同时相应地更新索引的新位置来实现。一旦完成，旧数据文件可以被删除，新文件的名称可以更改为与原始名称匹配。
- 3. 对 FixedRecordList 进行适当的更改以制作 VariableRecordList。
- 4. 为链表编写一个 linearize 方法，该方法将创建一个所有节点已重新排序为列表中出现顺序并且所有空闲节点已被移除的新文件。
- 5. 编写一个仅在内存中工作的 B 树。
- 6. 将上一练习中的 B 树转换为使用磁盘访问。

每个参与者都可以独立工作，与其他参与者无关，并执行可能只有它才做的专业任务。

参与者的行为由其他参与者发送的消息驱动。在装配线类比中，一条消息可以是移动到下一个站点的托盘中的物体，或是提供信息的喊声。不管怎样，消息只是从一个参与者传递信息到另一个参与者。如果该信息以物理对象的形式出现，传递它的参与者在传递后就不再与该物理对象交互。

actor 模型在线程中工作的方式以及它如何防止标准问题如竞态条件，取决于当某物通过消息传递时，发送方停止更改它的条件。你可以想象每个参与者都有自己的线程。¹ 每个参与者还可以拥有它私下保留的可变数据。这就是 actor 模型与纯函数式方法不同的地方。允许可变性，但它需要一次内部于一个参与者。参与者接收消息以执行操作，而不是在它们上面调用方法。区别很微妙，但很重要。方法调用将线程的控制权从一个对象传递到另一个对象。从一个参与者发送到另一个参与者的消息不会赋予接收参与者对发送者线程的控制权。它只是被发送的信息，而不是线程控制。这防止了竞态条件和死锁，因为可变数据被本地化到单个参与者/线程。

使用 actors 的一大优势，以及它们通常比使用线程级控制更容易且不易出错的原因是，你可以在更高层次上思考你的问题。不是思考线程和同步，你将问题视为拥有不同的参与者，每个参与者大多独立工作并相互通信。每个参与者可以有状态并改变该状态。它们的行为取决于它们所处的状态。事实上，当你处理基于 actor 的程序时，你可能不应该花太多时间思考 actors 可以并行执行操作这一事实。那部分会自动出现，并且在合适时会使用多个线程。

actor 并行模型并不独特于 Scala。Erlang 编程语言可能是与 actors 最常关联的语言。Erlang 是一种函数式语言，几乎所有事情都通过 actors 完成。Scala 库甚至借用了 Erlang 语法，因此在 Scala 中向 actors 发送消息看起来与在 Erlang 中相同。

## 34.2 scala.actors Package

Scala 的标准 actor 实现位于 scala.actors 包中。该包在第 21 章中简要提到，作为使用 Futures.future 或 Actor.actor 分别有无返回值地生成线程的简单方法。虽然使用 Actor.actor 技术上创建了一个 actor，但它的功能非常有限，因为主体不在 Actor 类的子类型的新的类范围内。要创建完全功能的 actors，我们需要创建一个扩展 Actor 的新类。

Actor 类型有一个抽象方法，必须由所有具体实现。

> ¹ 正如我们稍后在本章中将看到的，你通常不希望这种极端观点成为现实，因为可能有数百万个 actors，而你实际上并不想拥有数百万个线程。尽管如此，作为程序员不会手动控制线程，唯一安全的假设是每个 actor 都可能在单独的线程上运行。

