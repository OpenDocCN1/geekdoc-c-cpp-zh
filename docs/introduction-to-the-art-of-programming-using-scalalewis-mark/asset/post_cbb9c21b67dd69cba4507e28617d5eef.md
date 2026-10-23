
Any combination of these is also an affine transformation.

The AffineTransform is represented by a 3x3 matrix in the computer, the details of which we will generally ignore. Interested readers can look at the Application Programming Interface (API) page for some details or should consider a course in graphics, which should cover the details of matrix transforms for application in both 2-D and 3-D graphics. When you call new AffineTransform() you get an identity transform. This is a transform that does not change anything and is represented for the identity matrix. There are options for passing arguments that will let you build the transformation matrix in whatever manner you desire.

Generally, you do not want to go down to the level of the matrix elements. Normally you want to be able to specify how much of a rotation or translation you want. There are number of methods that you can call to do exactly this.

- AffineTransform.getRotateInstance(theta:Double)
- AffineTransform.getRotateInstance(theta:Double, anchorx:Double, anchory:Double)
- AffineTransform.getScaleInstance(sx:Double, sy:Double)
- AffineTransform.getShearInstance(shx:Double, shy:Double)
- AffineTransform.getTranslateInstance(tx:Double, ty:Double)

These methods return AffineTransform instances that produce the specified transformations. For the rotations, the angle, theta, should be given in radians.

AffineTransforms can be combined as well. This can be done in a general way with the concatenate(tx:AffineTransform) method. There are also methods to build up more complex transforms.

- rotate(theta:Double)
- rotate(theta:Double, anchorx:Double, anchory:Double)
- scale(sx:Double, sy:Double)
- shear(shx:Double, shy:Double)
- translate(tx:Double, ty:Double)

These methods will alter the transform object, which is mutable, to include this new transform. It should be noted that the Graphics2D object as a whole had nearly identical methods. Calling those methods will apply these changes to the AffineTransform that is being used for drawing.

To illustrate what a transform can do, we will add one line of code into our running example.

```
g.rotate(math.Pi/4)
```

This line should be inserted after the QuadCurve is drawn and before the String is drawn. The result of adding this is shown in figure 12.6. Notice how the orientation of the String has been changed. This version of rotate does the rotation about the origin which is at the top-left corner by default. We turned it through π/4 radians, which is the same as 45 degrees.

![](img/157fcf510c119278e4b1267c62717fa8_331_0.png)

FIGURE 12.6: This figure shows what happens when we do a rotation before drawing our String.

```
override def paint(g:Graphics2D) {
    if(img == null || img.getWidth < size.width ||
        img.getHeight < size.height) {
        img=new BufferedImage(size.width, size.height,
            BufferedImage.TYPE_INT_ARGB)
    }
    val g2=img.createGraphics
    // Draw to g2
    g.drawImage(img,0,0,null)
}
```

The first line in the Panel creates a new variable to store images. The BufferedImage type specification is required here because otherwise Scala will infer a type of Null. In the paint method, the first thing that happens is a check to see if the image has been created and if it is large enough to cover the Panel. If not, a new image is created.

After we are certain that we have an image of sufficient size, the code gets the Graphics2D object for drawing to that image and anything that we want to draw is drawn to that image. The last thing to happen in the method is to draw the image to the Panel so it appears on screen.

## 12.3.4 Revisiting TexturePaint

Now that we know about images we can revisit one of the Paint types that was discussed earlier, TexturePaint. The idea of the TexturePaint is to fill in the drawn/filled shape with a specified image that it repeated on a certain grid. When you make a TexturePaint you provide it with an image and a rectangle that is referred to as the anchor. The image will appear inside of that rectangle and will be repeated in a tiling pattern around it. To illustrate this, we can enter the following code before setting the color to blue for the ellipse.

```
g.setPaint(new TexturePaint(ImageIO.read(new File("rtImg.png")),
    new Rectangle2D.Double(0,0,200,200)))
g.fill(new Ellipse2D.Double(0,200,500,300))
```

This fills in the same ellipse, but does so with a texture of a file that was loaded off disk. The result using this particular file is shown in figure 12.7.

## 12.4 Other Events

The standard components in the Swing library had code in them to publish events that were specific to the way you interacted with them or to make it very easy to provide the actions for those interactions. The Panel does not have any standard modes of interaction. The way in which the user interacts with it is completely up to you. As such, you have to handle events at a somewhat lower level. We need to listen to the mouse and keyboard actions directly and react to them appropriately.

![](img/157fcf510c119278e4b1267c62717fa8_335_0.png)

FIGURE 12.7: This image displays the use of a TexturePaint. The ellipse is filled with a tiling of an image that is loaded from a disk.

### 12.4.1 Mouse Events

The mouse is often the most natural way to interact with components of a GUI. At first you might think that the only thing you want to respond to with the mouse is the button clicks. However, if you take a minute to think about it you will realize that a lot of programs interact with the mouse in more complex ways than just when you click. There are eight different types of events that the mouse can fire. It is unlikely that you will care about all of them with any single panel, but you might need to handle several of them in order to produce the effect that you want.

These mouse events are available on all **Components**, even the standard ones that already handle things in their own ways. This allows you to include your own custom behavior. For this reason, all the **Components** contain an object called *mouse*. The *mouse* object, in turn, contains three **Publisher** objects called `clicks`, `moves`, and `wheel`. Each of these different **Publishers** will give you information about different things the mouse is doing. You need to listen to the one or ones that produce the events you need. So if you only need to know when the mouse is clicked, you would need to do `listenTo(mouse.clicks)`. If you wanted to know where the mouse was moving or being dragged to, you would add `mouse.moves` to the list of things you are listening to.

This is a list of the different events in `scala.swing.event` organized by which of the **Publishers** produces them.

- MouseEvent - All of the events listed below are all subtypes of MouseEvent.
- `mouse.clicks`
  - `MouseClicked`
  - `MouseEntered`
  - `MouseExited`
  - `MousePressed`
  - `MouseReleased`
- `mouse.moves`
  - `MouseMoved`
  - `MouseDragged`
- `mouse.wheel`
  - `MouseWheelMoved`

All of the mouse events contain *point*, *source*, and *modifiers* as members. The *point* member is a `java.awt.Point` and it has members in it for *x* and *y*. The *source* is a **Component** so that you can figure out what in your GUI the mouse is over when the event is produced. The modifiers are stored in an **Int** and can give you information about which mouse button or buttons are down.

Any time a mouse button goes down, a **MousePressed** event will fire. When the mouse button goes up, a **MouseReleased** event will fire. The **MouseClicked** event only fires if the mouse button goes down and back up without the mouse moving. If the mouse moves while it is down, instead of getting a **MouseClicked** event, you will get **MouseDragged** events through the movement.

Inside of the **reactions** to the event, you will likely change some mutable data that alters what is drawn. This change will not automatically be seen in the drawing, however.
