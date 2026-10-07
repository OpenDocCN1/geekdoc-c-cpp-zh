
If you use a spine key, the property follows a path similar to the orange spine shown in Figure 14-7. In this example, on the left side of the graph, the value starts by changing relatively little as time increases; in the middle of the graph, the value changes quickly; and near the right side of the graph, the value decreases again. The result is that the value starts moving slowly, picks up the pace, and then slows down before reaching its final value.

You use the KeySpine attribute to specify the control points for a key frame with splines. This attribute should contain two points that give the control point coordinates in a normalized system (0 ≤ X ≤ 1, and 0 ≤ Y ≤ 1).

The RovingButtonWithSplines example uses the following code to make its Button follow the rectangular path followed by the RovingButton and RovingButtonWithKeyFrames. The programs are the same, but the speed with which the Button moves is different. In the earlier programs, the Button moves at a constant speed across each of the Rectangle's sides. In this, it's actually a pretty nice effect. Download the program from the book's website and see it for yourself.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_287_0.png)

```
<Storyboard X:Key="moveButton" RepeatBehavior="Forever">
  <DoubleAnimationUsingKeyFrames
    Storyboard.TargetName="btnM"
    Storyboard.TargetProperty="Canvas.Left">
    <SpineDoubleKeyFrame Value="370" KeyTime="0:0:1.5" KeySpine="0.5,0.5,0.5,1"/>
    <SpineDoubleKeyFrame Value="370" KeyTime="0:0:2.5"/>
    <SpineDoubleKeyFrame Value="10" KeyTime="0:0:4"/>
    <SpineDoubleKeyFrame Value="10" KeyTime="0:0:5"/>
    <SpineDoubleKeyFrame Value="160" KeyTime="0:0:2.5"/>
    <SpineDoubleKeyFrame Value="160" KeySpine="0.5,0.5,0.5,1"/>
  </DoubleAnimationUsingKeyFrames>
  <DoubleAnimationUsingKeyFrames
    Storyboard.TargetName="btnM"
    Storyboard.TargetProperty="Canvas.Top">
    <SpineDoubleKeyFrame Value="10" KeyTime="0:0:1.5"/>
    <SpineDoubleKeyFrame Value="160" KeyTime="0:0:2.5"/>
    <SpineDoubleKeyFrame Value="160" KeyTime="0:0:4"/>
    <SpineDoubleKeyFrame Value="160" KeyTime="0:0:5"/>
  </DoubleAnimationUsingKeyFrames>
</Storyboard>
```

RovingButtonWithSplines

# Discrete Key Frames

Linear and spine key frames move a property continuously from one value to another. A discrete key frame makes a property suddenly jump from one value to another.

The RovingButtonDiscrete example uses the following code to animate this Button:

```
<Storyboard x="sbButton" RepeatBehavior="Forever">
  <DoubleAnimationUsingKeyFrames>
    <Storyboard.TargetName="move" Target="Canvas.Left">
      <DiscreteKeyFrame Value="130" KeyTime="0:0:0.5"/>
      <DiscreteKeyFrame Value="250" KeyTime="0:0:1.0"/>
      <DiscreteKeyFrame Value="370" KeyTime="0:0:1.5"/>
      <DiscreteKeyFrame Value="370" KeyTime="0:0:2.5"/>
      <DiscreteKeyFrame Value="250" KeyTime="0:0:3.5"/>
      <DiscreteKeyFrame Value="130" KeyTime="0:0:4.0"/>
    </Storyboard.TargetName>
  </DoubleAnimationUsingKeyFrames>
  <DoubleAnimationUsingKeyFrames>
    <Storyboard.TargetName="move" Target="Canvas.Top">
      <DiscreteKeyFrame Value="85" KeyTime="0:0:0.2"/>
      <DiscreteKeyFrame Value="160" KeyTime="0:0:2.5"/>
      <DiscreteKeyFrame Value="85" KeyTime="0:0:4.5"/>
      <DiscreteKeyFrame Value="10" KeyTime="0:0:5.0"/>
    </Storyboard.TargetName>
  </DoubleAnimationUsingKeyFrames>
</Storyboard>
```

The example moves the Button in a rectangular path as much as the previous, but the Button moves in discrete jumps rather than smooth movements. Because discrete frames don't generate any intermediate values, the code must list every value you want.

# Path Animations

Path animations follow the coordinates or angle of a path. For example, you can use a path animation to move along the border of an ellipse or a series of curves. The RovingButtonWithPath example shown in Figure 14-8 moves a Button along the path shown in black. As it moves, the Button rotates to match the curve's angle at that point. RovingButtonWithPath program uses the following code to animate its Button:

```
<PathGeometry x="pathMove"
  Figures="M10 85 A 100,70 0 1 210,85 A 100,70 0 1 10,150"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_288_0.png)

Figure 14-8

# EVENT TRIGGERS AND ANIMATION

```
<Storyboard x:Key="sbMoveButton" RepeatBehavior="Forever">
  <DoubleAnimationUsingPath Duration="0:0:0:4">
    Storyboard.TargetName="btnMover"
    Storyboard.TargetProperty="Canvas.Left"
    Source="X"
    <PathGeometry x="StaticResource pathMove"/>
  </DoubleAnimationUsingPath>
  <DoubleAnimationUsingPath Duration="0:0:0:4">
    Storyboard.TargetName="btnMover"
    Storyboard.TargetProperty="Canvas.Top"
    Source="Y"
    <PathGeometry x="StaticResource pathMove"/>
  </DoubleAnimationUsingPath>
  <DoubleAnimationUsingPath Duration="0:0:0:4">
    Storyboard.TargetName="btnMover"
    Storyboard.TargetProperty="RenderTransform.Angle"
    Source="Angle"
    <PathGeometry x="StaticResource pathMove"/>
  </DoubleAnimationUsingPath>
</Storyboard>
```

RovingButtonWithPath The code creates a PathGeometry object to define the path. Then that object in sbMoveButton Storyboard's first DoubleAnimationUsingPath changes the Button's Canvas.Left property. The property should be set to the path's X coordinate as the animation progresses over the path. Similarly, the second DoubleAnimationUsingPath object matches the Button's Canvas.Top property to the path's Y coordinate as the animation progresses. The Button's definition includes a RenderTransform object that initially rotates the Button by -90 degrees. The final animation object makes the Button's Transform property match the path's Angle during the animation.

# Mix and Match Key Frames

Each of the previous key frame examples uses a single type of key frame, but you can mix and match them. For example, a single storyboard might include linear key frames and discrete key frames. The storyboard can even include path animations. The RovingButtonKeyFrames example program shown in Figure 14-9 demonstrates a mix of linear and discrete key frames, and path animation. When you click on the Start button, the Button follows the route drawn in black.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_289_0.png)

Figure 14-9

The RovingButtonKeyFrames program uses the following code to animate its Button:

```
<PathGeometry key="pathMove"
  Figures="M 30,10 A 50 0 1 150,170"/>
<Storyboard x="sbmoveButton" RepeatBehavior="Forever">
  <!-- Move right -->
  <DoubleAnimationUsingKeyFrames BeginTime="0:0:0:0">
    Storyboard.TargetName="btnMover"
    Storyboard.TargetProperty="(Canvas.Left)"
    <LinearKeyFrame KeyTime="0:0:1" Value="190"/>
    <DiscreteKeyFrame KeyTime="0:0:1" Value="350"/>
  </DoubleAnimationUsingKeyFrames>
  <!-- Move down -->
  <DoubleAnimationUsingKeyFrames BeginTime="0:0:0:1" Duration="0:0:0:1">
    Storyboard.TargetName="btnMover"
    Storyboard.TargetProperty="(Canvas.Left)"
    Source="X"
    <PathGeometry Source="StaticResource pathMove"/>
  </DoubleAnimationUsingKeyFrames>
  <DoubleAnimationUsingKeyFrames BeginTime="0:0:0:1" Duration="0:0:0:1">
    Storyboard.TargetName="btnMover"
    Storyboard.TargetProperty="(Canvas.Top)"
    Source="Y"
    <PathGeometry Source="StaticResource pathMove"/>
  </DoubleAnimationUsingKeyFrames>
  <!-- Move Left -->
  <DoubleAnimationUsingKeyFrames BeginTime="0:0:0:2">
    Storyboard.TargetName="btnMover"
    Storyboard.TargetProperty="(Canvas.Left)"
    <DiscreteKeyFrame KeyTime="0:0:0" Value="190"/>
    <LinearKeyFrame KeyTime="0:0:1" Value="10"/>
  </DoubleAnimationUsingKeyFrames>
  <!-- Rotate right-side -->
  <DoubleAnimationUsingKeyFrames BeginTime="0:0:0:3" Duration="0:0:0:1">
    Storyboard.TargetName="btnMover"
    Storyboard.TargetProperty="RenderTransform.Angle"/>
  </DoubleAnimationUsingKeyFrames>
  <!-- Move Up -->
  <DoubleAnimationUsingKeyFrames BeginTime="0:0:0:4">
    Storyboard.TargetName="btnMover"
    Storyboard.TargetProperty="(Canvas.Top)"
    <LinearKeyFrame KeyTime="0:0:1" Value="10"/>
  </DoubleAnimationUsingKeyFrames>
</Storyboard>
```

# Special Cases

WPF provides the following animation types for most data types:

- Simple (linear)
- Key frame animation with linear frames
- Key frame animation with spine frames
- Key frame animation with discrete frames

It also provides path animation for the Double, Matrix, and Point. A few types do not provide the standard animation types, generally because these animation types don't make sense. For example, it't really make sense to animate a String using linear interpolation or a spine. How would you define a String halfway between "Time" and "banana"?

For the String, Boolean, and Char data types, WPF provides only discrete animation.

The AnimatedText example shows in Figure 14-10 demonstrates string animation. When you click on the Quote button, the program displays the quotation text a few letters at a time. After the quote appears, Winston Churchill gradually fades.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_291_0.png)

Figure 14-10

The following code shows the Storyboard for the AnimatedText program to display its quote and attribute:

```
<Storyboard x:Key="sbShowQuote">
  Display the quote
    <StringAnimationUsingKeyFrames
      <Storyboard.TargetProperty="Content">
        <DiscreteKeyFrame KeyTime="0:0:0.1" Value="A j"/>
        <DiscreteKeyFrame KeyTime="0:0:0.2" Value="A jok"/>
        <DiscreteKeyFrame KeyTime="0:0:0.3" Value="A joke i"/>
        <DiscreteKeyFrame KeyTime="0:0:0.4" Value="A joke is a"/>
        <DiscreteKeyFrame KeyTime="0:0:0.5" Value="A joke is a ve"/>
        <DiscreteKeyFrame KeyTime="0:0:0.6" Value="A joke is a very"/>
      </Storyboard.TargetProperty>
    </StringAnimationUsingKeyFrames>
  </Display>
  ...
  Other key frames omitted
  <DiscreteKeyFrame KeyTime="0:0:1.2" Value="A joke is a very serious thing"/>
</Storyboard>
```
