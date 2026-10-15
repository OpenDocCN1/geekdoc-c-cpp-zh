an animation that produces the Double value. As there are number of different property types, there are several animation classes in the System.Windows.Media.Animation namespace. All of them follow a strict naming convention; and therefore, can be categorized in three parts, given as follows:

+   - Basic animation
+   - Key-frame animation
+   - Path animation

Let's discuss these in detail.

# Basic Animation

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

# Key-Frame Animation

The key-frame animation is a better choice in animations in comparison to the basic animation. In the key-frame animation, you can animate the value of a target property and can specify two or more target values. The target value is described using the KeyFrames collection. To specify the animation target value, you need to create KeyFrames objects and add them to the animation KeyFrames collection. To specify animation with the key-frame animation, you need to follow a particular sequence:

+   - Declare an animation and specify its duration
+   - Create a KeyFrames object of an appropriate type, and set its value and KeyTime structure, corresponding to each target value, and then add it to the KeyFrames collection
+   - Associate the animation with a property to complete the animation process

There are different key-frame animation classes for different property types which are listed in Table 12.34:

Table 12.34: Key-Frame Animation Classes
| Property Type | Animation Classes |
|---|---|
| Boolean | BooleanAnimationUsingKeyFrames |
| Byte | ByteAnimationUsingKeyFrames |
| Color | ColorAnimationUsingKeyFrames |