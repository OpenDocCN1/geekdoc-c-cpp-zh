```
[[UITapGestureRecognizer alloc]
    initWithTarget:self
    action:@selector(handleTapGesture:)];

tapGesture.numberOfTapsRequired = 2;
[imageView addGestureRecognizer:tapGesture];
[tapGesture release];

[super viewDidLoad];
}

//---handle tap gesture---
-(IBAction) handleTapGesture:(UIGestureRecognizer *) sender {
    if (sender.view.contentMode == UIViewContentModeScaleAspectFit)
        sender.view.contentMode = UIViewContentModeCenter;
    else
        sender.view.contentMode = UIViewContentModeScaleAspectFit;
}
- (void)dealloc {
    [imageView release];
    [super dealloc];
}
```

![](bbox=[0.1, 0.52, 0.9, 0.9])

FIGURE 12-2