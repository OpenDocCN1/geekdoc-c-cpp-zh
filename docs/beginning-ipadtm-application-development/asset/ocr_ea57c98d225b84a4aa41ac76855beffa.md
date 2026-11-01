```
if (currentDistance > originalDistance) {
    imageView.frame = CGRectMake(
        imageView.frame.origin.x - 2,
        imageView.frame.origin.y - 2,
        imageView.frame.size.width + 4,
        imageView.frame.size.height + 4);
}
else {
    //---zoom out---
    imageView.frame = CGRectMake(
        imageView.frame.origin.x + 2,
        imageView.frame.origin.y + 2,
        imageView.frame.size.width - 4,
        imageView.frame.size.height - 4);
}
    originalDistance = currentDistance;
} break;
...
```

# Implementing the Drag Gesture

Another gesture that you can implement is the drag, in which you touch an item on the screen and then drag it by moving the finger. In the following Try It Out, you learn how to drag an ImageView on the screen by implementing the drag gesture.

# TRY IT OUT  Dragging the ImageView

+   1. Using the MultiTouch project created earlier, resize the ImageView so that it fits the size of the image (see Figure 12-17).
+   
+   2. Add the following statements that appear in bold to the touchesMoved:withEvent: method:
+   ```
+   //---fired when the user moved his finger(s) on the screen---
+   -(void) touchesMoved: (NSSet *) touches withEvent: (UIEvent *) event {
+   
+       //---get all touches on the screen---
+       NSSet *allTouches = [event allTouches];
+   
+       //---compare the number of touches on the screen---
+       switch ([allTouches count])
+       {
+           //---single touch---
+           case 1: {
+               //---get info of the touch---
+               UITouch *touch = [[allTouches allObjects] objectAtIndex:0];
+   
+               //---check to see if the image is being touched---
+               CGPoint touchPoint = [touch locationInView:[self view]];
+   
+               if (touchPoint.x > imageView.frame.origin.x &&
+   ```