| Class | Description |
|---|---|
| `CAKeyframeAnimation` | An alternative to `CABasicAnimation` that animates the target value with a sequence of discrete steps called keyframes, defined by an array of points or a path. Includes an option to pace animations and force a fixed duration on the sequence of steps. |
| `CAGroupAnimation` | A wrapper for an array of animation objects that can be used together. |
| `CAMediaTiming` | A protocol implemented by all Core Animation objects that makes it possible to repeat animations, delay them, and apply autoreverse so that they run forward and then backward. Also defines how the final property value is defined after the animation. |
| `CAMediaTimingFunction` | Not a subclass of `CAMediaTiming`. This is a separate class that defines the animation timing curve with either one of four presets or a custom timing Bezier curve. The curve is an object that plugs into the `timingFunction` property. |

You can simplify this nest of classes with the following hints:

+   - You’ll rarely, if ever, use `CAAnimation` and `CAPropertyAnimation` directly.
+   - For a simple from-to animation, create a `CABasicAnimation`.
+   - For a complex path animation that follows a list of defined points, create a `CAKeyframeAnimation`.
+   - Optionally, define an instance of `CAMediaTimingFunction` to control time development. For most animations, the preset timing functions create a good result. Use a custom function for special effects.
+   - Optionally, set up repeat and autoreverse effects with an instance of `CAMediaTiming`.
+   - Plug your chosen timing function and timing settings back into your animation object.
+   - Optionally define a delegate and implement the `animationDidStart:` and `animationDidEnd:` methods. For example, you can use `animationDidEnd:` to run another animation object, creating complex chained animation sequences; or it can just log a message for debugging.
+   - To replace the default animator, bundle the new animation object into a dictionary and assign the dictionary to the target object’s `animations` property.

This looks like a lot of work, but most of it is optional. Some sample code that adds a timing function to the follow-bottom example follows:

```
```objective-c
- (void) awakeFromNib {
    oldPosition = theButton.frame.origin;
    //Create a basic animation object
    moveAnimation = [CABasicAnimation animation];
    moveAnimation.duration = 2.0;
    //Preset ease-in/out curve
```
```