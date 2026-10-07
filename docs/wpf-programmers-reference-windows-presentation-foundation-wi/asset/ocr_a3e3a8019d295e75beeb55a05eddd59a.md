The RovingButtonDiscrete example uses the following code to animate this Button:

```
<Storyboard x="sbButton" RepeatBehavior="Forever">
  <DoubleAnimationUsingKeyFrames>
    <Storyboard.TargetName="move" Target="Canvas.Left">
      <DiscreteKeyFrame Value="130" KeyTime="0:0:0.5/">
      <DiscreteKeyFrame Value="250" KeyTime="0:0:1.0/">
      <DiscreteKeyFrame Value="370" KeyTime="0:0:1.5/">
      <DiscreteKeyFrame Value="370" KeyTime="0:0:2.5/">
      <DiscreteKeyFrame Value="250" KeyTime="0:0:3.5/">
      <DiscreteKeyFrame Value="130" KeyTime="0:0:4.0/">
    </Storyboard.TargetName>
  </DoubleAnimationUsingKeyFrames>
  <DoubleAnimationUsingKeyFrames>
    <Storyboard.TargetName="move" Target="Canvas.Top">
      <DiscreteKeyFrame Value="85" KeyTime="0:0:0.2/">
      <DiscreteKeyFrame Value="160" KeyTime="0:0:2.5/">
      <DiscreteKeyFrame Value="85" KeyTime="0:0:4.5/">
      <DiscreteKeyFrame Value="10" KeyTime="0:0:5.0/">
  </DoubleAnimationUsingKeyFrames>
</Storyboard>
```

The example moves the Button in a rectangular path as much as the previous examples, but the Button moves in discrete jumps rather than smooth movements.

Because discrete frames don't generate any intermediate values, the code must list every value that you want to property.

# Path Animations

Path animations property values follow the coordinates or angle of a path. For example, you can use a path animation to move a control along the border of an ellipse or a series of curves.

The RovingButtonWithPath example program shown in Figure 14-8 moves a Button along the path shown in black. As it moves, the Button rotates to match the curve's angle at that point.

The RovingButtonWithPath program uses the following code to animate its Button:

```
<PathGeometry x="pathMove"
  Figures="M10 85
  A 100,70 0 1 10 210,85
  A 100,70 0 1 0 10,150>
```

![](bbox=[0.531, 0.638, 0.929, 0.818])

Figure 14-8