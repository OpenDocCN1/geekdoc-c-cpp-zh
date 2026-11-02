3. Double-click the FlipsideView.xib file to edit it in Interface Builder.

+   4. In the FlipsideView.xib window, double-click the Flipside View item and add the following views to the Flipside View window (see Figure 11-15):
+      - Label
+      - TextField
+      - PickerView

![](bbox=[0.064, 0.292, 0.598, 0.693])

FIGURE 11-15

5. Back in Xcode, insert the following code that appears in bold into the MainViewController.h file:

```
```objc
#import "FlipsideViewController.h"

@interface MainViewController : UIViewController <FlipsideViewControllerDelegate> {
}

- (IBAction)loadSettings: (id) sender;
- (IBAction)showInfo;

@end
```
```