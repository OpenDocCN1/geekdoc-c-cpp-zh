
- PauseTransition - This does not do anything but call the onFinished code when it is completed. You can create one with `new PauseTransition(duration: Duration)`.

- RotateTransition - Rotates a Node through the transition. You can make one of these with `new RotateTransition(duration: Duration, node: Node)` or `new RotateTransition(duration: Duration)`. You should specify the axis, which is a scalafx.geometry.Point3D. You should also set the angle or byAngle property.

- ScaleTransition - Scales a given Node through a transition. You can create instances using `new ScaleTransition(duration: Duration)`.

```
new ScaleTransition(duration: Duration)
```

or

```
new ScaleTransition(duration: Duration, node: Node).
```

You should specify the fromX, fromY, and fromZ properties. Then you can either specify tX, tY, and tZ or byX, byY, and bZ.

- SequentialTransition - This is the other approach to combining transitions. The transitions put in a SequentialTransition will happen after another. You can create instances of using `new SequentialTransition(children: Seq[Animation])`, `new SequentialTransition(node: Node)`, or `new SequentialTransition(node: Node, children: Seq[Animation])`. You will need to specify the node or the children properties if you use an option that does not give them.

- StrokeTransition - This changes the color of a stroke on a Shape. You can create instances using `new StrokeTransition(duration: Duration)`, `new StrokeTransition(duration: Duration, shape: Shape)`, `new StrokeTransition(duration: Duration, fromValue: Color, toValue: Color)`.

or

```
new StrokeTransition(duration: Duration, shape: Shape, fromValue: Color, toValue: Color).
```

If you use an option that not set all the properties, you should set them on the created object.

- TranslateTransition - Moves/translates the Node through a transition. You can create instances using `new TranslateTransition(duration: Duration, node: Node)` or `new TranslateTransition(duration: Duration)`. You should specify fromX, fromY, and fromZ, then give it tX, tY, and tZ or byX, byY, and bZ.

Nearly all of these are demonstrated in the following example. The scene has two rectangles. The one top has a number of sequential transitions that are controlled by the user with some buttons. The bottom one is doing number of transitions in parallel.

## Graphics and Advanced ScalaFX

## Listing 12.7: Transactions.scala

```
import scalafax.Includes._
import scalafax.application.JFXApp
import scalafax.scene.Scene
import scalafax.event.ActionEvent
import scalafax.animation._
import scalafax.scene.control.Button
import scalafax.scene.layout.FlowPane
import scalafax.scene.paint.Color
import scalafax.scene.shape._
import scalafax.util.Duration

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Transactions"
    scene = new Scene(600, 400)
    val rect1 = Rectangle(20, 50, 100, 100)
    rect1.strokeWidth = 10
    val fadeTrans = new FadeTransition(new Duration(1000))
    fadeTrans.fromValue = 0.5
    fadeTrans.autoReverse = true
    val path = new CubicCurve
    path.startX = 70
    path.startY = 100
    path.controlX1 = 600
    path.controlY1 = 0
    path.controlX2 = 400
    path.controlY2 = 400
    path.endX = 530
    path.endY = 100
    val pathTrans = new PathTransition(new Duration(1000), path)
    val strokeTrans = new StrokeTransition(rect1, List(fadeTrans), Color.Black, Color.Cyan)

    seqTrans.autoReverse = true
    seqTrans.cycleCount = 4
    val startButton = new Button("Start")
    startButton.onAction = (e:ActionEvent) => seqTrans.play
    val pauseButton = new Button("Pause")
    pauseButton.onAction = (e:ActionEvent) => seqTrans.pause
    val stopButton = new Button("Stop")
    stopButton.onAction = (e:ActionEvent) => seqTrans.stop
    val flowPane = new FlowPane
    flowPane.children = List(startButton, pauseButton, stopButton)
    val rect2 = Rectangle(20, 280, 100, 100)
    val transTrans = new TranslateTransition(new Duration(2000))
    transTrans.fromX = 0
    transTrans.toX = 460
    val fillTrans = new FillTransition(new Duration(2000), Color.Black, Color.Green)
    val rotTrans = new RotateTransition(new Duration(2000))
    rotTrans.fromAngle = 0
    rotTrans.toAngle = 360
```

## Introduction to Programming and Problem-Solving Using Scala

![](img/06d4e84f27a8884ea40ba6182ec7c778_382_0.png)

FIGURE 12.8: The window that is produced by running Transitions.scala.

```
val parallel = new ParallelTransition(rect2, List(transTrans, fillTrans,
  rotTrans))
parallel.autoReverse = true
parallel.cycleCount = 100000

// Uncomfort to see non-eased motion
transTrans.interpolator = Interpolator.LINEAR
rotTrans.interpolator = Interpolator.LINEAR

content = List(rect1, rect2, flowPane)

parallel.play
```

You can see a sample of what this program looks like figure 12.8. Lines 16 to 35 set up the first rectangle with a FadeTransition, a PathTransition, and a StrokeTransition. Those three are put together in a SequentialTransition that is applied to the rectangle. Lines 36 to 41 buttons to control Sequential Transition. Lines 44 to 54 set up the second rectangle with a TranslateTransition, a FillTransition, and a RotateTransition. These are all combined in a ParallelTransition, so the rectangle at the bottom spins from side to side of the window while changing color from black to green and back.

All of the transitions use EASE_BOTH interpolation by default. If you uncomment lines 57 and 58 you will be able to see that the movement accelerates at the beginning and decelerates at the end.

Another approach to doing animation is with the Timeline. Each KeyFrame is a part of a pair which contains a time and a value. You can build a Timeline with different KeyFrames. The default interpolator for KeyFrame is LINEAR. If you run this code, you will find what interpolation looks like by comparison.

## Timelines

Using a Timeline with KeyFrames allows you to specify the change from the previous KeyFrame to the current one. KeyFrame can optionally have a name or an onFinish handler. Note that all the KeyFrames are associated with it. If you do not want to provide a single argument, you can do so with:

```
KeyFrame(time: Duration, value: KeyValue[_)
```
individual are created with different values, but the types need to match. If the target value is a Double then the endTime needs to be a Double. In fact, the types needs to be.

## Graphics and Advanced ScalaFX

The following example shows the use of a basic Timeline with three KeyFrames. It begins with a rectangle that is in the top left corner. When the user presses the “Start” button, the rectangle slides along the top and rotates one full time. Half across the top, it spinning and slides down to the bottom while still moving.

## Listing 12.8: Timelines.scala

```
import scalafax.Includes._
import scalafax.application.JFXApp
import scalafax.scene.Scene
import scalafax.event.ActionEvent
import scalafax.animation._
import scalafax.scene.control.Button
import scalafax.scene.layout.FlowPane
import scalafax.scene.paint.Color
import scalafax.scene.shape._
import scalafax.util.Duration

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Transitions"
    scene = new Scene(600, 400)
    val rect1 = Rectangle(20, 50, 100, 100)
    rect1.strokeWidth = 10
    val fadeTrans = new FadeTransition(new Duration(1000))
    fadeTrans.fromValue = 0.5
    fadeTrans.autoReverse = true
    val path = new CubicCurve
    path.startX = 70
    path.startY = 100
    path.controlX1 = 600
    path.controlY1 = 0
    path.controlX2 = 400
    path.controlY2 = 400
    path.endX = 530
    path.endY = 100
    val pathTrans = new PathTransition(new Duration(1000), path)
    val strokeTrans = new StrokeTransition(rect1, List(fadeTrans), Color.Black, Color.Cyan)

    seqTrans.autoReverse = true
    seqTrans.cycleCount = 4
    val startButton = new Button("Start")
    startButton.onAction = (e:ActionEvent) => seqTrans.play
    val pauseButton = new Button("Pause")
    pauseButton.onAction = (e:ActionEvent) => seqTrans.pause
    val stopButton = new Button("Stop")
    stopButton.onAction = (e:ActionEvent) => seqTrans.stop
    val flowPane = new FlowPane
    flowPane.children = List(startButton, pauseButton, stopButton)
    val rect2 = Rectangle(20, 280, 100, 100)
    val transTrans = new TranslateTransition(new Duration(2000))
    transTrans.fromX = 0
    transTrans.toX = 460
    val fillTrans = new FillTransition(new Duration(2000), Color.Black, Color.Green)
    val rotTrans = new RotateTransition(new Duration(2000))
    rotTrans.fromAngle = 0
    rotTrans.toAngle = 360

    val kv1 = KeyValue(rect1.translateX, 0)
    val kv2 = KeyValue(rect1.translateY, 0)
    val kv3 = KeyValue(rect1.rotate, 0)
    val kf1 = KeyFrame(new Duration(0), values = Set(kv1, kv2, kv3))
    val kv21 = KeyValue(rect1.translateX, 360)
    val kv22 = KeyValue(rect1.rotate, 360)
    val kf2 = KeyFrame(new Duration(1000), values = Set(kv21, kv22))
    val kv31 = KeyValue(rect1.translateX, 460)
    val kv32 = KeyValue(rect1.translateY, 230)
    val kf3 = KeyFrame(new Duration(2000), values = Set(kv31, kv32))

    val timeline = Timeline(List(kf1, kf2, kf3))
    timeline.play
  }
}
```
