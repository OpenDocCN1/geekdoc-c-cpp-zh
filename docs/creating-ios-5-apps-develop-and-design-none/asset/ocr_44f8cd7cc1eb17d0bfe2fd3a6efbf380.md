```
```objc
@property (strong, nonatomic) IBOutlet UIPickerView *unitPickerView;
@property (strong, nonatomic) IBOutlet UIButton *doneButton;
- (IBAction)done:(id)sender;
@end
```
```

We still need to make a few additional changes. Start by importing our WeightEntry class, and add a forward declaration for the UnitSelectorViewControllerDelegate protocol before its @interface block.

```
```objc
#import <UIKit/UIKit.h>

#import "WeightEntry.h"
@protocol UnitSelectorViewControllerDelegate;
@interface UnitSelectorViewController :
UIViewController <UIPickerViewDelegate, UIPickerViewDataSource> {
...
```
```

Now let’s declare two additional properties: one for our delegate, the other for our default unit.

```
```objc
@property (strong, nonatomic) IBOutlet UIButton *doneButton;
@property (weak, nonatomic) id<UnitSelectorViewControllerDelegate>
    delegate;
@property (assign, nonatomic) WeightUnit defaultUnit;
- (IBAction)done:(id)sender;
```
```

Finally, we need to define our protocol. Add the following, after the @interface block:

```
```objc
@protocol UnitSelectorViewControllerDelegate <NSObject>
- (void)unitSelectorDone:(UnitSelectorViewController*)controller;
- (void)unitSelector:(UnitSelectorViewController*)controller
             changedUnit:(WeightUnit)unit;
@end
```
```

That’s it. We’re done with the interface. Now we need to implement these methods.