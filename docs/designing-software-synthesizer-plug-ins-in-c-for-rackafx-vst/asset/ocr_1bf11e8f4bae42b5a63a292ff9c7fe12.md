# Adding the joystick control to your plug-in is three part process.

```
@interface WPTrackPad : NSControl
    // --- these are raw positions -1 to +1 ordinarily
    CGSize currentPosition; // current position
    CGSize mouseDownPosition; // position of knob when mousedown

    // --- mouse down location
    CGSize mouseDownLocation;

    // --- mouse point location
    NSPoint mousePoint;

    // --- default is 1.0
    float knobScale;

    // --- get the XY coordinates of mouse
    -(void)getControlCoords:(float*)x Y:(float*)y;
```

Remember that, because of the fact namespace in Cocoa, you need to rename the control and its custom cell for each new synth project, you should be used to this by now.

# Part One: Declare the Controls

As usual, this requires index values that we place in the control enumeration in SynthParamLimits.h:

VECTORJOYSTICK_X
VECTORJOYSTICK_Y

# Part Two: View Object

In the view object, #include the proper files and an IBOutlet for the new object; here the view is VectorSynthView. You also need to declare a message handler for the control named WPTrackPadChanged (my choice, you are free to name the function whatever you wish).

Next, you implement the message handler in the .m file in the usual way that you implement the knob

```
#import "WPTrackPad.h"

@interface VectorSynthView : NSView
```