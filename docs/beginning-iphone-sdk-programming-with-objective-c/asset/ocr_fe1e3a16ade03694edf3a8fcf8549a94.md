```
@property (nonatomic, retain) UISlider *slider;

-(IBAction) sliderMoved:(id) sender;

@end
```

2. In the AnimationViewController.m file, add the following statement that appears in bold:

```
-(void) onTimer {
    //---rotation---
    imageView.transform = CGAffineTransformMakeRotation(angle);
    angle += 0.02;
    if (angle>6.2857) angle = 0;
    
    imageView.center = CGPointMake(
        imageView.center.x + position.x,
        imageView.center.y + position.y);
    
    if (imageView.center.x > 320 - ballRadius || imageView.center.x < ballRadius)
        position.x = -position.x;
    if (imageView.center.y > 460 - ballRadius || imageView.center.y < ballRadius)
        position.y = -position.y;
}
```

```
-(void)viewDidLoad {
    //---set the angle to 0---
    angle = 0;
    
    ballRadius = imageView.frame.size.width/2;
    [slider setShowValue:YES];
    position = CGPointMake(12.0,4.0);
    timer = [NSTimer scheduledTimerWithTimeInterval:slider.value
             target:self
             selector:@selector(onTimer)
             userInfo:nil
             repeats:YES];
    [super viewDidLoad];
}
```

> NOTE If you have added the code to perform translation in the Translation section, be sure to remove it before adding the code outlined in this step.

3. Press Command-R to test the application. The tennis ball now rotates as it bounces across the screen.