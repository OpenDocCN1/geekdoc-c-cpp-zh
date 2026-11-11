
Such a transformation is called an *affine transformation*. In the Java 2D API, the `AffineTransform` class describes such a transformation. If you know the components of a particular transformation matrix, you can construct it directly as

```
var t = new AffineTransform(a, b, c, d, e, f);
```

Additionally, the factory methods `getRotateInstance`, `getScaleInstance`, `getTranslateInstance`, and `getShearInstance` construct the matrices that represent these transformation types. For example, the call

```
t = AffineTransform.getScaleInstance(2.0F, 0.5F);
```

returns a transformation that corresponds to the matrix

```
[ 2    0    0 ]
[ 0   0.5   0 ]
[ 0    0    1 ]
```

Finally, the instance methods `setToRotation`, `setToScale`, `setToTranslation`, and `setToShear` set a transformation object to a new type. Here is an example:

```
t.setToRotation(angle); // sets t to a rotation
```

You can set the coordinate transformation of the graphics context to an `AffineTransform` object.

```
g2.setTransform(t); // replaces current transformation
```

However, in practice, you shouldn’t call the `setTransform` operation, as it replaces any existing transformation that the graphics context may have. For example, a graphics context for printing in landscape mode already contains a 90-degree rotation transformation. If you call `setTransform`, you obliterate that rotation. Instead, call the `transform` method.

```
g2.transform(t); // composes current transformation with t
```

It composes the existing transformation with the new `AffineTransform` object.

If you just want to apply a transformation temporarily, first get the old transformation, compose it with your new transformation, and finally restore the old transformation when you are done.

```
AffineTransform oldTransform = g2.getTransform(); // save old transform
g2.transform(t); // apply temporary transform
draw on g2
g2.setTransform(oldTransform); // restore old transform
```

## java.awt.geom.AffineTransform 1.2

- `AffineTransform(double a, double b, double c, double d, double e, double f)`
- `AffineTransform(float a, float b, float c, float d, float e, float f)`  
  constructs the affine transform with matrix

  $$
  \begin{bmatrix}
  a & c & e \\
  b & d & f \\
  0 & 0 & 1
  \end{bmatrix}
  $$

- `AffineTransform(double[] m)`
- `AffineTransform(float[] m)`  
  constructs the affine transform with matrix

  $$
  \begin{bmatrix}
  m[0] & m[2] & m[4] \\
  m[1] & m[3] & m[5] \\
  0 & 0 & 1
  \end{bmatrix}
  $$

- `static AffineTransform getRotateInstance(double a)`  
  creates a rotation around the origin by the angle *a* (in radians). The transformation matrix is

  $$
  \begin{bmatrix}
  \cos(a) & -\sin(a) & 0 \\
  \sin(a) & \cos(a) & 0 \\
  0 & 0 & 1
  \end{bmatrix}
  $$

  If *a* is between 0 and $\pi / 2$, the rotation moves the positive *x* axis toward the positive *y* axis.
- `static AffineTransform getRotateInstance(double a, double x, double y)`  
  creates a rotation around the point (*x*, *y*) by the angle *a* (in radians).
- `static AffineTransform getScaleInstance(double sx, double sy)`  
  creates a scaling transformation that scales the *x* axis by *sx* and the *y* axis by *sy*. The transformation matrix is

  $$
  \begin{bmatrix}
  sx & 0 & 0 \\
  0 & sy & 0 \\
  0 & 0 & 1
  \end{bmatrix}
  $$

## java.awt.geom.AffineTransform 1.2 *(Continued)*

- `static AffineTransform getShearInstance(double shx, double shy)`  
  creates a shear transformation that shears the *x* axis by `shx` and the *y* axis by `shy`. The transformation matrix is:

  ```
  [ 1   shx  0 ]
  [ shy  1   0 ]
  [ 0    0   1 ]
  ```

- `static AffineTransform getTranslateInstance(double tx, double ty)`  
  creates a translation transformation that moves the *x* axis by `tx` and the *y* axis by `ty`. The transformation matrix is:

  ```
  [ 1   0   tx ]
  [ 0   1   ty ]
  [ 0   0   1  ]
  ```

- `void setToRotation(double a)`
- `void setToRotation(double a, double x, double y)`
- `void setToScale(double sx, double sy)`
- `void setToShear(double shx, double shy)`
- `void setToTranslation(double tx, double ty)`  
  sets this affine transformation to a basic transformation with the given parameters. See the `getXxxInstance` methods for an explanation of the basic transformations and their parameters.

## java.awt.Graphics2D 1.2

- `void setTransform(AffineTransform t)`  
  replaces the existing coordinate transformation of this graphics context with `t`.
- `void transform(AffineTransform t)`  
  composes the existing coordinate transformation of this graphics context with `t`.
- `void rotate(double a)`
- `void rotate(double a, double x, double y)`
- `void scale(double sx, double sy)`
- `void shear(double sx, double sy)`
- `void translate(double tx, double ty)`  
  composes the existing coordinate transformation of this graphics context with a basic transformation with the given parameters. See the `AffineTransform.getXxxInstance` methods for an explanation of the basic transformations and their parameters.

## 11.3.7 Clipping

By setting a *clipping shape* in the graphics context, you constrain all drawing operations to the interior of that clipping shape.

```
g2.setClip(clipShape); // but see below
g2.draw(shape); // draws only the part that falls inside the clipping shape
```

However, in practice, you don’t want to call the setClip operation because it replaces any existing clipping shape that the graphics context might have. For example, as you will see later in this chapter, a graphics context for printing comes with a clip rectangle that ensures that you don’t draw on the margins. Instead, call the clip method.

```
g2.clip(clipShape); // better
```

The clip method intersects the existing clipping shape with the new one that you supply.

If you just want to apply a clipping area temporarily, you should first get the old clip, add your new clip, and finally restore the old clip when you are done:

```
Shape oldClip = g2.getClip(); // save old clip
g2.clip(clipShape); // apply temporary clip
draw on g2
g2.setClip(oldClip); // restore old clip
```

In Figure 11.50, we show off the clipping capability with a rather dramatic drawing of a line pattern clipped by a complex shape—namely, the outline of a set of letters.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_755_0.png)

**Figure 11.50** Using letter shapes to clip a line pattern

To obtain the character outlines, you need a *font render context*. Use the getFontRenderContext method of the Graphics2D class.

```java
FontRenderContext context = g2.getFontRenderContext();
```

Next, using a string, a font, and the font render context, create a `TextLayout` object:

```java
var layout = new TextLayout("Hello", font, context);
```

This text layout object describes the layout of a sequence of characters, as rendered by a particular font render context. The layout depends on the font render context—the same characters will look different on a screen and on a printer.

More important for our application, the `getOutline` method returns a `Shape` object that describes the shape of the outline of the characters in the text layout. The outline shape starts at the origin (0, 0), which might not be what you want. In that case, supply an affine transform to the `getOutline` operation to specify where you would like the outline to appear.

```java
AffineTransform transform = AffineTransform.getTranslateInstance(0, 100);
Shape outline = layout.getOutline(transform);
```

Then, append the outline to the clipping shape.

```java
var clipShape = new GeneralPath();
clipShape.append(outline, false);
```

Finally, set the clipping shape and draw a set of lines. The lines appear only inside the character boundaries.

```java
g2.setClip(clipShape);
var p = new Point2D.Double(0, 0);
for (int i = 0; i < NLINES; i++)
{
   double x = . . .;
   double y = . . .;
   var q = new Point2D.Double(x, y);
   g2.draw(new Line2D.Double(p, q)); // lines are clipped
}
```

| java.awt.Graphics 1.0 |
| :--- |
| • `void setClip(Shape s)` 1.2<br>sets the current clipping shape to the shape s. |
| • `Shape getClip()` 1.2<br>returns the current clipping shape. |
