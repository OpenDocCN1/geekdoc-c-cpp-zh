# Graphics and Advanced ScalaFX

- new Light.Spot(x: Double, y: Double, specularExponent: Double, color: Color)

+   - MotionBlur - Creates the effect of blurring from motion. You can create one with new
MotionBlur(angle: Double, radius: Double). The angle specifies the perceived
direction of motion and the radius tells it how much blurring to do.

+   - PerspectiveTransform - This effect cannot be done with affine transforms, when viewed in
perspective, parallel lines appear to meet in the distance. You can create
one with new PerspectiveTransform(ulx: Double, uly: Double, urx: Double,
ury: Double, lx: Double, lry: Double, llx: Double, lly: Double), the vals
used in pass to specify the location of corners of a quadrilateral or the Node is
mapped to.

+   - Reflection - This renders a reflected version of the node below the actual con-
ent. You can create one using new Reflection(topOffset: Double, fraction:
Double, topOpacity: Double, bottomOpacity: Double). The opacities allow the
reflection to have a fading appearance.

+   - SepiaTone - Applies a sepia coloration to an image. You can create one with new
SepiaTone(level: Double).

+   - Shadow - This creates a shadow of the Node it is attached to. Unlike DropShadow,
it does not show both the original and the shadow. You can create one with new
Shadow(radius: Double, color: Color) or new Shadow(blurType: BlurType,
color: Color, radius: Double). The BlurType has the same options as mentioned
for DropShadow.

Usage of the mastery of these is shown in the following code. In particular, this code
displays the ones that work with text. Effects that work best with images are shown
in section 12.3.

# Listing 12.11: Effects.scala

```
import scalafx.Includes.
import scalafx.application.JFXApp
import scalafx.scene.
import scalafx.scene.effect.
import scalafx.scene.paint.
import scalafx.scene.shape.
import scalafx.scene.text.
def makeText(x: Double, y: Double, s: String, effect: Effect, darkBack: Boolean):Node = {
 val text = new Text(x, y, s)
text.font = Font("serif", FontWeight.Bold, 40)
text.fill = if (darkBack) Color.White else Color.Black
text.effect = effect
if (darkBack) {
 val group = new Group
val b = text.boundsInLocal.value
val r = Rectangle(b.minX, b.minY, b.width, b.height)
r.fill = Color.Black
group.children = List(r, text)
group}
```