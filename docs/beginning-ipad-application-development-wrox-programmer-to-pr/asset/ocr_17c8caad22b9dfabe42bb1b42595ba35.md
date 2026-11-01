![](bbox=[0.14, 0.1, 0.7, 0.42])

FIGURE 12-10

5. Select the ImageView and view its Attributes Inspector window (see Figure 12-11). Set its Image property to apple.jpeg.

6. In the MultiTouchViewController.h file, add the following statements that appear in bold:

```
```objc
#import <UIKit/UIKit.h>

@interface MultiTouchViewController : UIViewController {
    IBOutlet UIImageView *imageView;
}

@property (nonatomic, retain) UIImageView *imageView;

@end
```
```

7. Back in Interface Builder, Control-click and drag the File's Owner item to the ImageView. Select ImageView.

8. In the MultiTouchViewController.m file, add the following statements that appear in bold:

```
```objc
#import "MultiTouchViewController.h"

@implementation MultiTouchViewController

@synthesize imageView;

//---fired when the user finger(s) touches the screen---
-(void) touchesBegan: (NSSet *) touches withEvent: (UIEvent *) event {

    //---get all touches on the screen---
    NSSet *allTouches = [event allTouches];

    //---compare the number of touches on the screen---
```
```