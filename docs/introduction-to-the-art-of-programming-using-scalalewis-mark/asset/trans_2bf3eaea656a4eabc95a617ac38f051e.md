

在 GUI 的顶部放置它并让它更新 vars 映射中与名称 "t" 关联的值，以便在公式中使用。

// Add this.
@transient private var tTimeSlider:Slider = null

...

// Add this.
private def timeSlider = {
  if(tTimeSlider==null) {
    tTimeSlider = new Slider {
      min = 0
      max = 800
      listenTo(this)
      reactions += {
        case vc:ValueChanged =>
          vars("t") = value
          drawPanel.repaint()
      }
    }
    if(!vars.contains("t")) vars("t") = 0
    tTimeSlider.value = vars("t").toInt
  }
  tTimeSlider
}

...

// Change to this.
},new SplitPane(Orientation.Horizontal,
  new BorderPanel {
    layout += new ScrollPane(drawPanel) -> Center
    layout += timeSlider -> North
  },
  commandPanel))

vars 映射是在我们向命令添加逆波兰表示法 RPN 计算器时引入的。它可以在这里与 Formula 类型一起再次使用。这不仅仅是复用，它增加了能力。现在命令可以用来设置在公式中引用的变量。我们现在需要做的只是让我们绘制的东西也使用公式。

这也不难做到。例如，DrawRectangle 类型的宽度和高度可以更改为使用公式，改动如下。

```
class DrawRectangle(p:DrawTransform,
  private var width:Formula = new Formula("100.0"),
  private var height:Formula = new Formula("100.0"),
  private var color:Color = Color.black) extends DrawLeaf {
```

...

```
def draw(g:Graphics2D) {
  g.setPaint(color)
```

你会输入到 RPN 计算器中的内容，并且不需要括号来指定运算顺序。虽然你可能不会通常认为方程是树，但事实证明这种形式非常好地包含了它们的含义，并且可以很容易地转换为表达式的不同有用版本。

## 29.3 二叉搜索树：作为映射的二叉树

上面的例子是树的一个有趣用法，也是树强大功能的一个有趣说明。然而，这些结构最主要的使用是存储数据。在本节中，我们将探讨二叉搜索树 BST 的细节，作为实现 Map ADT 的一种手段。

map ADT 的性质在第 20 章中描述过，当时我们查看了 Scala 集合库中内置的那些。二叉搜索树首先是一个二叉树。这是一种允许每个节点有 0、1 或 2 个子节点的树。在 BST 的情况下，子节点通常称为左和右，并且可能有右子节点而没有左子节点。存储在节点中的数据至少一部分包括一个具有完全顺序的键。这意味着对于任意两个键值，你可以询问其中一个是否小于、等于或大于另一个。BST 的主要标准是左边的后代具有较小的键值，而右边的后代具有更大的键值。

二叉搜索树的名称应该让人联想到第 13 章中讨论的二分搜索。这并非偶然。平衡良好的 BST 在用户查找元素时，其行为会非常类似于二分搜索。为了理解这一点，我们将考虑一个例子。图 29.5 显示了一个使用基本整数作为键以保持简单性的 BST 示例。该树以正确的 BST 组织方式包含值 0 - 9。¹ 粗体箭头指示搜索值 2 时所走的路径。

向基本 BST 添加新元素相当直接。如果树为空，没有根，那么我们创建一个包含当前元素的节点并使其成为根。对于任何其他情况，我们从根开始，以与搜索相同的方式向下走，当新值小于节点中存储的值时向左走，当它更大时向右走。最终，这个过程会到达没有子节点在指示方向上的点。创建一个新节点来存储新值并将其放置在树中的该位置。图 29.6 按 5、3、1、8、7、4、2、9、0、6 的顺序逐步完成此过程。结果是图 29.5 中显示的树。请注意，添加数字的顺序很重要。虽然某些其他顺序会产生相同的树，但大多数不会。

从 BST 中删除的过程比添加要复杂一些。考虑我们想要从示例树中删除值为 5 的节点的情况。这恰好是根节点。我们不能简单地将其拿走，因为那样会使我们剩下两棵独立的树。我们必须做一些修改树的方式，使结果仍然是一个有效的 BST。一个方法是把右子树放在左子树的底部右侧，反之亦然。在这种情况下，这会把 8 放在 4 的右侧或把 3 放在 7 的左侧。虽然这些在技术上可行，但远非理想，因为它们倾向于使树失衡。我们很快就会看到这会产生很大的差异。

另一种方法是移动来自一个更低的节点的数据，该节点更容易删除，然后将其提升以替换 5，然后删除该下层节点。如果节点有零个或一个子节点，则很容易删除。当然，被移动的数据必须能够取代被删除的节点的位置而不破坏树的正确顺序。只有两个节点可以做到这一点，左边的最大元素或右边的最小元素。在这种情况下，它们是值 4 和 6。如果 5 被其中任何一个替换，其余的树结构保持完全完整并保留正确的顺序。虽然这个过程描述起来相当容易，但不幸的是它有许多特殊情况需要处理。

以下是使用 BST 实现 Scala 库中可变映射的代码。此代码对键和值类型都有类型参数，在此代码中称为 K 和 V。TreeMap 必须在构造时传递一个比较函数。这提供了键所需的完全顺序。可变 Map 类型有四个必须实现的抽象方法，+=、-=、get 和 iterator。完整的实现如下所示。

```
package scalabook.adt

import collection.mutable
import annotation._

class TreeMap[K,V](comp:(K,K)=>Int) extends mutable.Map[K,V] {
  private class Node(var key:K, var data:V) {
    var left:Node = null
    var right:Node = null
  }

  private var root:Node = null

  def +=(kv:(K,V)) = {
```

```
```
}
}

root = findVictim(root)
this
}

def get(key:K):Option[V] = {
var rover = root
var c = comp(key,rover.key)
while(rover!=null && c!=0) {
rover = if(c<0) rover.left else rover.right
if(rover!=null) c = comp(key,rover.key)
}
if(rover==null) None else Some(rover.data)
}

def iterator = new Iterator[(K,V)] {
val stack = new ListStack[Node]
pushRunLeft(root)
def hasNext:Boolean = !stack.isEmpty
def next:(K,V) = {
val n = stack.pop()
pushRunLeft(n.right)
n.key -> n.data
}
@tailrec def pushRunLeft(n:Node) {
if(n!=null) {
stack.push(n)
pushRunLeft(n.left)
}
}
}
}

object TreeMap {
def apply[K,V](data:(K,V)*)(comp:(K,K)=>Int):TreeMap[K,V] = {
val tm = new TreeMap[K,V](comp)
val d = data.sortWith((a,b) => comp(a._1,b._1)<0).toIndexedSeq
def binaryAdd(start:Int,end:Int) {
if(start<end) {
val mid = (start+end)/2
tm += d(mid)
binaryAdd(start,mid)
binaryAdd(mid+1,end)
}
}
binaryAdd(0,data.length)
tm
}
}
```

这段代码中最简单的方法是 **get** 方法。它创建一个 **rover** 和一个存储比较结果的变量，然后有一个 **while** 循环，直到找到正确的键或 rover 从树的底部掉落。变量 **c** 用于存储比较结果

![](img/157fcf510c119278e4b1267c62717fa8_781_0.png)

图 29.5：这是一个使用整数值键的二叉搜索树示例。在树中搜索元素所遵循的步骤与二分搜索执行的步骤非常相似。粗体箭头显示了搜索值 2 时会走的路径。

