# Introduction to Programming and Problem-Solving Using Scala

![](bbox=[0.227, 0.068, 0.772, 0.229])

**FIGURE 12.7:** On the left you will see an example of Interpolator.EaseBoth. On the right you see an example of Interpolator.Linear.

+   - **targetFerate**: Double - Tells you the maximum frame rate that this animation is expected to be played.
- **totalDuration** - This ReadOnlyProperty[Duration] tells you how long the full animation to play, including any repeating.

The fact that animations take time to execute leads to several of the methods listed above working with the scalaf.util.Duration. Instances of this type represent time duration in milliseconds. You can make one by calling `new Duration(millis: Double)`. You can perform standard math operations and comparisons between Durations. There are also special values defined at Duration.Indefinite, Duration.One, Unknown, and Duration.Zero.

# 12.5.1 Transitions

The first subset of Animation that we want to consider is the Transition type. The Transition type has all members of Animation listed above, but adds ObjectProperty[Interpolator] called interpolator that governs the way in which the animation goes from beginning to end.

You can imagine an animation as taking time from 0.0 to 1.0 and the position in the animation going from 0.0 to 1. An Interpolator is a function that takes a fractional time and gives back a fractional position. The simplest approach to this gives back the same value that is passed in. This can look a bit unnatural for some actions as there are abrupt stops at the ends. For this reason, there are alternative functions as well as mechanisms that you can use to define your own interpolation. Here are the options defined in the Interpolator object.

+   - **Discrete** - Gives back 1.0 for the input 1.0 and 0.0 otherwise.
- **EaseBoth** - Slows the transition at the beginning and the end is linear between.
- **EaseIn** - Slows the transition at the beginning, but is linear in the middle and end.
- **EaseOut** - Slows the transition at the end, but is linear at the beginning and middle.
- **Linear** - This is the basic interpolator that gives back the input value.
- **Spline** (x1:Double, y1:Double, x2:Double, y2:Double): Interpolator - This creates a cubic function that uses the two specified control points.