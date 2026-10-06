
ColorAdjust - This effect detects per-pixel adjustments to hue, brightness, and contrast. You create one new ColorAdjust(hue: Double, saturation: Double, brightness: Double, contrast: Double).

ColorInput - Renders a rectangular region that is filled with the grey Paint. You create one new ColorInput(x: Double, y: Double, width: Double, height: Double, paint: Paint).

DisplacementMap - This causes the image to be rendered with offsets specified by a FlowMap. This allows you to do things like make a Node appear wavy. You create one new DisplacementMap(mapData: FlowMap, offsetX: Double, offsetY: Double, scale: Double, scale: Double) or new DisplacementMap(mapData: FlowMap). The FlowMap can be created using new FlowMap(width: Int, height: Int) and the values in it are set using the setDefs(x: Int, y: Int, s: Float, f: Unit) method.

DropShadow - Renders a shadow given the content with a specified radius, offset, and color. You create one new DropShadow(radius: Double, offsetX: Double, offsetY: Double, color: Color), new DropShadow(radius: Double, color: Color), or new DropShadow(blurType: BlurType, color: Color, radius: Double, spread: Double, offsetX: Double, offsetY: Double). The BlurType can be one of the four values: BlurType.Gaussian, BlurType.OnePassBox, BlurType.ThreePassBox, BlurType.TwoPassBox.

GaussianBlur - This blurs the image using a Gaussian function with the specified radius. You create one new GaussianBlur(radius: Double).

Glow - Makes an image appear to glow. You can create one with new Glow(level: Double).

InnerShadow - Renders a shadow inside the edges of some content with a specified radius, offset, and color. You create one new InnerShadow(radius: Double, offsetX: Double, offsetY: Double, color: Color), new InnerShadow(radius: Double, color: Color), or new InnerShadow(blurType: BlurType, color: Color, radius: Double, choke: Double, offsetX: Double, offsetY: Double). The BlurType is one of the same values used for DropShadow.

Lighting - Creates the effect of a light shining on an element to make it a more realistic look. You create one new Lighting(light: Light). The Light type is created by instantiating one of three subtypes, Light.Distant, Light.Point, or Light.Spot. These can be made using the following calls:

- new Light.Distant (azimuth: Double, elevation: Double; color: Double, color: Color)
- new Light.Point (x: Double, y: Double, z: Double, color: Color)

> ⁸The FlowMap type different "bands" can be used for different things. The DisplacementMap uses two bands for x and y values, respectively.

> ⁹These are the names used at the time of writing. The developers of ScalaFX appear to be moving to a camel-standard, so it is likely in the future these will be Gaussian, OnePassBox, ThreePassBox, and TwoPassBox instead.

# Graphics and Advanced ScalaFX

- new Light.Spot(x: Double, y: Double, specularExponent: Double, color: Color)

- MotionBlur - Creates the effect of blurring from motion. You can create one with new MotionBlur(angle: Double, radius: Double). The angle specifies the perceived direction of motion and the radius tells it how much blurring to do.

- PerspectiveTransform - This effect cannot be done with affine transforms, when viewed in perspective, parallel lines appear to meet in the distance. You can create one with new PerspectiveTransform(ulx: Double, uly: Double, urx: Double, ury: Double, lx: Double, lry: Double, llx: Double, lly: Double), the vals used in pass to specify the location of corners of a quadrilateral or the Node is mapped to.

- Reflection - This renders a reflected version of the node below the actual content. You can create one using new Reflection(topOffset: Double, fraction: Double, topOpacity: Double, bottomOpacity: Double). The opacities allow the reflection to have a fading appearance.

- SepiaTone - Applies a sepia coloration to an image. You can create one with new SepiaTone(level: Double).

- Shadow - This creates a shadow of the Node it is attached to. Unlike DropShadow, it does not show both the original and the shadow. You can create one with new Shadow(radius: Double, color: Color) or new Shadow(blurType: BlurType, color: Color, radius: Double). The BlurType has the same options as mentioned for DropShadow.

Usage of the mastery of these is shown in the following code. In particular, this code displays the ones that work with text. Effects that work best with images are shown in section 12.3.

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
text.effect = effect
if (darkBack) {
 val group = new Group
val r = new Rectangle(text.bounds)
r.fill = Color.Black
group.children.addAll(r, text)
group
} else {
  text
}
}

val app = new JFXApp {
  stage = new Stage {
    scene = new Scene {
      val root = new VBox(10) {
        val bloom = makeText(20, 40, "Bloom", new Bloom(), true)
        val boxBlur = makeText(20, 80, "BoxBlur", new BoxBlur(), false)
        val displacementMap = makeText(20, 120, "DisplacementMap", new DisplacementMap(), false)
        val gaussianBlur = makeText(20, 160, "GaussianBlur", new GaussianBlur(), false)
        val innerShadow = makeText(20, 200, "InnerShadow", new InnerShadow(), false)
        val lighting = makeText(20, 240, "Lighting", new Lighting(new Light.Distant(0, 45, Color.White)), true)
        val motionBlur = makeText(20, 280, "MotionBlur", new MotionBlur(15, 10), false)
        val perspective = makeText(20, 320, "Perspective", new PerspectiveTransform(500, 500, 400, 520), false)
        val reflection = makeText(20, 360, "Reflection", new Reflection(0.5, 1.0, 0.0), false)
        val shadow = makeText(20, 400, "Shadow", new Shadow(5, Color.Black), false)
        root.children.addAll(bloom, boxBlur, displacementMap, gaussianBlur, innerShadow, lighting, motionBlur, perspective, reflection, shadow)
      }
      content = root
    }
    title = "Effects"
  }
}

app.main(args)
```

![](img/06d4e84f27a8884ea40ba6182ec7c778_401_0.png)

FIGURE 12.12: The window that is produced by running Effects.scale.

# Introduction to Programming and Problem-Solving Using Scala

# Listing 12.12: ImageEffects.scala

A output of this program can be seen in figure 12.13.¹10
