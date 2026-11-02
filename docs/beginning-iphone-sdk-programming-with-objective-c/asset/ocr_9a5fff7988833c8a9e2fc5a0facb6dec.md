+   8. Under the Resources group, add a new View XIB item and name it as `AddCountryView.xib`.

+   9. Double-click on the `AddCountryView.xib` file to edit it in Interface Builder. Populate it with a Search Bar and a Round Rect Button view (see Figure 9-11).

+   10. In the AddCountryView.xib window, select the File’s Owner item and view the Identity Inspector window. Set the Class to `AddCountryViewController`. Also, add a done action to the File’s Owner item (see Figure 9-12).

+   11. Control-click and drag the File’s Owner item to the View item and select view.

+   12. Control-click and drag the Done button to the File’s Owner item. Select the done action.

![](bbox=[0.565, 0.099, 0.85, 0.438])

![](bbox=[0.112, 0.467, 0.606, 0.761])

+   13. Back in Xcode, insert the following code that appears in bold in the `AddCountryViewController.h` file:

```
```objc
#import <UIKit/UIKit.h>

//---defines the protocol---
@protocol AddCountryViewControllerDelegate;

@interface AddCountryViewController : UIViewController {
    //---delegate---
    id <AddCountryViewControllerDelegate> delegate;
}
```
```