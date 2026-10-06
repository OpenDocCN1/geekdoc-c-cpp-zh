
```scala
scene = new Scene(500, 300) {
  val path += MoveTo(50, 50)
  path.elements += VLineTo(250)
  path.elements += HLineTo(250)
  path.elements += LineTo(300, 200)
  path.elements += CubicCurveTo(500, 300, 500, 0, 100, 100)
  path.elements += QuadCurveTo(250, 0, 100)
  path.elements += Arc(100, 45, 50, 0, 50, false)
  path.elements += new ClosePath
}

val path2 = new Path
  path2.elements += MoveTo(75, 75)
  path2.elements += VLineTo(175)
  path2.elements += HLineTo(175)
  path2.elements += VLineTo(75)
  path2.elements += CubicCurveTo(0, 175, 250, 175, 75)
  path2.fill = FillRule.EvenOdd
  path2.fill = Color.Blue

val path3 = new Path
  path3.elements += MoveTo(275, 75)
  path3.elements += VLineTo(175)
  path3.elements += HLineTo(375)
  path3.elements += LineTo(75)
  path3.elements += CubicCurveTo(200, 175, 450, 175, 675)
  path3.fill = FillRule.NonZero
  path3.fill = Color.Cyan

content = List(path, path2, path3)
```

You can see the window produced by this code in figure 12.2. The variable named path sets up the perimeter and includes each of the different elements. The smaller paths have a box where one edge is a cubic curve that forms a loop. The loop allows us to illustrate that there are two methods that can be used for filling. There are FillRule.EvenOdd and FillRule.NonZero. The darker shape on the left uses EvenOdd rule. With this rule, whether a region is filled depends on if you cross an odd or even number of times. The central loop is filled because it requires crossing two parts of the path. The lighter shape on the right uses NonZero rule. This fills the central loop that would require going over the path more than zero times. Note that you can also specify the fill of SVG.

## Paint and Stroke

The way in which different shapes are drawn is determined by different settings. When you create a Circle or a Rectangle, you can pass in a color to use for the fill property.

![](img/06d4e8f27a888ea40ba6182ec778_361)

**FIGURE 12.1:** The window produced by Path.scala. The smaller paths show different rules for paths. For any other shape, you need to make the shape first and then set the property. So far we have only looked at using Colors for the fill, but there are other subtypes of general Paint type, LinearGradient and RadialGradient. All of these are found in scalafx.scene.package. You can also change the way lines are drawn using settings for the stroke. You can change the paint style, the dashing, the way they are joined, where the line is relative to the shape, and the width of the line. The code below demonstrates both point and stroke settings.

### ShapeSettings.scala

```scala
import scalafx.application.JFXApp
import scalafx.scene.Scene
import scalafx.scene.Paint._
import scalafx.scene.shape._

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Shape Settings"
    scene = new Scene(500, 300, 300) {
      val polygon1 = Polygon(10, 10, 100, 190, 100)
      polygon1.fill = Color.Green
      polygon1.stroke = Color.Black
      polygon1.strokeWidth = 5
      polygon1.strokeType = StrokeType.Centered
      polygon1.strokeLineJoin = StrokeJoin.Bevel

      val polygon2 = Polygon(160, 10, 250, 190, 340, 100)
      polygon2.fill = LinearGradient(160, 10, 340, 100, false, CycleMethod.NoCycle,
        Stop(0.0, Color.White), Stop(0.3, Color.Cyan), Stop(0.7, Color.Blue), Stop(1.0, Color.Black))
    }
  }
}
```

## Introduction to Programming and Problem-Solving Using Scala

```scala
polygon2.stroke = Color.Black
polygon2.strokeWidth = 5
polygon2.strokeType = StrokeType.Inside
polygon2.strokeLineJoin = StrokeJoin.Miter
```

```scala
val polygon3 = Polygon(310, 10, 400, 190, 100)
polygon3.fill = RadialGradient(45, 0.5, 400, 100, 50, false, CycleMethod.Reflect, Stop(0.0, Color.White), Stop(0.5, Color.Red), Stop(1.0, Color.Black))
polygon3.stroke = Color.Black
polygon3.strokeWidth = 5
polygon3.strokeType = StrokeType.Outside
polygon3.strokeLineJoin = StrokeJoin.Round
```

```scala
val line1 = Line(50, 220, 450, 220)
line1.stroke = Color.Black
line1.strokeWidth = 5
line1.strokeLineCap = StrokeLineCap.Butt
line1.strokeArray = List(30, 10, 20, 15)
```

```scala
val line2 = Line(50, 250, 450, 250)
line2.stroke = Color.Black
line2.strokeWidth = 5
line2.strokeLineCap = StrokeLineCap.Round
line2.strokeArray = List(30, 10, 20, 15)
```

```scala
val line3 = Line(50, 220, 450, 220)
line3.stroke = Color.Black
line3.strokeWidth = 5
line3.strokeLineCap = StrokeLineCap.Square
line3.strokeArray = List(30, 10, 20, 15)
```

You can see the window produced by this code in figure 12.2. The variable named path sets up the perimeter and includes each of the different elements. The smaller paths have a box where one edge is a cubic curve that forms a loop. The loop allows us to illustrate that there are two methods that can be used for filling. There are FillRule.EvenOdd and FillRule.NonZero. The darker shape on the left uses EvenOdd rule. With this rule, whether a region is filled depends on if you cross an odd or even number of times. The central loop is filled because it requires crossing two parts of the path. The lighter shape on the right uses NonZero rule. This fills the central loop that would require going over the path more than zero times. Note that you can also specify the fill of SVG.

## Paint and Stroke

The way in which different shapes are drawn is determined by different settings. When you create a Circle or a Rectangle, you can pass in a color to use for the fill property.

![](img/06d4e8f27a888ea40ba6182ec778_361)

**FIGURE 12.2:** The window produced by Path.scala. The smaller paths show different rules for paths. For any other shape, you need to make the shape first and then set the property. So far we have only looked at using Colors for the fill, but there are other subtypes of general Paint type, LinearGradient and RadialGradient. All of these are found in scalafx.scene.package. You can also change the way lines are drawn using settings for the stroke. You can change the paint style, the dashing, the way they are joined, where the line is relative to the shape, and the width of the line.

### ShapeSettings.scala

```scala
import scalafx.application.JFXApp
import scalafx.scene.Scene
import scalafx.scene.Paint._
import scalafx.scene.shape._

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Shape Settings"
    scene = new Scene(500, 300, 300) {
      val polygon1 = Polygon(10, 10, 100, 190, 100)
      polygon1.fill = Color.Green
      polygon1.stroke = Color.Black
      polygon1.strokeWidth = 5
      polygon1.strokeType = StrokeType.Centered
      polygon1.strokeLineJoin = StrokeJoin.Bevel

      val polygon2 = Polygon(160, 10, 250, 190, 340, 100)
      polygon2.fill = LinearGradient(160, 10, 340, 100, false, CycleMethod.NoCycle,
        Stop(0.0, Color.White), Stop(0.3, Color.Cyan), Stop(0.7, Color.Blue), Stop(1.0, Color.Black))
    }
  }
}
```

## Introduction to Programming and Problem-Solving Using Scala

```scala
polygon2.stroke = Color.Black
polygon2.strokeWidth = 5
polygon2.strokeType = StrokeType.Inside
polygon2.strokeLineJoin = StrokeJoin.Miter
```

```scala
val polygon3 = Polygon(310, 10, 400, 190, 100)
polygon3.fill = RadialGradient(45, 0.5, 400, 100, 50, false, CycleMethod.Reflect, Stop(0.0, Color.White), Stop(0.5, Color.Red), Stop(1.0, Color.Black))
polygon3.stroke = Color.Black
polygon3.strokeWidth = 5
polygon3.strokeType = StrokeType.Outside
polygon3.strokeLineJoin = StrokeJoin.Round
```

```scala
val line1 = Line(50, 220, 450, 220)
line1.stroke = Color.Black
line1.strokeWidth = 5
line1.strokeLineCap = StrokeLineCap.Butt
line1.strokeArray = List(30, 10, 20, 15)
```

```scala
val line2 = Line(50, 250, 450, 250)
line2.stroke = Color.Black
line2.strokeWidth = 5
line2.strokeLineCap = StrokeLineCap.Round
line2.strokeArray = List(30, 10, 20, 15)
```

```scala
val line3 = Line(50, 220, 450, 220)
line3.stroke = Color.Black
line3.strokeWidth = 5
line3.strokeLineCap = StrokeLineCap.Square
line3.strokeArray = List(30, 10, 20, 15)
```

You can see the window produced by this code in figure 12.2. The variable named path sets up the perimeter and includes each of the different elements. The smaller paths have a box where one edge is a cubic curve that forms a loop. The loop allows us to illustrate that there are two methods that can be used for filling. There are FillRule.EvenOdd and FillRule.NonZero. The darker shape on the left uses EvenOdd rule. With this rule, whether a region is filled depends on if you cross an odd or even number of times. The central loop is filled because it requires crossing two parts of the path. The lighter shape on the right uses NonZero rule. This fills the central loop that would require going over the path more than zero times.

## Shape Settings

![](img/06d4e8f27a888ea40ba6182ec778_363)

**FIGURE 12.3:** The window produced by Path.scala. The smaller paths show different rules for paths. For any other shape, you need to make the shape first and then set the property. So far we have only looked at using Colors for the fill, but there are other subtypes of general Paint type, LinearGradient and RadialGradient. All of these are found in scalafx.scene.package. You can also change the way lines are drawn using settings for the stroke. You can change the paint style, the dashing, the way they are joined, where the line is relative to the shape, and the width of the line.
