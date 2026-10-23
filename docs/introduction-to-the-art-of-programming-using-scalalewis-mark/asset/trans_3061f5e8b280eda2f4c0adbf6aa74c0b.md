

![](img/157fcf510c119278e4b1267c62717fa8_505_0.png)

**图 19.5：** 该 UML 类图展示了一种为我们前三个 Drawable 子类型设置层次结构的可行方式。

```
/**
 * This class represents a transformation with children.
 *
 * @param parent the DrawTransform that is the parent of this Drawable.
 */
class DrawTransform(parent:DrawTransform) extends Drawable {
  private val subnodes = mutable.Buffer[Drawable]()
  private var propPanel:Component = null

  private object TransformType extends Enumeration {
    val Translate,Rotate,Scale,Shear = Value
  }
  import TransformType._

  private var transformType = Translate
  private val transformValue = Array.fill(3)(0.0)

  /**
   * This method applies a transform and draws all the subnodes.
   *
   * @param g the Graphics2D object to draw to.
   */
  def draw(g:Graphics2D) {
    val oldTrans = g.getTransform
    g.transform(buildTransform)
    subnodes.foreach(_.draw(g))
    g.setTransform(oldTrans)
  }

  private def buildTransform:AffineTransform = transformType match {
    case Translate =>
      AffineTransform.getTranslateInstance(transformValue(0),transformValue(1))
    case Rotate =>
      AffineTransform.getRotateInstance(transformValue(0),transformValue(1),transformValue(2))
    case Scale =>
      AffineTransform.getScaleInstance(transformValue(0),transformValue(1))
    case Shear =>
      AffineTransform.getShearInstance(transformValue(0),transformValue(1))
  }

  /**
   * Returns a GUI element for setting parameters.
   * If this method is called multiple times, the same object will be returned.
   *
   * @return a Component that can be added to a Swing GUI.
   */
  def propertiesPanel() : Component = {
    if(propPanel == null) {
      propPanel = new BorderPanel {
        layout += new GridPanel(transformValue.length+1,1) {
          contents += new ComboBox(TransformType.values.toSeq) {
            listenTo(selection)
            reactions += { case e => if(selection.item!=null)
              transformType=selection.item }
          }
          for(i <- transformValue.indices) {
            val textField = new TextField(transformValue(i).toString) {
              listenTo(this)
              reactions += { case e:EditDone => transformValue(i)=text.toDouble }
            }
            contents += textField
          }
        } -> BorderPanel.Position.North
      }
    }
    propPanel
  }

  /**
   * Returns an object that can be used to run through the children.
   *
   * @return a java.util.Enumeration object for the subnodes.
   */
  def children : java.util.Enumeration[Drawable] = new
    java.util.Enumeration[Drawable] {
    val iter = subnodes.iterator
    def hasMoreElements() = iter.hasNext
    def nextElement() = iter.next
  }
  /**
   * Tells whether this can have children.
   *
   * @return always true for this type.
   */
  def getAllowsChildren : Boolean = true
  */

  /**
   * Returns the child at a specified index.
   *
   * @param childIndex the index in the sequence of children.
   * @Return the child at that index.
   */
  def getChildAt(childIndex : Int) : Drawable = subnodes(childIndex)

  /**
   * Returns how many children this node has.
   *
   * @Return the number of children currently under this node.
   */
  def getChildCount : Int = subnodes.length

  /**
   * Returns the index of a particular object.
   *
   * @param node a TreeNode to search for in the sequence of children.
   * @Return the index of that child of -1 if it isn't a child.
   */
  def getIndex(node : TreeNode) : Int = subnodes.indexOf(node)

  /**
   * Returns the parent of this node.
   *
   * @Return the parent of this node. Will be null if this is the root.
   */
  def getParent : DrawTransform = parent

  /**
   * Tells is this node is a leaf in the tree.
   *
   * @Return true if there are currently no children, otherwise false.
   */
  def isLeaf : Boolean = subnodes.isEmpty

  /**
   * Adds a child to this node.
   *
   * @param c the node to add.
   */
  def addChild(c : Drawable) { subnodes += c }

  /**
   * Removes the specified drawable from the sequence of children.
   *
   * @param c the node to remove.
   */
  def removeChild(c : Drawable) { subnodes -= c }

  override def toString() = "Transform"
}
```

该类有四个私有数据成员。第一个名为 subnodes，它是一个 Buffer，用于存储变换的所有子节点。5 这些子节点就是变换将被应用到的对象。下一章将详细介绍 Buffer 类型。第二个是一个 Component，用于保存对属性面板的引用。出于下面将看到的原因，它最初为 null。其余两个成员数据分别是变换类型的枚举和与变换关联的数值数组。枚举类型在私有对象中定义。有关枚举的详细信息请参见旁注。

## 枚举

DrawTransform 的 transformType 成员需要能够取一组很小的值中的一个。使用 Int 来实现这一点是可行的，但 Int 类型允许超过 40 亿个不同的可能值。我们只希望允许四种。需要一种只有少量可能值的类型在编程中非常常见。满足此要求的类型称为枚举。许多语言仅为创建这些类型而包含特殊的语言构造，通常使用关键字 enum。Scala 的目标之一是可扩展性，而枚举正是这一点的完美体现。

DrawTransform 的定义展示了通过让对象扩展 scala.Enumeration 类来创建的枚举类型。枚举的不同值是通过 val 声明创建的，其中将我们想要的四个可能选项设置为 Value。Value 来自 Enumeration。

在此声明之后，类型 TransformType.Value 仅允许 Translate、Rotate、Scale 和 Shear 作为值。如果尝试将该类型的引用，例如 transformType 设置为其他任何值，将导致语法错误。

成员之后是各种方法，首先是继承自 Drawable 的那些方法。首先是 draw 方法。该方法将 g 中的当前变换存储在临时变量中，然后将要使用的变换应用到 g 上。buildTransform 方法根据枚举值进行匹配，并生成适当的变换类型，同时传递数组中的 2 或 3 个值。之后，subnodes 的每个元素都被告知绘制自身。绘制完成后，g 上的变换被设置回原来的状态。

draw 之后是 propertiesPanel 方法。如 scaladoc 注释所述，如果多次调用此方法，应返回相同的对象。因此，它始终返回 propPanel。但是，如果 propPanel 为 null，它会将其更改为引用一个新构建的面板，该面板具有一个 ComboBox 和三个 TextFields，并带有适当的事件处理，以便在 ComboBox 选择更改时更改 transformType，或在文本字段被编辑时更改 transformValue 数组中的值。6

文件中的接下来是 TreeNode 所要求的七个方法。其中大多数基于 subnodes 的内容有直接的实现。其中有两个方法值得进一步讨论。第一个是 children 方法。该方法值得注意

5 Buffer 类型将在下一章详细介绍。简而言之，它就像一个具有增长和收缩能力的数组。

6 此代码如果用户输入的不是有效的 Double 值则不会进行适当的异常处理。修复此问题留给读者作为练习。

因为它必须返回 java.util.Enumeration 类型的对象。此类型不像我们刚才看到的枚举那样。此类型基本上是一个迭代器，最初包含在 Java 库中。Java 的后续版本创建了自己的 Iterator 类型，也在 java.util 中，但任何已经使用 Enumeration 的库类，如 TreeNode，都被困在了那个类型上。

Scala 集合通常不会生成 java.util.Enumeration，因此我们必须自己创建。我们通过创建一个继承自 java.util.Enumeration 的匿名类来实现。幸运的是，Enumeration 只有两个抽象方法需要实现：hasMoreElements 和 nextElement。这些方法的实现非常直接，使用我们从 subnodes 获取的迭代器。

另一个有趣的方法是 getParent。此方法的实现非常简单，但它迫使我们在类的顶部放置一个参数，以便在创建 DrawTransform 时必须提供父节点。关于 getParent 的另一个有趣点是返回类型。TreeNode 类型中的 getParent 方法指定返回类型为 TreeNode。但是，当你重写一个方法时，允许将返回类型更改为更具体的子类型。在这种情况下，我们知道所有父节点都将是 DrawTransform 类型，它是 TreeNode 的子类型，因此我们没有违反超类型指定的内容。getChild 方法也返回比 TreeNode 要求更具体的类型。

DrawTransform 中的接下来两个方法是 addChild 和 removeChild。这些方法没有从任何超类型继承。它们存在于此处，以便 Drawing 类型可以在不完全破坏 subnodes 封装的情况下对子节点执行所需的操作。最后是 toString 方法的重写，以便变换对象在 GUI 中显示得更好。

完成 DrawTransform 后，我们现在可以转向 Drawable 层次结构的另一侧。我们将从 DrawLeaf 开始。它是一个 trait，只会实现 TreeNode 所要求的那些方法。

```
package scalabook.drawing

import javax.swing.tree.TreeNode
import java.util.Enumeration

/**
 * A supertype for Drawables that don't allow children.
 */
trait DrawLeaf extends Drawable {
  val parent:DrawTransform

  /**
   * Returns an empty enumeration.
   */
  def children : Enumeration[Drawable] = new Enumeration[Drawable] {
    def hasMoreElements() = false
    def nextElement() = null
  }

  /**
   * Returns false.
   */
  def getAllowsChildren : Boolean = false
```

