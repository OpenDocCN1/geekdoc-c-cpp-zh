3. Press Command-R to test the application on the iPhone Simulator. When the application is loaded, you see the alert view as shown in Figure 4-2.

![](bbox=[0.7, 0.14, 0.92, 0.6])

4. Back in Xcode, modify the otherButtonTitles parameter by setting it with the value shown in bold:

```
```objc
UIAlertView *alert = [[UIAlertView alloc]
initWithTitle:@"Hello"
message:@"This is an alert view"
delegate:self
cancelButtonTitle:@"OK"
otherButtonTitles:@"Option 1",
@"Option 2", nil];
```
```

5. In the UsingViewsViewController.h file, add the following line that appears in bold:

```
```objc
#import <UIKit/UIKit.h>

@interface UsingViewsViewController : UIViewController
<UIAlertViewDelegate> {
}

@end
```
```

6. In the UsingViewsViewController.m file, add the following method:

```
```objc
- (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:
(NSInteger)buttonIndex {

NSLog([[NSString stringWithFormat:@"%d", buttonIndex]);
}
```
```

![](bbox=[0.7, 0.7, 0.92, 0.95])

7. Press Command-R to test the application in the iPhone Simulator. Notice that there are now two additional buttons besides the OK button (see Figure 4-3).

8. Click any one of the buttons — Option 1, Option 2, or OK.

9. In Xcode, press Command-Shift-R to view the Debugger Console window. Observe the values printed. You can rerun the application a number of times and click the different buttons to observe the values printed.

10. You should observe the values printed for each button clicked:

+   - OK button — 0
+   - Option 1 — 1
+   - Option 2 — 2