![](bbox=[0.079, 0.074, 0.895, 0.411])

**FIGURE 19.5:** This UML class diagram shows a possible way to set up the hierarchy for our first three Drawable subtypes.

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
```