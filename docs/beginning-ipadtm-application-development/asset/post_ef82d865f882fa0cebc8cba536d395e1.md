
```objc
[imageView addGestureRecognizer:swipeLeftGesture];
[swipeLeftGesture release];
}
[super viewDidLoad];

//---handle swipe gesture---
-(IBAction) handleSwipeGesture:(UIGestureRecognizer *) sender {

    UISwipeGestureRecognizerDirection direction =
        [(UISwipeGestureRecognizer *) sender direction];

    switch (direction) {
        case UISwipeGestureRecognizerDirectionUp:
            NSLog(@"up");
            break;
        case UISwipeGestureRecognizerDirectionDown:
            NSLog(@"down");
            break;
        case UISwipeGestureRecognizerDirectionLeft:
            imageIndex++;
            break;
        case UISwipeGestureRecognizerDirectionRight:
            imageIndex--;
            break;
        default:
            break;
    }

    imageIndex = (imageIndex < 0) ? ([images count] - 1) : imageIndex % [images count];
    imageView.image = [UIImage imageNamed:[images objectAtIndex:imageIndex]];
}
-(void)dealloc {
    [images release];
    [imageView release];
    [super dealloc];
}
```

- 3. Test the application on the iPhone Simulator by pressing Command-R.
- 4. Click the ImageView and drag the mouse from left to right and then from right to left. The ImageView changes its image as you swipe it with your mouse.

## How It Works

You first instantiate the images NSArray object with the names of the three images:

```objc
//---swipe gesture---
images = [[NSArray alloc] initWithObjects:@"architecture.jpg",
    @"Buildings.jpeg",
    @"Bridge.jpeg", nil];
```

> NOTE Remember to comment out the statements for the pan gesture recognizer. The swipe gesture recognizer will not work with the pan gesture recognizer.

## Long Press

Use the long press gesture recognizer to detect if the user is touching on a view and then holding onto it. A very common use of the long press gesture is when you want to save an image in the mobile Safari Web browser. When you long press on an image, an action sheet pops up, allowing you to save or copy that image.

The following Try It Out shows you how to recognize for long press using the UILongPressGestureRecognizer.

### TRY IT OUT Recognizing Long Presses

- 1. Using the same project created in the previous Try It Out, edit the GesturesViewController.m by adding the following bold statements:

```objc
- (void)viewDidLoad {

    //---tap gesture---
    UITapGestureRecognizer *tapGesture =
    [[UITapGestureRecognizer alloc]
        initWithTarget:self
        action:@selector(handleTapGesture:)];

    tapGesture.numberOfTapsRequired = 2;
    [self.imageView addGestureRecognizer:tapGesture];
    [tapGesture release];

    //---pinch gesture---
    UIPinchGestureRecognizer *pinchGesture =
    [[UIPinchGestureRecognizer alloc]
        initWithTarget:self
        action:@selector(handlePinchGesture:)];

    [imageView addGestureRecognizer:pinchGesture];
    [pinchGesture release];

    //---rotate gesture---
    UIRotationGestureRecognizer *rotateGesture =
    [[UIRotationGestureRecognizer alloc]
        initWithTarget:self
        action:@selector(handleRotateGesture:)];

    [imageView addGestureRecognizer:rotateGesture];
    [rotateGesture release];

    //---pan gesture---
    UIPanGestureRecognizer *panGesture =
        [[UIPanGestureRecognizer alloc]
            initWithTarget:self
            action:@selector(handlePanGesture:)];
    //---comment this out---
    //[imageView addGestureRecognizer:panGesture];
    [panGesture release];

    //---swipe gesture---
    images = [[NSArray alloc] initWithObjects:@"architecture.jpg",
                         @"Buildings.jpeg",
                         @"Bridge.jpeg", nil];

    //---right swipe (default)---
    UISwipeGestureRecognizer *swipeGesture =
        [[UISwipeGestureRecognizer alloc]
            initWithTarget:self
            action:@selector(handleSwipeGesture:)];
    [imageView addGestureRecognizer:swipeGesture];
    [swipeGesture release];

    //---left swipe---
    UISwipeGestureRecognizer *swipeLeftGesture =
        [[UISwipeGestureRecognizer alloc]
            initWithTarget:self
            action:@selector(handleSwipeGesture:)];
    swipeLeftGesture.direction = UISwipeGestureRecognizerDirectionLeft;
    [imageView addGestureRecognizer:swipeLeftGesture];
    [swipeLeftGesture release];

    //---long press gesture---
    UILongPressGestureRecognizer *longpressGesture =
        [[UILongPressGestureRecognizer alloc]
            initWithTarget:self
            action:@selector(handleLongpressGesture:)];
    longpressGesture.minimumPressDuration = 1;
    longpressGesture.allowableMovement = 15;
    longpressGesture.numberOfTouchesRequired = 1;
    [imageView addGestureRecognizer:longpressGesture];
    [longpressGesture release];
}

//---handle long press gesture---
-(IBAction) handleLongpressGesture:(UIGestureRecognizer *) sender {
    UIActionSheet *actionSheet = [[UIActionSheet alloc]
```

To detect touches on the screen of the iPad, you need to acquaint yourself with a few events that handle the detection of touches. Through these events, you will know whether the user has single-tapped, double-tapped, or moved his fingers on your application and react accordingly. These events are:

- touchesBegan:withEvent: — Fires when one or more fingers touch down in a view or window
- touchesMoved:withEvent: — Fires when one or more fingers move within a view or window
- touchesEnded:withEvent: — Fires when one or more fingers are raised from a view or window
- touchesCancelled:withEvent: — Fires when a system event (such as low-memory warning) cancels the touch event

These events are defined in the UIResponder class, which is the superclass of UIApplication, UIView, and its subclasses. Hence, you can implement event handlers for these events in your View Controller.

> NOTE The four touch events are the foundation events used by the gesture recognizers that you saw earlier in this chapter. To create your own custom gesture recognizers to recognize your own gestures (such as a figure-of-eight gesture), you need to implement your own event handlers for these four events. Creating your own custom gesture recognizer is beyond the scope of this book.

## Detecting Single Touch

Time to get the engine rolling! Make sure you download the code indicated here so you can work through the following Try It Out activity, in which you'll see how to detect when the user is tapping on the screen.

### TRY IT OUT Detecting for Taps

codefile MultiTouch.zip is available for download at Wrox.com

- 1. Using Xcode, create a new View-based Application project and name it MultiTouch.
- 2. Drag and drop an image into the Resources folder. Figure 12-10 shows an image named apple.jpeg located in the Resources folder.
- 3. Double-click the MultiTouchViewController.xib file to edit it in Interface Builder.
- 4. Populate the View window with an ImageView. Ensure that the ImageView covers the entire View window.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_364_0.png)

- 5. Select the ImageView and view its Attributes Inspector window (see Figure 12-11). Set its Image property to `apple.jpeg`.

- 6. In the `MultiTouchViewController.h` file, add the following statements that appear in bold:

```objc
#import <UIKit/UIKit.h>

@interface MultiTouchViewController : UIViewController {
    IBOutlet UIImageView *imageView;
}

@property (nonatomic, retain) UIImageView *imageView;

@end
```

- 7. Back in Interface Builder, Control-click and drag the File’s Owner item to the ImageView. Select `ImageView`.

- 8. In the `MultiTouchViewController.m` file, add the following statements that appear in bold:

```objc
#import "MultiTouchViewController.h"

@implementation MultiTouchViewController

@synthesize imageView;

//---fired when the user finger(s) touches the screen---
-(void)touchesBegan: (NSSet *) touches withEvent: (UIEvent *) event {

    //---get all touches on the screen---
    NSSet *allTouches = [event allTouches];

    //---compare the number of touches on the screen---
```
