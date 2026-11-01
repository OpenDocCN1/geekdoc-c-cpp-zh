8. Name the View Controller SecondViewController.m.

9. Next, add a new view .xib file so that the UI can be created using Interface Builder. Right-click the Resources group in Xcode and add a new file. Choose the User Interfaces group and then select the View XIB template (see Figure 4-24).

![](bbox=[0.12, 0.23, 0.6, 0.54])

FIGURE 4-24

10. Name the .xib file SecondView.xib. The Xcode should now contain the files that you have just added (see Figure 4-25).

11. Take a look at the SecondViewController.h file and observe that the SecondViewController class inherits from the UIViewController base class:

```
#import <UIKit/UIKit.h>

@interface SecondViewController : UIViewController {
}

@end
```

![](bbox=[0.45, 0.6, 0.92, 0.85])

FIGURE 4-25