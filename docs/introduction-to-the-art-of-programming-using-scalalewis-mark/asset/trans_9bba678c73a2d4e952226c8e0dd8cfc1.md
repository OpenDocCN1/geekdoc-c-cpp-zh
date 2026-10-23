
为了更具体地说明，想象你站在一个四岔路口。你向预言机询问每个方向，得到的值分别为 7、13、4 和 19。因此最短路径位于返回 4 的那个方向。然而，那是从该方向走一步后的距离。你所在位置的最小距离比那个值大 1，也就是 5 步。它是四个值中的最小值，再加上一步才能到达那个位置。取最小值的这个解法也为我们处理撞墙或走出边界的基本情况指明了正确方向。如果最佳解是最小值，那么对于一条糟糕的路径，我们应该返回一个不可能成为最小值的数。像十亿这样的大数对于几乎任何迷宫来说都足够了。你可能会想用 Int.MaxValue，但请记住我们还要给它加 1。在 REPL 中试试 Int.MaxValue+1，你就会明白为什么这不是一个理想的选择。

这就定义了我们的递归情形。还需要考虑另一个因素。如果你曾置身于树篱迷宫或其他无法越过墙壁看到远处的迷宫中，你会发现很难区分各个位置，除非你采取措施标记之前到过的地方，否则可能会绕圈子，永远找不到出口。格林兄弟在《汉塞尔与格莱特》中描述了一个相当著名的解决方案，他们留下面包屑来标记路径。我们也会采用同样的方法。假设你的电脑里没有鸟，这对你来说应该比那对兄妹更有效。如果你的电脑里确实有鸟，你可能应该在继续阅读之前先处理一下这个问题。

因此，我们的算法所需的最后一个方面是能够放下面包屑来标记路径。如果我们再次遇到自己的面包屑，就把它当作撞墙或越界一样处理。在从一条路径返回之前，我们还会清扫掉面包屑。汉塞尔和格莱特并不需要这样做，他们只是想找到自己的路。然而，我们希望找到最优路径，而到处留下面包屑常常会导致我们错过这样的路径。将所有这些转换为代码，结果如下。

```scala
def shortestPath(maze:Array[Array[Int]],x:Int,y:Int,endX:Int,endY:Int):Int = {
  if(x<0 || y<0 || y>=maze.length || x>=maze(y).length || maze(y)(x)!=0) {
    1000000000
  } else if (x==endX && y==endY) {
    0
  } else {
    maze(y)(x)=1
    val dist=(shortestPath(maze,x+1,y,endX,endY) min
      shortestPath(maze,x-1,y,endX,endY) min
      shortestPath(maze,x,y+1,endX,endY) min
      shortestPath(maze,x,y-1,endX,endY)) + 1
    maze(y)(x)=0
    dist
  }
}
```

整个函数由 if 表达式构成。第一个分支用于处理越界、撞墙或遇到我们留下的面包屑，并返回十亿。这个数大到不可能是有效路径，但又足够小，即使在迷宫中为其他步骤加 1 也不会溢出。第二个分支是到达终点的情况。这两个分支可以互换，如果出口位于边界之外或在数组中以特殊值标记，那就需要交换。最后一个分支是递归情形，它会丢下面面包屑，进行四次递归调用，用 min 组合它们，然后拾起面包屑并返回。可以使用以下调用来调用这段代码。

```scala
println(shortestPath(maze,0,0,9,9))
```

对于上面显示的迷宫，这次调用的返回值是 36。对于这个特定的迷宫，这是从 (0,0) 到 (9,9) 的唯一路径的长度。你应该多玩玩这个迷宫，以确保该函数能为其他配置找到最短路径。

这个函数实际上测试了迷宫中的每一条路径，并返回最短的一条。这种方法有优点也有缺点。缺点是，如果路径很多，可能会花一些时间。我们将在第 28 章进一步探讨并考虑解决方法。优点是，只需对这段代码做很小的修改，就能产生其他类似的函数，例如寻找最长路径或统计路径数量的函数。这些特定问题留给学生作为练习，但现在我们要告诉你，真正需要修改的只是基本情况的返回值以及递归调用的组合方式。

## 15.6 排序

在第 13 章中，我们使用循环来实现所有迭代。我们本可以使用递归。实际上，有些排序用递归来表达非常优雅。考虑一个 maxSort。两个循环可以写成两个递归函数，其中一个可以嵌套在另一个内部。内层函数在某个位置之前查找最大值的索引。它嵌套在一个函数中，该函数从后向前遍历数组，找到最大值并将其交换到正确位置，然后再向前移动一个位置。实现这一点的代码如下。

```scala
def maxSort(a:Array[Double],end:Int) {
  def maxIndex(end2:Int):Int =
    if(end2==0) 0 else {
      val m=maxIndex(end2-1)
      if(a(m) > a(end2)) m else end2
    }

  if(end>0) {
    val index=maxIndex(end)
    if(index!=end) {
      val tmp=a(index)
      a(index)=a(end)
      a(end)=tmp
    }
    maxSort(a,end-1)
  }
}
```

这比使用循环的版本稍长一些，但也没长太多。如果我们希望有一个只需单个参数即可调用的版本，就需要一个包装函数。

也许一个更好的例子是插入排序。插入排序的内层循环在执行插入操作，因此我们编写一个递归的 insert 函数。它被一个执行排序的外层函数调用，该函数简单地遍历数组，将每个元素放到正确位置。

```scala
def insertionSort(a:Array[Double],i:Int=1) {
  def insert(v:Double,i:Int) {
```

一个接收 List[Int] 并返回 List[Int] 的函数。1 它使用递归的 merge 函数来将列表合并到一起。

```scala
def merge(lst1: List[Int], lst2: List[Int]): List[Int] = (lst1, lst2) match {
    case (Nil, _) => lst2
    case (_, Nil) => lst1
    case (h1 :: t1, h2 :: t2) =>
        if (h1 < h2) h1 :: merge(t1, lst2)
        else h2 :: merge(lst1, t2)
}
```

```scala
def mergeSort(lst: List[Int]): List[Int] = lst match {
    case Nil => lst
    case h :: Nil => lst
    case _ =>
        val (l1, l2) = lst.splitAt(lst.length / 2)
        merge(mergeSort(l1), mergeSort(l2))
}
```

这两个函数都使用模式匹配来处理递归中的不同情况。这使它们简洁、易读。遗憾的是，递归版本的 merge 必须为每个被合并的元素分配一个新的栈帧。这意味着这个版本的代码无法扩展到大规模。

为了克服这个限制，我们需要使用一个更命令式的、基于 while 循环的 merge，这样的版本可能如下所示。

```scala
def merge(lst1: List[Int], lst2: List[Int]): List[Int] = {
    var l1 = lst1
    var l2 = lst2
    var ret = List[Int]()
    while (l1.nonEmpty && l2.nonEmpty) {
        if (l1.head < l2.head) {
            ret ::= l1.head
            l1 = l1.tail
        } else {
            ret ::= l2.head
            l2 = l2.tail
        }
    }
    if (l1.nonEmpty) ret ::= l1.reverse
    else ret ::= l2.reverse
    ret.reverse
}
```

这个版本没那么优雅，而且长度大约是原来的两倍。然而，它能处理明显更长的列表，因此实用性强得多。

关于归并排序，最后需要注意的一点是它的工作方式。当递归调用沿栈向下时，几乎没有什么操作。输入的 List 被分成两半，这两半被传递下去。这个过程不断重复，直到到达单个元素。真正的工作发生在递归沿栈向上返回时。在函数返回之前，它会调用 merge，而 merge 才做真正的工作。所以，如果你在脑海中想象类似图 15.1 的画面，

> 1 与使用数组的版本不同，使用 List 的排序必须返回一个新的 List，因为原始 List 无法被修改。

