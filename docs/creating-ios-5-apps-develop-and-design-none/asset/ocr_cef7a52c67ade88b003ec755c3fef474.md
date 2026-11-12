![](bbox=[0.06, 0.153, 0.752, 0.534])

Then switch back to the storyboard file, and open the Assistant editor. Make sure UnitSelectorViewController.h is showing. Control-drag the picker view to the header file, and create a strong outlet named unitPickerView. Next, Control-drag the button twice. First, create a strong outlet named doneButton. Then create an action named done. Make sure its Event is set to Touch Up Inside.

FIGURE 4.15 The unit selector view

FIGURE 4.16 Connecting the delegate

Now we need to link the picker view to its delegate and data source. Right-click the picker view, and then drag from the pop-up window's delegate outlet to the view controller icon in the scene's dock (Figure 4.16). Next, drag the pop-up's dataSource outlet to the view controller as well.

# DEFINING THE VIEW DELEGATE

Switch back to the Standard editor and the UnitSelectorViewController.h file. It should now appear as shown here:

```
```objc
#import <UIKit/UIKit.h>

@interface UnitSelectorViewController : UIViewController
<UIPickerViewDelegate, UIPickerViewDataSource>
```
```