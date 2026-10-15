
an animation that produces the Double value. As there are number of different property types, there are several animation classes in the System.Windows.Media.Animation namespace. All of them follow a strict naming convention; and therefore, can be categorized in three parts, given as follows:

- Basic animation
- Key-frame animation
- Path animation

Let's discuss these in detail.

## Basic Animation

The basic animation in WPF creates a transition between two target values. It animates between a starting and destination value. The From property of the animation defines the starting point of the animation. The ending value is defined by setting the To property of the animation. The By property of the animation specifies an offset value. You can use the From, To, and By properties that can be used together or separately to determine an animation target value. The resulting behavior of the From, To, and By properties are listed in Table 12.33:

Table 12.33: Resulting Behavior of the Properties
| Property | Resulting Behavior |
|---|---|
| From | Represents the animation progress from the value specified by the From property to the base value of the property being animated or to a previous animation's output value |
| From and To | Represents these properties together for the animation to progress from the value specified by the From property to the value specified by the To property |
| From and By | Represents these properties together for the animation to progress from the value specified by the From property to the value specified by the sum of the From and By properties |
| To | Represents the animation progress from the animated property's base value or a previous animation's output value to the value specified by the To property |
| By | Represents the animation progress from the base value of the property being animated, or a previous animation's output value to the sum of that value and the value specified by the By property |

> NOTE
> if you set the To and By properties in the same animation, the .NET Framework 4.0 ignores the task performed by the By property.

## Key-Frame Animation

The key-frame animation is a better choice in animations in comparison to the basic animation. In the key-frame animation, you can animate the value of a target property and can specify two or more target values. The target value is described using the KeyFrames collection. To specify the animation target value, you need to create KeyFrames objects and add them to the animation KeyFrames collection. To specify animation with the key-frame animation, you need to follow a particular sequence:

- Declare an animation and specify its duration
- Create a KeyFrames object of an appropriate type, and set its value and KeyTime structure, corresponding to each target value, and then add it to the KeyFrames collection
- Associate the animation with a property to complete the animation process

There are different key-frame animation classes for different property types which are listed in Table 12.34:

Table 12.34: Key-Frame Animation Classes
| Property Type | Animation Classes |
|---|---|
| Boolean | BooleanAnimationUsingKeyFrames |
| Byte | ByteAnimationUsingKeyFrames |
| Color | ColorAnimationUsingKeyFrames |
| Decimal | DecimalAnimationUsingKeyFrames |
| Double | DoubleAnimationUsingKeyFrames |
| Int16 | Int16AnimationUsingKeyFrames |
| Int32 | Int32AnimationUsingKeyFrames |
| Int64 | Int64AnimationUsingKeyFrames |
| Matrix | MatrixAnimationUsingKeyFrames |
| Object | ObjectAnimationUsingKeyFrames |
| Point | PointAnimationUsingKeyFrames |
| Quaternion | QuaternionAnimationUsingKeyFrames |
| Rect | RectAnimationUsingKeyFrames |
| Rotation3D | Rotation3DAnimationUsingKeyFrames |
| Single | SingleAnimationUsingKeyFrames |
| String | StringAnimationUsingKeyFrames |
| Size | SizeAnimationUsingKeyFrames |
| Thickness | ThicknessAnimationUsingKeyFrames |
| Vector3D | Vector3DAnimationUsingKeyFrames |
| Vector | VectorAnimationUsingKeyFrames |

The basic purpose of key-frame animation is to specify the Value and KeyTime properties. The Value property specifies the target value for the KeyFrames collection; while the KeyTime property specifies the time when the Value property of the KeyFrames collection is met. When the key-frame animation begins, it iterates through its key frames in the order defined by their KeyTime properties. If there is no key frame at time 0, the animation creates a transition between the current value of target property and the Value of the first key frame.

> NOTE
> If you set the animation duration to Automatic or Equal to the time of the last key frame, the animation ends.

You learn more about key-frame animation and its practical application in the Immediate Solutions section of the chapter.

## Path Animation

A path animation is implemented by using a geometric path to generate output values. It is used to move or rotate objects on a complex path. A path based animation modifies a value to correspond with the shape that is described by a PathGeometry object. It is primarily useful for moving an element along a path. Path animation can be used to modify any property that has the right data type. It is most useful when animating position related properties. When you create a path animation, you do not supply the starting and ending values, but the PathGeometry class. The collection of lines and curves that constitute a path, determines the value that is used for the animated property.

> NOTE
> A path based animation, always runs at a continuous speed. The total length of a path and the duration that you have specified, determines the speed.

## Animation Classes

You have learned about the different types of animations in WPF, such as basic animation, key-frame animation, and path animation. Although, WPF uses these three types of animations currently, you can create more animation classes that modify values using a completely different approach. These different types of animation are contained in the System.Windows.Media.Animation namespace. Broadly speaking, there are two kinds of animation:

- Those that vary a property incrementally between the starting and finishing values
- Those that abruptly change a property from one value to another

The different types of animation classes available in the System.Windows.Media.Animation namespace are listed in Table 12.35:

Table 12.35: Classes of the System.Windows.Media.Animation Namespace

| Class | Description |
|---|---|
| Animatable | Provides animation support |
| AnimationClock | Maintains the run-time state of an AnimationTimeline object and processes its output values |
| AnimationException | Throws when an error occurs while animating a property |
| AnimationTimeline | Defines a segment of time over which output values are produced |
| BeginStoryboard | Begins a Storyboard timeline and distributes its animations to their targeted objects and properties |
| BooleanAnimationUsingKeyFrames | Animates the value of a property that takes a Boolean value along a set of KeyFrames objects over a specified duration |
| BooleanKeyFrame | Defines a segment with its own target value and interpolation method for a BooleanAnimationUsingKeyFrames object |
| BooleanKeyFrameCollection | Represents a collection of BooleanKeyFrame objects |
| ByteAnimation | Animates the value of a Byte property between two target values using linear interpolation over a specified duration |
| ByteAnimationUsingKeyFrames | Animates the value of a Byte property along a set of KeyFrames objects |
| ByteKeyFrame | Defines an animation segment with its own target value and interpolation method for a ByteAnimationUsingKeyFrames object |
| ByteKeyFrameCollection | Represents a collection of ByteKeyFrame objects |
| CharAnimationUsingKeyFrames | Animates the value of a Char property along a set of KeyFrames objects over a specified duration |
| CharKeyFrame | Defines an animation segment with its own target value and interpolation method for a CharAnimationUsingKeyFrames object |
| CharKeyFrameCollection | Represents a collection of CharKeyFrame objects |
| Clock | Maintains run-time timing state for a Timeline object |
| ClockCollection | Represents an ordered collection of Clock objects |
| ClockController | Controls a Clock interactively |
| ColorAnimation | Animates the value of a Color property between two target values using linear interpolation over a specified duration |
| ColorAnimationBase | Animates a Color value |
| ColorAnimationUsingKeyFrames | Animates the value of a Color property along a set of KeyFrames objects over a specified duration |
