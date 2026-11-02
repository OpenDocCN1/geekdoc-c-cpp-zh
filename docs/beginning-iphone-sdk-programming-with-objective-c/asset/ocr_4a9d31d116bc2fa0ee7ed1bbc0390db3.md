![](bbox=[0.05, 0.14, 0.78, 0.64])

FIGURE 11-16

+   10. In the MainView.xib window, Control-click and drag the Button view to the File's Owner item and select loadSettings:.
+   11. Save the project in Interface Builder.
+   12. In Xcode, add the following code in bold to the FlipsideViewController.m file:

```
```objc
#import "FlipsideViewController.h"

@implementation FlipsideViewController

@synthesize delegate;
@synthesize loginName;
@synthesize password;
@synthesize favoriteColor;

NSMutableArray *colors;
NSString *favoriteColorSelected;

- (void)viewDidLoad {
    //---create an array containing the colors values---
    colors = [[NSMutableArray alloc] init];
    [colors addObject:@"Red"];
```
```