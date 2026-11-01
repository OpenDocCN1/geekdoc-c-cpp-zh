# How It Works

This application works by sensing the user's touch on the screen of the iPad. When the user touches the screen, the View or View Controller fires a series of events that you can handle. There are four such events:

+   - touchesBegan:withEvent:
+   - touchesEnded:withEvent:
+   - touchesMoved:withEvent:
+   - touchesCancelled:withEvent:

Take a closer look at the first event. The touchesBegan:withEvent: event is fired when at least one touch is sensed on the screen. In this event, you can know how many fingers are on the screen by calling the allTouches method of the UIEvent object (event):

```
//---get all touches on the screen---
NSSet *allTouches = [event allTouches];
```

The allTouches method returns an NSSet object containing a set of UITouch objects. To know how many fingers are on the screen, simply count the number of UITouch objects in the NSSet object using the count method. In this case, you are (at this moment) interested only in a single touch, therefore you implement only the case for one touch:

```
//---compare the number of touches on the screen---
switch ([allTouches count])
{
    //---single touch---
    case 1: {
        //---get info of the touch---
        UITouch *touch = [[allTouches allObjects] objectAtIndex:0];

        //---compare the taps---
        switch ([touch tapCount])
        {
            //---single tap---
            case 1: {
                imageView.contentMode = UIViewContentModeScaleAspectFit;
            } break;

            //---double tap---
            case 2: {
                imageView.contentMode = UIViewContentModeCenter;
            } break;
        }
    } break;
}
```

You extract details of the first touch by using the allObjects method of the NSSet object to return an NSArray object. You then use the objectAtIndex: method to obtain the first array item.

The UITouch object (touch) contains the tapCount property, which tells you whether the user has single-tapped the screen or performed a double tap (or more). If the user single-tapped the screen, you resize the