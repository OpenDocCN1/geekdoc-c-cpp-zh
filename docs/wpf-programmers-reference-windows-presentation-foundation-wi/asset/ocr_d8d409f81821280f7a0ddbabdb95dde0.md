If you use a spine key, the property follows a path similar to the orange spine shown in Figure 14-7. In this example, on the left side of the graph, the value starts by changing relatively little as time increases; in the middle of the graph, the value changes quickly; and near the right side of the graph, the value decreases again. The result is that the value starts moving slowly, picks up the pace, and then slows down before reaching its final value.

You use the KeySpine attribute to specify the control points for a key frame with splines. This attribute should contain two points that give the control point coordinates in a normalized system (0 ≤ X ≤ 1, and 0 ≤ Y ≤ 1).

The RovingButtonWithSplines example uses the following code to make its Button follow the rectangular path followed by the RovingButton and RovingButtonWithKeyFrames. The programs are the same, but the speed with which the Button moves is different. In the earlier programs, the Button moves at a constant speed across each of the Rectangle's sides. In this, it's actually a pretty nice effect. Download the program from the book's website and see it for yourself.

![](bbox=[0.04, 0.41, 0.133, 0.477])

```
<Storyboard X:Key="moveButton" RepeatBehavior="Forever">
DoubleAnimationUsingKeyFrames
Storyboard.TargetName="btnM"
Storyboard.TargetProperty="Canvas.Left">
<SpineDoubleKeyFrame Value="370"
KeyTime="0:0:1.5" KeySpine="0.5,0.5,0.5,1//>
<SpineDoubleKeyFrame Value="370" KeyTime="0:0:2.5">
<SpineDoubleKeyFrame Value="10" KeyTime="0:0:4">
<SpineDoubleKeyFrame Value="10" KeyTime="0:0:5">
<SpineDoubleKeyFrame Value="160" KeyTime="0:0:2.5">
<SpineDoubleKeyFrame Value="160" KeySpineine="0.5,0.5,0.5,1//>
</DoubleAnimationUsingKeyFrames>
DoubleAnimationUsingKeyFrames
Storyboard.TargetName="btnM"
Storyboard.TargetProperty="Canvas.Top">
<SpineDoubleKeyFrame Value="10" KeyTime="0:0:1.5">
<SpineDoubleKeyFrame Value="160" KeyTime="0:0:2.5">
<SpineDoubleKeyFrame Value="160" KeyTime="0:0:4">
<SpineDoubleKeyFrame Value="160" KeyTime="0:0:5">
</DoubleAnimationUsingKeyFrames>
</Storyboard>
```

RovingButtonWithSplines

# Discrete Key Frames

Linear and spine key frames move a property continuously from one value to another. A discrete key frame makes a property suddenly jump from one value to another.