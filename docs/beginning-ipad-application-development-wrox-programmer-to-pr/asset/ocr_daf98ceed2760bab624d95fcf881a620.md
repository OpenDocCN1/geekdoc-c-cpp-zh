11. In the windowBasedAppAppDelegate.m file, insert the following code lines that appear in bold:

```
#import "windowBasedAppAppDelegate.h"
#import "HelloWorldViewController.h"

@implementation windowBasedAppAppDelegate

@synthesize window;

//---synthesize the property---
//@synthesize viewController;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch
    //---add the new view to the current window---
    [window addSubview:viewController.view];
    
    [window makeKeyAndVisible];
    
    return YES;
}

- (void)dealloc {
    [viewController release];
    [window release];
    [super dealloc];
}

@end
```

12. In the MainWindow.xib window, Control-click and drag the Window Based App App Delegate item to the Hello World View Controller item (see Figure 4-20). Select viewController. This will associate the window with the View Controller.

13. That's it! Press Command-R to test the application on the iPhone Simulator. The button appears on the main screen of the application (see Figure 4-21).

![](bbox=[0.6, 0.55, 0.95, 0.8])

FIGURE 4-20