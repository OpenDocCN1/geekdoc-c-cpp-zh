```
```objective-c
controller.view.center =
    CGPointMake(center.x + vBounce,
                center.y + hBounce)
}
completion:bounceDown];
};
```
```

Here, we define our bounceUp block. Again, we’re using a 0.15-second duration; however, this time we use UIViewAnimationCurveEaseOut. The animation will start quickly and slow down over the duration. In the animation block, we simply move the view to the top of its bounce position (defined by the vertical and horizontal bounce offsets). When this animation is finished, we call our bounceDown block.

```
```objective-c
// Initial movement onto the screen.
// This will call bounce up when completed.
[UIView animateWithDuration:0.5f
                     delay:0.0f
                   options:UIViewAnimationCurveEaseIn
                animations:^{
                    controller.view.center = center;
                    controller.view.alpha = 1.0f;
                }
                completion:bounceUp];
}
```
```

Finally, we have the initial animation block. This takes a half second, with a UIViewAnimationCurveEaseIn animation curve. Again, this will cause the view to start moving slowly, but it will accelerate over the duration of the sequence.

This simply centers our pop-up view. We also set the alpha value to 1.0f, just in case. After all, it is possible to both move and fade-in our view at the same time. When the animation sequence is done, we call our bounceUp method.