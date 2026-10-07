The AccDecelRatios example program shown in Figure 14-5 demonstrates the AccelerationRatio and DecelerationRatio properties. When you click on the Go button, the program starts a storyboard that moves the two Image across the window. The first Image moves at a constant speed throughout the animation. The second Image has AccelerationRatio = 0.4 and DecelerationRatio = 0.2, so it takes a while to get up speed and then slows down as it approaches its destination. (I guess that he is a slower and pulls up lame at the end.)

![](bbox=[0.4052, 0.1035, 0.8748, 0.2235])

Figure 14-5

The following code shows the storyboard used by the AccDecelRatios program:

```
<Storyboard>
  <DoubleAnimation Duration="0:0:02" From="5" To="500"
    Storyboard.TargetName="img1"
    Storyboard.TargetProperty="Canvas.Left"/>
  <DoubleAnimation Duration="0:0:02" From="5" To="500"
    AccelerationRatio="0.4"
    DecelerationRatio="0.2"
    Storyboard.TargetName="img2"
    Storyboard.TargetProperty="Canvas.Left"/>
</Storyboard>
```

The animation classes add a few extra properties that they do not inherit from the Storyboard class. Most important of these are From, To and By:

+   - From Indicates the value at which the animation should begin. In the previous code, the DoubleAnimations have From = 5, so the Canvas.Left properties animate start at the value 5.
- To Indicates the animation's final property value. In the previous example, the Canvas .Left ranges from 5 to 500.
- By Indicates The animation ends at this value plus the property's original value. For example, if From is 10 and By is 100, then the final value is 10 + 100 = 110.

If you don't specify a value for the From property, the animation begins with the property's current value. That may be the control's original property value, or it may be the result of a previous animation.

In fact, if an animation is under way but does not finish when the new animation starts, the current value may be somewhere in the middle of the previous animation.