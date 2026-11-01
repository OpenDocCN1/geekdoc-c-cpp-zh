![](bbox=[0.13, 0.16, 0.46, 0.56])

FIGURE 17-3

# How It Works

To use the accelerometer in your iPhone or iPod Touch, you need to the implement the UIAccelerometerDelegate protocol in your delegate (such as the View Controller):

```
@interface AccelerometerViewController : UIViewController
<UIAccelerometerDelegate> {
```

When the view is loaded, you first obtain a single instance of the UIAccelerometer class using the sharedAccelerometer method. You then specify the delegate of the instance and the update interval in which you want to obtain accelerometer data:

```
- (void)viewDidLoad {
    UIAccelerometer *acc = [UIAccelerometer sharedAccelerometer];
    acc.delegate = self;
    acc.updateInterval = 1.0f/60.0f;
    [super viewDidLoad];
}
```

The updateInterval property specifies the interval in seconds — that is, the number of seconds between updates. In the preceding case, you indicate that you want the accelerometer data to be updated 60 times a second.