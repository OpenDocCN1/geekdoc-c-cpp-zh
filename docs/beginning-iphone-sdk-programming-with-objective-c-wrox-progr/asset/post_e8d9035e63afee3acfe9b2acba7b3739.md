
2. Press Command-R to test the application on the iPhone Simulator.
3. In the iPhone Simulator, press the Option key, and two circles should appear (see Figure 14-4). Clicking the screen simulates two fingers touching the screen of the device. Click and move the mouse to simulate pinching the screen.
4. Open the Debugger Console window (press Command-Shift-R) and observe the output as you Option-click the screen of the iPhone Simulator:

![](img/16991b58db5894715c4a443315e06a22_356_0.png)

FIGURE 14-4

```text
2009-08-25 10:01:15.510 MultiTouch[2230:207] Touch1: 107, 201
2009-08-25 10:01:15.511 MultiTouch[2230:207] Touch2: 213, 239
2009-08-25 10:01:15.758 MultiTouch[2230:207] Touch1: 105, 201
2009-08-25 10:01:15.759 MultiTouch[2230:207] Touch2: 215, 239
2009-08-25 10:01:15.918 MultiTouch[2230:207] Touch1: 105, 239
2009-08-25 10:01:15.919 MultiTouch[2230:207] Touch2: 105, 201
2009-08-25 10:01:16.054 MultiTouch[2230:207] Touch1: 105, 201
2009-08-25 10:01:16.055 MultiTouch[2230:207] Touch2: 215, 239
2009-08-25 10:01:16.238 MultiTouch[2230:207] Touch1: 105, 201
2009-08-25 10:01:16.239 MultiTouch[2230:207] Touch2: 215, 239
```

> **NOTE** Using the iPhone Simulator, the coordinates for the two touches are often interchanged as you Option-click the same spot on the screen of the iPhone Simulator.

## How It Works

As you do when detecting for single-touch, you check for multi-touches in the touchesBegan:withEvent: event. Rather than receive information about the first touch, you now obtain information for both the first and second touch:

```objc
//---get info of first touch---
UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];

//---get info of second touch---
UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];
```

> **NOTE** Basically, to detect more than two touches, you simply extend the preceding code by getting information about the third touch, fourth touch, and so on.

To get the coordinates (represented as a CGPoint structure) of each touch, you use the locationInView: method of the UITouch class and pass it the view that it is currently in:

```objc
//---get the points touched---
CGPoint touch1PT = [touch1 locationInView:[self view]];
CGPoint touch2PT = [touch2 locationInView:[self view]];
```

The coordinates returned by the locationInView: method are relative to the view specified. In the preceding snippet, the coordinates displayed are relative to the main View window.

The x and y coordinates of a CGPoint structure are represented using the CGFloat type, so you need to use the %f format specifier when printing them in the Debugger Console window:

```objc
NSLog(@"Touch1: %.0f, %.0f", touch1PT.x, touch1PT.y);
NSLog(@"Touch2: %.0f, %.0f", touch2PT.x, touch2PT.y);
```

One important thing to understand is that the coordinates values displayed are relative to a specified view. Figure 14-5 shows that the top-left corner has a coordinate of (0,-20) and the bottom-right corner a coordinate of (320,460) when you reference against the main View window:

```objc
//---get the points touched---
CGPoint touch1PT = [touch1 locationInView:[self view]];
CGPoint touch2PT = [touch2 locationInView:[self view]];
```

![](img/16991b58db5894715c4a443315e06a22_357_0.png)

FIGURE 14-5

Suppose the size of the image view was shrunk to the size shown in Figure 14-6 (remember that it is currently filling up the entire screen). If you referenced that against the imageView view, the (0,0) position would then start at the top-left corner of the image view. All other points to the top left of the (0,0) point would have negative x- and y-coordinates:

```objc
//---get the points touched---
CGPoint touch1PT = [touch1 locationInView:imageView];
CGPoint touch2PT = [touch2 locationInView:imageView];
```

![](img/16991b58db5894715c4a443315e06a22_358_0.png)

FIGURE 14-6

## Implementing the Pinch Gesture

Now that you know the technique for detecting multi-touches in your application, you can write some cool applications that make use of multi-touches. A cool example would be to implement the famous iPhone pinch gesture that differentiates it from the competition.

Using the pinch gesture, you place two fingers on the screen and pinch by moving the two fingers closer to each other. This often translates to a zoom-out action when applying this gesture to, say, a photo that you are viewing, or to a Web page in Mobile Safari. When you move the two fingers apart, you zoom in on a photo or Web page.

To use the pinch gesture on an image, you actually need to enlarge the image first. This is because the image can only be resized if its display mode is set to UIViewContentModeScaleAspectFit. Hence, in this case, you need to single-tap on the image (which actually sets the image mode to UIViewContentModeScaleAspectFit) before you can try the pinching effect.

In the following Try It Out, you learn how to implement the pinch gesture to zoom the image in and out in the image view.

## TRY IT OUT Zooming In and Out

1. Using the same project created earlier, add the following statement that appears in bold to the MultiTouchViewController.h file:

```objc
#import <UIKit/UIKit.h>

@interface MultiTouchViewController : UIViewController {
    IBOutlet UIImageView *imageView;
}

@property (nonatomic, retain) UIImageView *imageView;

-(CGFloat) distanceBetweenTwoPoints: (CGPoint)fromPoint toPoint: (CGPoint)toPoint;

@end
```

2. In the MultiTouchViewController.m file, implement the distanceBetweenTwoPoints:toPoint: and touchesMoved:withEvent: methods and add the statements that appear in bold to the touchesBegan:withEvent: method:

```objc
#import "MultiTouchViewController.h"

@implementation MultiTouchViewController

@synthesize imageView;

CGFloat originalDistance;

-(CGFloat) distanceBetweenTwoPoints:(CGPoint)fromPoint toPoint:(CGPoint)toPoint {
    float lengthX = fromPoint.x - toPoint.x;
    float lengthY = fromPoint.y - toPoint.y;
    return sqrt((lengthX * lengthX) + (lengthY * lengthY));
}

-(void) touchesBegan: (NSSet *) touches withEvent: (UIEvent *) event {
    //---get all touches on the screen---
    NSSet *allTouches = [event allTouches];

    //---compare the number of touches on the screen---
    switch ([allTouches count])
    {
        //---single touch---
        case 1:
            //---get info of the touch---
            UITouch *touch = [[allTouches allObjects] objectAtIndex:0];

            //---compare the touches---
            switch ([touch tapCount])
            {
                //---single tap---
                case 1: {
                    imageView.contentMode = UIViewContentModeScaleAspectFit;
                } break;

                case 2: {
                    imageView.contentMode = UIViewContentModeCenter;
                } break;
            } break;

        //---double-touch---
        case 2: {
            //---get info of first touch---
            UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];
            //---get info of second touch---
            UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];

            //---get the points touched---
            CGPoint touch1PT = [touch1 locationInView:[self view]];
            CGPoint touch2PT = [touch2 locationInView:[self view]];

            NSLog(@"Touch1: %.0f, %.0f", touch1PT.x, touch1PT.y);
            NSLog(@"Touch2: %.0f, %.0f", touch2PT.x, touch2PT.y);

            //---record the distance made by the two touches---
            originalDistance = [self distanceBetweenTwoPoints:touch1PT
                                toPoint: touch2PT];
        } break;
    }
}

//---fired when the user moved his finger(s) on the screen---
-(void) touchesMoved: (NSSet *) touches withEvent: (UIEvent *) event {

    //---get all touches on the screen---
    NSSet *allTouches = [event allTouches];

    //---compare the number of touches on the screen---
    switch ([allTouches count])
    {
        //---single touch---
        case 1: {
        } break;

        //---double-touch---
        case 2: {
            //---get info of first touch---
            UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];

            //---get info of second touch---
            UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];

            //---get the points touched---
```
