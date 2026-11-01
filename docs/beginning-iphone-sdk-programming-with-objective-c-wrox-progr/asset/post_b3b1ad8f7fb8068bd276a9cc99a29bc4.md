
```objc
CGPoint touch1PT = [touch1 locationInView:[self view]];
CGPoint touch2PT = [touch2 locationInView:[self view]];

NSLog(@"Touch1: %.0f, %.0f", touch1PT.x, touch1PT.y);
NSLog(@"Touch2: %.0f, %.0f", touch2PT.x, touch2PT.y);

CGFloat currentDistance = [self distanceBetweenTwoPoints: touch1PT
toPoint: touch2PT];

//---zoom in---
if (currentDistance > originalDistance)
{
    imageView.frame = CGRectMake(imageView.frame.origin.x - 2,
                                 imageView.frame.origin.y - 2,
                                 imageView.frame.size.width + 4,
                                 imageView.frame.size.height + 4);
}
else {
    //---zoom out---
    imageView.frame = CGRectMake(imageView.frame.origin.x + 2,
                                 imageView.frame.origin.y + 2,
                                 imageView.frame.size.width - 4,
                                 imageView.frame.size.height - 4);
}
originalDistance = currentDistance;
} break;
}
```

- 3. Press Command-R to test the application on the iPhone Simulator.
- 4. Single-tap the image view to enlarge. To zoom the image in and out, Option-click the image (see Figure 14-7).

### How It Works

To detect for the pinch gesture, you need to find out the distance between the two fingers and constantly compare their distances so that you know whether the two fingers are moving toward or away from each other.

To find the distance between two fingers, you define the distanceBetweenTwoPoints:toPoint: method:

```objc
-(CGFloat) distanceBetweenTwoPoints:(CGPoint)fromPoint
toPoint:(CGPoint)toPoint {
    float lengthX = fromPoint.x - toPoint.x;
    float lengthY = fromPoint.y - toPoint.y;
    return sqrt((lengthX * lengthX) + (lengthY * lengthY));
}
```

This method takes in two CGPoint structures and then calculates the distance between them.
No rocket science here — just the Pythagorean theorem in action.

![](img/16991b58db5894715c4a443315e06a22_361_0.png)

When the two fingers first touch the screen, you record their distance in the touchesBegan:withEvent: method (see the code in bold):

```objc
-(void) touchesBegan: (NSSet *) touches withEvent: (UIEvent *) event {
    //...
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
```

As the two fingers move on the screen, you constantly compare their current distance with the original distance (see Figure 14-8).

![](img/16991b58db5894715c4a443315e06a22_362_0.png)

FIGURE 14-8

If the current distance is greater than the original distance, this is a zoom-in gesture. If not, it is a zoom-out gesture:

``` 
//---fired when the user moved his finger(s) on the screen---
// - (void) touchesMoved: (NSSet *) touches withEvent: (UIEvent *) event {
//
// ...
// //---double-touch---
// case 2: {
// //---get info of first touch---
// UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];
//
// //---get info of second touch---
// UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];
//
// //---get the points touched---
// CGPoint touch1PT = [touch1 locationInView:[self view]];
// CGPoint touch2PT = [touch2 locationInView:[self view]];
//
// NSLog(@"Touch1: %.0f, %.0f", touch1PT.x, touch1PT.y);
// NSLog(@"Touch2: %.0f, %.0f", touch2PT.x, touch2PT.y);
//
// CGFloat currentDistance = [self distanceBetweenTwoPoints: touch1PT
// toPoint: touch2PT];
//
// //---zoom in---
// if (currentDistance > originalDistance)
// {
// imageView.frame = CGRectMake(imageView.frame.origin.x - 2,
// imageView.frame.origin.y - 2,
// imageView.frame.size.width + 4,
// imageView.frame.size.height + 4);
// }
// else {
// //---zoom out---
// imageView.frame = CGRectMake(imageView.frame.origin.x + 2,
// imageView.frame.origin.y + 2,
// imageView.frame.size.width - 4,
// imageView.frame.size.height - 4);
// }
// originalDistance = currentDistance;
// } break;
// }
```

### Implementing the Drag Gesture

Another gesture that you can implement is the drag gesture, in which you tap an item on the screen and drag the item by moving the finger. In the following Try It Out, you learn how to drag an image view on the screen by implementing the drag gesture.

### TRY IT OUT Dragging the ImageView

- 1. Using the same project created earlier, resize the ImageView view so that it fits the size of the image (see Figure 14-9).
- 2. Add the following statements that appear in bold to the touchesMoved:withEvent: method:

```objc
//---fired when the user moved his finger(s) on the screen---
- (void) touchesMoved: (NSSet *) touches withEvent:
(UIEvent *) event {

//---get all touches on the screen---
NSSet *allTouches = [event allTouches];

//---compare the number of touches on the screen---
switch ([allTouches count])
{
    //---single touch---
    case 1: {
        //---get info of the touch---
        UITouch *touch = [[allTouches allObjects] objectAtIndex:0];

        //---check to see if the image is being touched---
        CGPoint touchPoint = [touch locationInView:[self view]];

        if (touchPoint.x > imageView.frame.origin.x &&
            touchPoint.x < imageView.frame.origin.x +
            imageView.frame.size.width &&
            touchPoint.y > imageView.frame.origin.y &&
            touchPoint.y < imageView.frame.origin.y +
            imageView.frame.size.height) {
            [imageView setCenter:touchPoint];
        }
    } break;

    //---double-touch---
    case 2: {
        //---get info of first touch---
        UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];
        //---get info of second touch---
        UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];

        //...
    } break;
}
```

![](img/16991b58db5894715c4a443315e06a22_364_0.png)

FIGURE 14-9

## 15 Simple Animations

### WHAT YOU WILL LEARN IN THIS CHAPTER

- How to use the `NSTimer` class to create timers that will call methods at regular time intervals
- How to perform some simple animations using the `NSTimer` class
- How to perform affine transformation on the `ImageView`
- How to animate a series of images using the `ImageView`

Up to this point, the applications you have written have all made use of the standard views provided by the iPhone SDK. As Apple has reiterated, the iPhone and iPod Touch are more than just phones. The iPhone is also a music player and, more important for this chapter, the iPhone is also a gaming platform.

In this chapter, you can have some fun and create something visual. You learn how to perform some simple animations using a timer object and then perform some transformations on a view. Although it is beyond the scope of this book to show you how to create animations using OpenGL, this chapter does show you some interesting techniques that you can use to make your applications come alive!

### USING THE NSTIMER CLASS

One of the easiest ways to get started with animation is to use the `NSTimer` class. The `NSTimer` class creates timer objects, which allow you to call a method at regular time intervals. Using an `NSTimer` object, you can update an image at regular time intervals, thereby creating an impression that it is being animated.

- 5. Select the View (outside the ImageView) and change the background color to black (see Figure 15-2).

![](img/16991b58db5894715c4a443315e06a22_370_0.png)

FIGURE 15-2

- 6. Add a Label and a Slider view from the Library onto the View window (see Figure 15-3). Set the Initial property of the Slider view to 0.01.

![](img/16991b58db5894715c4a443315e06a22_370_1.png)

FIGURE 15-3
