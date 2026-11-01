![](bbox=[0.14, 0.15, 0.7, 0.38])

```
FIGURE B-14
```objc
-(void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration {
    if ([toInterfaceOrientation isEqualToInterfaceOrientationPortrait]) {
        win.frame = CGRectMake(320,480,320,480);
    } else
        win.frame = CGRectMake(180,243,288,371);
    }
```
```

> NOTE You can toggle the state of a breakpoint by clicking it to enable or disable it. Breakpoints displayed in dark blue are enabled; those displayed in light blue are disabled. To remove a breakpoint, click on one and drag it out of its resting place. It will disappear into a puff of smoke!

After you have set breakpoints in your application, press Command-Y to debug your application. The code will stop at your breakpoints.

> NOTE If you press Command-R to run the application, your code will not stop at the breakpoints.

When the application reaches the breakpoint you have set, Xcode indicates the current line of execution with a red arrow (see Figure B-15).

![](bbox=[0.15, 0.92, 0.8, 1.0])