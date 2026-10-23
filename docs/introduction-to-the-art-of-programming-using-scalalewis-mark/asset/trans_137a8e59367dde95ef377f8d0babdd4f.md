

```scala
</drawGraph>
}

def react(evt:Event,cx:Double,cy:Double) {
  evt match {
    case me:MouseEvent =>
      hoverNode = null
      hoverEdge = null
      var lastDist = 1e100
      for(n <- nodes) {
        val dx = cx-n.x
        val dy = cy-n.y
        val dist = math.sqrt(dx*dx+dy*dy)
        if(dist<10 && dist<lastDist) {
          hoverNode = n
          lastDist = dist
        }
      }
      if(lastDist>3) for(e <- n.edges; 
          if(nodes.indexOf(e.from)<nodes.indexOf(e.to))) {
        val line = new Line2D.Double(e.from.x,e.from.y,e.to.x,e.to.y)
        val edist = line.ptSegDist(me.point).abs
        if(edist<3 && edist<lastDist) {
          hoverEdge = e
        }
      }
      if(hoverNode!=null) hoverEdge = null
      if(clickAction!=null) clickAction(me,cx,cy)
      drawing.refresh
    case _ =>
  }
}

private def canReach(n:Node,visited:mutable.Set[Node]):Boolean = {
  if(n==endNode) true
  else if(visited(n)) false
  else {
    visited += n
    n.edges.exists(e => canReach(e.to,visited))
  }
}

private def shortestPath(n:Node,visited:Set[Node]):Option[(Int,Set[Node])] = {
  if(n==endNode) Some(0 -> visited)
  else if(visited(n)) None
  else {
    val newVisited = visited+n
    n.edges.foldLeft(None:Option[(Int,Set[Node])])((last,e) => {
      (last,shortestPath(e.to,newVisited)) match {
        case (None,Some((len,v))) => Some(len+e.weight,v)
        case (_,None) => last
        case (Some((len1,_)), Some((len2,v))) => if(len1<len2+e.weight) last
                                                    else Some(len2+e.weight,v)
      }
    })
  }
}
```

```
}
}
}

object DrawGraph {
    def apply(p:DrawTransform) = new DrawGraph(p,List(new Point2D.Double(100,100)),List(),-1)

    def apply(p:DrawTransform,n:xml.Node) = {
        val end = (n \ "@en").text.toInt
        val pnts = (n \ "node").map(pn => {
            val x = (pn \ "@x").text.toDouble
            val y = (pn \ "@y").text.toDouble
            new Point2D.Double(x,y)
        })
        val edges = (n \ "edge").map(en => {
            val from = (en \ "@from").text.toInt
            val to = (en \ "@to").text.toInt
            val weight = (en \ "@weight").text.toInt
            (from,to,weight)
        })
        new DrawGraph(p,pnts,edges,end)
    }

    private class Node(var x:Double,var y:Double) extends Serializable {
        var edges = List[Edge]()
    }

    private class Edge(val from:Node,val to:Node,val weight:Int) extends Serializable {
        def sameAs(e:Edge):Boolean = {
            weight==e.weight && ((from==e.from && to==e.to) || (from==e.to && to==e.from))
        }
    }
}
```

一般来说，图中的边可以是有向的，即只能从一个节点到另一个节点，而不能反过来。示例中存储节点的方式保留了这种灵活性，但代码维护的是双向连接，因此用户界面不必能够区分同一对节点之间的两条连接。

由于这段代码与 `DrawMaze` 类型的相似性，你应该可以比较轻松地读懂其中大部分内容。你应该将它放入自己的项目，向 `Drawing` 和 `DrawTransform` 添加适当代码以支持新增该类型并从 XML 加载它，然后使用它一段时间。这里我们想重点关注的是两个递归遍历图的方法，因为项目中的一些可选任务包括向你的代码添加类似功能。

第一个方法只是检查能否从你点击的节点到达终点节点。该方法使用一个可变集合来记录已经访问过的节点。这个集合在这个算法中扮演了“面包屑”的角色。使用 `Set` 类型是出于效率考虑。让集合是可变的，得到的算法行为就像不再捡回面包屑一样。在这里这样做是可以的，因为我们只想知道某个节点是否可达，完全不关心经过的路径。

```scala
private def canReach(n:Node,visited:mutable.Set[Node]):Boolean = {
    if(n==endNode) true
    else if(visited(n)) false
    else {
        visited += n
        n.edges.exists(e => canReach(e.to,visited))
    }
}
```

基准情况包括到达终点节点和遇到已访问过的节点。每访问一个节点，就把该节点加入集合。递归发生在对当前节点所有出边调用 `exists` 的过程中。`exists` 方法很适合我们，因为只要运行到任意一个返回 `true` 的元素，它就会停止执行。因此，如果从某个节点出发的第一条边就能到达终点，其他边就不需要被遍历了。

第二个方法是另一个最短路径算法，但这次是在带权图上，而不是在迷宫中。这里同样传入一个集合，用来记录已访问的元素。在这种情况下，集合是不可变的，因为路径很重要，我们需要把面包屑收回来。这个方法的返回类型也明显更复杂，是 `Option[(Int,Set[Node])]`。`Option` 部分表示可能没有解；例如，如果从选定的起始节点无法到达终点，就会出现这种情况。这种写法通常比用 `null` 表示“没有任何结果”更受青睐。其中的 `Int` 是路径长度，`Set[Node]` 是在找到的路径上访问过的所有节点。严格来说，这并不等同于返回一条路径，但它提供了足够的信息，让用户在大多数情况下都能很容易地推断出所走的路径。而且这种方法也很容易实现，因为我们本来就在用不可变集合跟踪已访问节点。

```scala
private def shortestPath(n:Node,visited:Set[Node]):Option[(Int,Set[Node])] = {
    if(n==endNode) Some(0 -> visited)
    else if(visited(n)) None
    else {
        val newVisited = visited+n
        n.edges.foldLeft(None:Option[(Int,Set[Node])])((last,e) => {
            (last,shortestPath(e.to,newVisited)) match {
                case (None,Some((len,v))) => Some((len+e.weight,v))
                case (_,None) => last
                case (Some((len1,_)), Some((len2,v))) => if(len1<=len2+e.weight) last
                    else Some(len2+e.weight,v)
            }
        })
    }
}
```

这里的基准情况与上面检查可达性的方法相同，只是返回值略有不同。递归分支的代码也要长一些，以处理各种不同情况。它使用 `fold` 来汇总答案，遍历当前节点的不同出边。`fold` 以一个指定了合适类型的 `None` 值开始。`fold` 中的函数对传入的值和当前边的递归调用结果进行匹配。当其中一个是 `None` 时，就使用另一个值。如果两个值都是 `Some`，则用模式匹配取出长度，以便返回较短的一个。这里的匹配模式展示了 `_` 的用法：只为必要的最少值命名。

这种针对图的最短路径解法，与最初的迷宫解法如出一辙。

## 28.4 分治法

使用递归的一种标准问题求解技术是分治法。其思想是：取一个大问题，把它分成两个或更多较小的部分，解决这些部分，然后组合结果，得到完整解决方案。这与我们在第 5 章首次讨论的问题分解思想类似。解决难题的标准方法是将其分解成更容易的问题。这是编程的一个基本方面，因为程序可能任意复杂。程序也可以用类似的方法来解决问题。

分治法是递归的，因为解决整个问题的函数也被用来解决各个部分。基准情况就是当你把问题缩小到无需再分解就能解决的程度。这通常会让你一直缩小到问题变得微不足道为止。由于每次递归调用处理的问题都比原来的问题更小，递归会不断把你推向基准情况。我们将通过几个不同的分治算法示例来了解这种方法如何运作。

我们将首先考虑的分治算法示例是第 15 章中简要介绍过的排序算法：归并排序和快速排序。这两种排序的做法都是取一个数字序列，将其分成两个部分，再递归处理。默认的基准情况是单个元素，因为只有一个元素的数组总是已经正确排序的。不过，在元素数量较大的某个阈值处停止递归，转而使用我们之前探索过的某种排序来完成较小分段的排序，可能会更高效。

### 28.4.1 归并排序

归并排序的工作原理是：将数组递归地分成两个相等的部分⁴，然后递归调用自身处理这两个部分。归并排序中真正的工作发生在代码从调用栈中返回、已排序的子段合并在一起的过程中。归并排序的一个关键优势是它的工作量非常稳定。它总是从中间对半划分，因此递归深度始终为 log₂(n) 层。对两个各含 n/2 个元素的列表进行合并，需要 n − 1 次比较和 n 次内存移动。因此，无论输入形式如何，归并排序的复杂度总是 O(n log₂(n))。

归并排序的主要缺点是它无法原地完成。这是因为，如果不用额外空间，就无法将已经分别排序的两个数组半段合并成一个有序数组。这使得归并排序很适合列表：列表容易合并，但列表不可变，因此原地操作的概念对列表没有意义。要编写一个适用于数组且内存消耗不超过 O(n) 的归并排序，会稍微棘手一些。

我们先从最简单的归并排序形式开始。这是一种对 `List` 排序的实现，使用递归合并。该函数的代码如下所示。

