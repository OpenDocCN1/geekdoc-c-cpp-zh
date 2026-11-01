```
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
```

+   3. Press Command-R to test the application on the iPhone Simulator.
+   4. Single-tap the image view to enlarge. To zoom the image in and out, Option-click the image (see Figure 14-7).

# How It Works

To detect for the pinch gesture, you need to find out the distance between the two fingers and constantly compare their distances so that you know whether the two fingers are moving toward or away from each other.

To find the distance between two fingers, you define the distanceBetweenTwoPoints:toPoint: method:

```
```objc
-(CGFloat) distanceBetweenTwoPoints:(CGPoint)fromPoint
toPoint:(CGPoint)toPoint {
    float lengthX = fromPoint.x - toPoint.x;
    float lengthY = fromPoint.y - toPoint.y;
    return sqrt((lengthX * lengthX) + (lengthY * lengthY));
}
```
```

This method takes in two CGPoint structures and then calculates the distance between them.
No rocket science here — just the Pythagorean theorem in action.

![](bbox=[0.75, 0.55, 0.95, 0.9])