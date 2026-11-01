# TRY IT OUT Dragging the ImageView

+   1. Using the same project created earlier, resize the ImageView view so that it fits the size of the image (see Figure 14-9).
+   2. Add the following statements that appear in bold to the touchesMoved:withEvent: method:

```
//---fired when the user moved his finger(s) on the screen---
- (void) touchesMoved: (NSSet *) touches withEvent:
(UIEvent *) event (

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

![](bbox=[0.68, 0.2, 0.92, 0.62])

FIGURE 14-9