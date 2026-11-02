
# 7 View Controllers

## What You Will Learn in This Chapter

- How to create a Window-based Application and manually add a View Controller and a View window to it
- How to create views dynamically during runtime
- How to wire up events of views with event handlers via code
- How to switch to another view during runtime
- How to animate the switching of views

Until this point, you have been dealing with single view applications; that is, applications with a single View Controller. The previous chapters have all been using the View-based Application template available in the iPhone SDK because it is the simplest way to get started in iPhone programming. When you create a View-based application, there is by default one View Controller (named `<project_name>ViewController` by the iPhone SDK). In real-life applications, you often need more than one View Controller, with each controlling a different view displaying different information. A good example of a multiview application is the Weather application shipped with the iPhone. The main view shows the weather of a region you have selected, and you can swipe the screen to view the weather of other locations. You can also press the **i** icon to flip to another view and add locations.

This chapter teaches you how to create multiple views in your application and then programmatically switch among them during runtime. In addition, you learn how to animate the switching of views using the built-in animation methods available in the iPhone SDK.

## Creating a Window-Based Application

In this section, you discover another type of application template you can create using the iPhone SDK: the Window-based Application template. Unlike the View-based Application template, the Window-based Application template does not include a View Controller by default. Instead, it provides only the skeleton of an iPhone application and leaves the rest to the developer — you need to add your own views and View Controllers. Because of this, a Window-based Application presents a very good way for you to understand how View Controllers work and appreciate all the work needed to connect the View Controllers and XIB files. When you understand how View Controllers work, you will be on your way to creating multiview applications.

To put first things first, execute the following Try It Out to write a Window-based Application and then progressively add a View Controller to it. You will need to download the project files as indicated here for this and other Try It Out features in this chapter.

### Try It Out: Adding a View Controller Using Interface Builder

Codefile [WinBasedApp.zip] available for download on Wrox.com

1. Using Xcode, create a Window-based Application project and name it WinBasedApp. Observe the files created for this project type (see Figure 7-1). Apart from the other, usual supporting file, note that there is only one XIB file (MainWindow.xib) and two delegate files (WinBasedAppAppDelegate.h and WinBasedAppAppDelegate.m).

2. Press Command-R to test the application, and you will realize that an empty screen is displayed on the iPhone Simulator. This is because the Window-based Application template provides only the skeleton structure for a simple iPhone application containing just a window and the application delegate.

3. Back in Xcode, double-click MainWindow.xib to edit it in Interface Builder. Observe that there are four items in the MainWindow.xib window (see Figure 7-2):
   - File's Owner
   - First Responder
   - Win Based App App Delegate
   - Window

![FIGURE 7-1](img/aab2d775c46f70cd606f2e58e2521324_192_0.png)

![FIGURE 7-2](img/aab2d775c46f70cd606f2e58e2521324_192_1.png)

![FIGURE 7-4](img/aab2d775c46f70cd606f2e58e2521324_194_0.png)

6. Right-click the Resources group in Xcode and add a new file. Select the View XIB item and name it MyView.xib. Xcode should now look like Figure 7-5.

![FIGURE 7-5](img/aab2d775c46f70cd606f2e58e2521324_194_1.png)

7. Back in Interface Builder, select the View Controller item in the MainWindow.xib window and view its Identity Inspector window. In the Class drop-down list, select MyViewController (see Figure 7-6). The name of the View Controller will now change to My View Controller.

```objc
#import <UIKit/UIKit.h>

@class MyViewController;

@interface WinBasedAppAppDelegate : NSObject <UIApplicationDelegate> {
    UIWindow *window;

    //---create an instance of the view controller---
    MyViewController *myViewController;
}

@property (nonatomic, retain) IBOutlet UIWindow *window;

//---expose the view controller as a property---
@property (nonatomic, retain) IBOutlet MyViewController *myViewController;

@end
```

In the WinBasedAppAppDelegate.m file, insert the following code lines that appear in bold:

```objc
#import "WinBasedAppAppDelegate.h"

#import "MyViewController.h"

@implementation WinBasedAppAppDelegate

@synthesize window;

//---synthesize the property---
@synthesize myViewController;

- (void)applicationDidFinishLaunching:(UIApplication *)application {
    // Override point for customization after application launch
    //---add the new view to the current window---
    [window addSubview:myViewController.view];

    [window makeKeyAndVisible];
}

- (void)dealloc {
    [myViewController release];
    [window release];
    [super dealloc];
}

@end
```

13. In the MainWindow.xib window, Control-click and drag the Win Based App App Delegate item to the My View Controller item (see Figure 7-10). Select myViewController. This will associate the window with the View Controller.

![FIGURE 7-10](img/aab2d775c46f70cd606f2e58e2521324_198_0.png)

![FIGURE 7-11](img/aab2d775c46f70cd606f2e58e2521324_198_1.png)

14. That's it! Press Command-R to test the application on the iPhone Simulator. You should now see the button appearing on the main screen of the application (see Figure 7-11).

> **Note:** As an exercise, you might want to create an action to display an alert view when the button is pressed.

### How It Works

When you create an iPhone project using the Window-based Application template, Xcode provides you with only the bare minimum number of items in your project — a MainWindow.xib file and the application delegate. You are supposed to add your own View Controller and view.

In the preceding exercise, you first added a View Controller item to the MainWindow.xib window. You then added an instance of the UIViewController class (which you named MyViewController) so that it could be connected to the View Controller you just added. This controller class contains the code that you will write to handle the interactions between the view and the user.

You also added a XIB file to the project (MyView.xib) representing a View in Interface Builder. Take note of the various steps that you need to perform to connect the relevant classes to the correct XIB and View Controller items.

When the application has finished launching, you add the View represented by the myViewController object to the window so that it is visible using the addSubview: method of the UIWindow instance:

```objc
[window addSubview:myViewController.view];
```

```objc
[myViewController release];
[window release];
[super dealloc];
}
```

3. In the MySecondViewController.h file, insert the following lines of code that appear in bold:

```objc
#import <UIKit/UIKit.h>

@interface MySecondViewController : UIViewController {
    //---create two outlets - label and button---
    UILabel *label;
    UIButton *button;
}

//---expose the outlets as properties---
@property (nonatomic, retain) UILabel *label;
@property (nonatomic, retain) UIButton *button;

@end
```

4. In the MySecondViewController.m file, add the viewDidLoad() method:

```objc
//---synthesize the properties---
@synthesize label, button;

- (void)viewDidLoad {

    //---create a CGRect for the positioning---
    CGRect frame = CGRectMake(10, 10, 300, 50);

    //---create a label view---
    label = [[UILabel alloc] initWithFrame:frame];
    label.textAlignment = UITextAlignmentCenter;
    label.font = [UIFont fontWithName:@"Verdana" size:20];
    label.text = @"This is a label";

    //---create a Button view---
    frame = CGRectMake(10, 250, 300, 50);
    button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
    button.frame = frame;
    [button setTitle:@"OK" forState:UIControlStateNormal];
    button.backgroundColor = [UIColor clearColor];

    [self.view addSubview:label];
    [self.view addSubview:button];

    [super viewDidLoad];
}
```
