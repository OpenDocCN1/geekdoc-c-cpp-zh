
## Table 12.35: Classes of the System.Windows.Media.Animation Namespace

| Class | Description |
|---|---|
| ColorKeyFrame | Defines an animation segment with its own target value and interpolation method for a ColorAnimationUsingKeyFrames object |
| ColorKeyFrameCollection | Represents a collection of ColorKeyFrame objects |
| ControllableStoryboardAction | Manipulates a Storyboard timeline that has been applied by a BeginStoryboard action |
| DecimalAnimation | Animates the value of a Decimal property between two target values using linear interpolation over a specified duration |
| DecimalAnimationBase | Animates a Decimal value |
| DecimalAnimationUsingKeyFrames | Animates the value of a Decimal property along a set of KeyFrames objects |
| DecimalKeyFrame | Defines an animation segment with its own target value and interpolation method for a DecimalAnimationUsingKeyFrames objects |
| DecimalKeyFrameCollection | Represents a collection of DecimalKeyFrame objects |
| DiscreteBooleanKeyFrame | Animates from the Boolean value of the previous key frame to its own value using discrete interpolation |
| DiscreteByteKeyFrame | Animates from the Byte value of the previous key frame to its own value using discrete interpolation |
| DiscreteCharKeyFrame | Animates from the Char value of the previous key frame to its own value using discrete interpolation |
| DiscreteColorKeyFrame | Animates from the Color value of the previous key frame to its own value using discrete interpolation |
| DiscreteDecimalKeyFrame | Animates from the Decimal value of the previous key frame to its own value using discrete interpolation |
| DiscreteDoubleKeyFrame | Animates from the Double value of the previous key frame to its own value using discrete interpolation |
| DiscreteInt16KeyFrame | Animates from the Int16 value of the previous key frame to its own value using discrete interpolation |
| DiscreteInt32KeyFrame | Animates from the Int32 value of the previous key frame to its own value using discrete interpolation |
| DiscreteInt64KeyFrame | Animates from the Int64 value of the previous key frame to its own value using discrete interpolation |
| DiscreteMatrixKeyFrame | Animates from the Matrix value of the previous key frame to its own value using discrete interpolation |
| DiscreteObjectKeyFrame | Animates from the Object value of the previous key frame to its own value using discrete interpolation |
| DiscretePoint3DKeyFrame | Animates from the Point3D value of the previous key frame to its own value using discrete interpolation |
| DiscretePointKeyFrame | Animates from the Point value of the previous key frame to its own value using discrete interpolation |
| DiscreteQuaternionKeyFrame | Animates from the Quaternion value of the previous key frame to its own value using discrete interpolation |
| DiscreteRectKeyFrame | Animates from the Rect value of the previous key frame to its own value using discrete interpolation |
| DiscreteRotation3DKeyFrame | Animates from the Rotation3D value of the previous key frame to its own value using discrete interpolation |
| DiscreteSingleKeyFrame | Animates from the Single value of the previous key frame to its own value using discrete interpolation |
| DiscreteSizeKeyFrame | Animates from the Size value of the previous key frame to its own value using discrete interpolation |
| DiscreteStringKeyFrame | Animates from the String value of the previous key frame to its own value using discrete interpolation |
| DiscreteThicknessKeyFrame | Animates from the Thickness value of the previous key frame to its own value using discrete interpolation |
| DiscreteVector3DKeyFrame | Animates from the Vector3D value of the previous key frame to its own value using discrete interpolation |
| DiscreteVectorKeyFrame | Animates from the Vector value of the previous key frame to its own value using discrete interpolation |
| DoubleAnimation | Animates the value of a Double property between two target values using linear interpolation over a specified duration |
| DoubleAnimationBase | Animates a Double value |
| DoubleAnimationUsingKeyFrames | Animates the value of a Double property along a set of KeyFrames objects |
| DoubleAnimationUsingPath | Animates the value of a Double property between two or more target values using a PathGeometry object to specify those values |
| DoubleKeyFrame | Defines an animation segment with its own target value and interpolation method for a DoubleAnimationUsingKeyFrames object |
| DoubleKeyFrameCollection | Represents a collection of DoubleKeyFrame objects |
| KeySpline | Defines animation progress by using a spline key frame |
| ParallelTimeline | Defines a segment of time that may contain child Timeline objects |
| PauseStoryboard | Pauses a Storyboard timeline |
| PointAnimation | Animates the value of a Point property between two target values using linear interpolation over a specified duration |
| RectAnimation | Animates the value of a Rect property between two target values using linear interpolation |
| RemoveStoryboard | Removes a Storyboard timeline |
| RepeatBehaviorConverter | Converts instances of RepeatBehavior class to and from other data types |
| ResumeStoryboard | Resumes a paused Storyboard timeline |
| SeekStoryboard | Provides functionality for seeking a specified time within the active period of a Storyboard timeline |
| SetStoryboardSpeedRatio | Changes the speed of a Storyboard timeline |
| SingleAnimation | Animates the value of a Single property between two target values using linear interpolation over a specified duration |
| SizeAnimation | Animates the value of a Size property between two target values using linear interpolation over a specified duration |
| SkipStoryboardToFill | Advances a Storyboard timeline to the end of its fill period |
| StopStoryboard | Stops a Storyboard timeline |
| Storyboard | Provides object and property targeting information for its child animations |
| ThicknessAnimation | Animates the value of a Thickness property between two target values using linear interpolation over a specified duration |
| Timeline | Defines a segment of time |
| TimelineCollection | Represents a collection of Timeline objects |
| TimelineGroup | Represents a Timeline that may contain a collection of child Timeline objects |

## Essentials of Animation

In the preceding section, you learned about the different types of animation available in WPF and the different animation classes. To make the animation actually happen in WPF, there are some essentials of animation that you should keep in mind. These essentials include the Timeline class, the Storyboard class, the EventTrigger class, and the KeyFrames collection. Let's first discuss the Timeline class.

### The Timeline Class

A timeline represents a stretch of time. It usually describes one or more events that happen during that stretch of time. Timelines of all kinds have a start time and duration. It provides the properties that enable you to specify the length of the segment, when it should start, how many times it should repeat, and how fast the time progresses in the segment. The timeline in animation is represented by the Timeline class. There are different types of specialized timelines:

- The AnimationTimeline class—Generates output values based on the timing progress. It defines a segment of time over which the output values are produced. The values are used to animate the target property.
- The MediaTimeline class—Represents a Timeline object that provides control over media timing in the same way that animation timeline objects control animations. For example, you can specify the Duration and BeginTime properties to specify when the media begins and how long it plays.
- The ParallelTimeline class—Represents a segment of time that contains other child Timeline objects. These child elements are active according to their respective BeginTime properties. You can also make the child elements run in parallel with each other. The ParallelTimeline class has its own BeginTime property, and so all the child timeline BeginTime values are relative to the parent ParallelTimeline values for the BeginTime property.
- The Storyboard class—Represents a special type of the ParallelTimeline class that provides object and property targeting information for the timelines it contains. A Storyboard object can contain any type of timeline, including other container timelines and animation.

The noteworthy properties of the Timeline class are listed in Table 12.36:

## Table 12.36: Properties of the Timeline Class

| Property | Description |
|---|---|
| AccelerationRatio | Gets or sets a value specifying the percentage of the timeline's duration spent accelerating the passage of time from zero to its maximum rate |
| AutoReverse | Gets or sets a value that indicates whether the timeline plays in reverse after it completes a forward iteration |
| BeginTime | Gets or sets the time at which timeline should begin |
| CanFreeze | Retrieves a value that indicates whether the object can be made unmodifiable |
