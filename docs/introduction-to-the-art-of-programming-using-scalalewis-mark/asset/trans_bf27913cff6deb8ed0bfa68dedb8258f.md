

![](img/157fcf510c119278e4b1267c62717fa8_880_0.png)

![](img/157fcf510c119278e4b1267c62717fa8_880_1.png)

FIGURE 35.1: 该图显示了向左和向右的单次旋转。当节点的外部孙节点左侧或右侧长得过高导致节点失衡时，可以使用这些旋转。

在内部孙节点，即左孩子的右孩子或右孩子的左孩子，长大导致树失衡的情况下，需要进行两次旋转。第一次旋转应用于高度更大的孩子，使其向外移动。第二次旋转然后将父节点移动到相反的一侧。图 35.2 显示了其工作原理。请注意，这些双重旋转中的每一步都是图 35.1 中所示的单次旋转之一。这在代码中也很重要，因为在实现单次旋转后，使用它们构建双重旋转是一个简单的任务。

## 35.2.2 Implementation

要实现 AVL 树，我们将使用第 29 章中编写的不可变 BST 作为基础并对其进行适当的编辑。使 AVL 树可变留给读者作为练习。与该树一样，我们有一个代表树的公共类型，没有任何功能。我们还有两个私有类来实现该公共类型。顶层类型在功能上增加了 rotate 和 height，以及用于调试目的的 verifyBalance。rotate 方法 supposed to 检查平衡并在需要时执行适当的旋转。height 成员存储节点的高度。它是一个抽象 val，因此子类型必须提供一个值。这里显示了该代码。

```
package scalabook.adts

abstract sealed class ImmutableAVLTreeMap[K <% Ordered[K], +V] extends Map[K,V] {
  def +[B >: V](kv:(K,B)):ImmutableAVLTreeMap[K,B]
  def -(k:K):ImmutableAVLTreeMap[K,V]
  def rotate:ImmutableAVLTreeMap[K,V]
  val height:Int
  def verifyBalance:Boolean
```

![](img/157fcf510c119278e4b1267c62717fa8_881_0.png)

FIGURE 35.2: 该图显示了向左-右和向右-左的双重旋转。当节点的内部孙节点左侧或右侧长得过高导致节点失衡时，可以使用这些旋转。请注意，每一个都只是图 35.1 中旋转的两次应用。

```
}
```

```
private final class AVLNode[K <% Ordered[K],+V](private val key:K,
    private val data:V, private val left:ImmutableAVLTreeMap[K,V],
    private val right:ImmutableAVLTreeMap[K,V]) extends ImmutableAVLTreeMap[K,V] {

val height = (left.height max right.height)+1

def +[B >: V](kv:(K,B)) = {
    val ret = if(kv._1 == key) new AVLNode(kv._1, kv._2, left,right)
    else if(kv._1 < key) new AVLNode(key, data, left+kv, right)
    else new AVLNode(key, data, left, right+kv)
    ret.rotate
}

def -(k:K) = {
    val ret = if(k == key) {
        left match {
            case _:AVLEmpty[K] => right
            case i:AVLNode[K,V] => {
                right match {
                    case _:AVLEmpty[K] => left
                    case _ => {
                        val (k, d, newLeft) = i.removeMax
                        new AVLNode(k, d, newLeft, right)
                    }
                }
            }
        }
    }
```

```
}
}
} else if(k < key) {
    new AVLNode(key, data, left-k, right)
} else {
    new AVLNode(key, data, left, right-k)
}
ret.rotate
}

def get(k:K):Option[V] = {
    if(k==key) Some(data)
    else if(k<key) left.get(k)
    else right.get(k)
}

def iterator = new Iterator[(K,V)] {
    val stack = new ListStack[AVLNode[K,V]]
    pushRunLeft(AVLNode.this)
    def hasNext:Boolean = !stack.isEmpty
    def next:(K,V) = {
        val n = stack.pop()
        pushRunLeft(n.right)
        n.key -> n.data
    }
    def pushRunLeft(n:ImmutableAVLTreeMap[K,V]) {
        n match {
            case e:AVLEmpty[K] =>
            case i:AVLNode[K,V] =>
                stack.push(i)
                pushRunLeft(i.left)
        }
    }
}

def rotate:ImmutableAVLTreeMap[K,V] = {
    if(left.height>right.height+1) {
        left match {
            case lNode:AVLNode[K,V] => // Always works because of height.
                if(lNode.left.height>lNode.right.height) {
                    rotateRight
                } else {
                    new AVLNode(key,data,lNode.rotateLeft,right).rotateRight
                }
            case _ => null // Can't happen.
        }
    } else if(right.height>left.height+1) {
        right match {
            case rNode:AVLNode[K,V] => // Always works because of height.
                if(rNode.right.height>rNode.left.height) {
                    rotateLeft
                } else {
                    new AVLNode(key,data,left,rNode.rotateRight).rotateLeft
                }
            case _ => null // Can't happen.

```

```
}
} else this
}

def verifyBalance:Boolean = {
  left.verifyBalance && right.verifyBalance && (left.height-right.height).abs<2
}

private def removeMax:(K,V,ImmutableAVLTreeMap[K,V]) = {
  right match {
    case e:AVLEmpty[K] => (key, data, left)
    case i:AVLNode[K,V] =>
      val (k, d, r) = i.removeMax
      (k, d, new AVLNode(key,data,left,r).rotate)
  }
}

private def rotateLeft:AVLNode[K,V] = right match {
  case rNode:AVLNode[K,V] =>
    new AVLNode(rNode.key,rNode.data,new
      AVLNode(key,data,left,rNode.left),rNode.right)
  case _ => throw new IllegalArgumentException("Rotate left called on node with empty right.")
}

private def rotateRight:AVLNode[K,V] = left match {
  case lNode:AVLNode[K,V] =>
    new AVLNode(lNode.key,lNode.data,lNode.left,new
      AVLNode(key,data,lNode.right,right))
  case _ => throw new IllegalArgumentException("Rotate right called on node with empty left.")
}
}
```

```
private final class AVLEmpty[K <% Ordered[K]] extends
  ImmutableAVLTreeMap[K,Nothing] {
  def +[B](kv:(K,B)) = {
    new AVLNode(kv._1, kv._2, this, this)
  }

  def -(k:K) = {
    this
  }

  def get(k:K):Option[Nothing] = {
    None
  }

  def iterator = new Iterator[(K,Nothing)] {
    def hasNext = false
    def next = null
  }

  def rotate:ImmutableAVLTreeMap[K,Nothing] = this
```

```
def verifyBalance:Boolean = true

val height:Int = 0
}
```

```
object ImmutableAVLTreeMap {
    def apply[K <%
        Ordered[K],V](data:(K,V)*)(comp:(K,K)=>Int):ImmutableAVLTreeMap[K,V] = {
        val empty = new AVLEmpty[K]()
        val d = data.sortWith((a,b) => comp(a._1,b._1)<0)
        def binaryAdd(start:Int,end:Int):ImmutableAVLTreeMap[K,V] = {
            if(start<end) {
                val mid = (start+end)/2
                new AVLNode(d(mid)._1,d(mid)._2,binaryAdd(start,mid),binaryAdd(mid+1,end))
            } else empty
        }
        binaryAdd(0,data.length)
    }
}
```

对 AVLEmpty 类型的添加很简单。height 始终为 0，rotate 返回 this 因为它总是平衡的，并且 verifyBalance 方法始终返回 true。

内部节点类型稍微复杂一些。height 被设置为明显的 (left.height max right.height)+1 的值。verifyBalance 方法检查子节点的高度并递归地在这些子节点上调用自身。更改的核心在于 rotate 方法。该方法检查子节点的高度，如果它们不平衡，则执行一次或两次旋转以返回具有平衡子树的节点。旋转本身在名为 rotateLeft 和 rotateRight 的私有方法中实现。

在不同的 rotate 方法中进行了多次匹配。这是因为它们必须获取左右孙节点。这需要匹配，因为顶层类型没有 left 和 right。这是有意义的，因为它们未定义在 AVLEmpty 上。代码的编写方式，不应可能将这些方法与 AVLEmpty 节点一起调用。旋转方法编写为在发生这种情况时抛出异常。

唯一的其他更改是在 + 和 - 方法中添加了对 rotate 的调用。这些调用在向上弹出堆栈时发生，因此每次都会重新平衡整个树。对该类的测试从原始 BST 的测试代码开始。为了确保其正常工作，必须使用 + 构建树然后使用 verifyBalance 检查。伴生对象中实现的快捷方式方法始终生成完美平衡的树，因此使用它实际上并不会测试旋转代码。

## 35.3 Order-Statistic Trees: Trees as Sequences

AVL 树使用高度的扩增来实现自平衡。通过大小扩增可以生成一个树，该树作为序列工作，对于随机访问以及随机插入和删除都相当高效。相当高效的意思是 O(log(n))，因为它会保持高度扩增并且是平衡树。

