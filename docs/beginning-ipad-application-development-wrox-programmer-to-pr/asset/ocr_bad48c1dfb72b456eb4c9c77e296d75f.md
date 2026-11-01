```
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
images = [[NSArray alloc] initWithObjects:@"architecture.jpeg",
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
```