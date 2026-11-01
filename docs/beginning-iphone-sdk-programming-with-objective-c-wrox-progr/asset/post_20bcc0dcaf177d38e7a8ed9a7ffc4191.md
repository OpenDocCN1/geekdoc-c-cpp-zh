
![](img/16991b58db5894715c4a443315e06a22_101_0.png)

## FIGURE 3-35

In MyViewController.h, create an outlet for the Web view and expose it as a property:

```objc
#import <UIKit/UIKit.h>

@interface MyViewController : UIViewController {
    IBOutlet UIWebView *webView;
}

@property (retain, nonatomic) UIWebView *webView;

@end
```

Back in the MyViewController.xib file, connect the outlet to the Web view. To verify that the connection is made correctly, right-click the File's Owner item. You should see the connection shown in Figure 3-36.

![](img/16991b58db5894715c4a443315e06a22_102_0.png)

## FIGURE 3-36

In the MyViewController.m file, code the following so that when the view is loaded, it displays the Web page of Apple.com in the Web view:

```objc
#import "MyViewController.h"

@implementation MyViewController

@synthesize webView;

// Implement viewDidLoad to do additional setup after loading the view,
// typically from a nib.
- (void)viewDidLoad {
    NSString *strUrl = @"http://www.apple.com";
    //---create an URL object---
    NSURL *url = [NSURL URLWithString:strUrl];

    //---create an URL Request Object---
    NSURLRequest *request = [NSURLRequest requestWithURL:url];

    //---load the request in the UIWebView---
    [webView loadRequest:request];

    [super viewDidLoad];
}
- (void)dealloc {
    [webView release];
    [super dealloc];
}
@end
```

That's it! Press Command-R to test the application on the iPhone Simulator. Figure 3-37 shows the simulator displaying Apple's home page.

## SUMMARY

In this chapter, you have seen the use of XIB files as well as the role played by View Controllers in an iPhone application. Understanding the use of outlets and actions is extremely important because it is the cornerstone of iPhone development. Throughout this book, you will come across them frequently.

In the next chapter, you learn how you can control the virtual keyboard that automatically pops up when the user tries to enter some data into your application.

![](img/16991b58db5894715c4a443315e06a22_103_0.png)

FIGURE 3-37

## EXERCISES

- 1. Declare and define an outlet for a UITextField view using code.
- 2. Declare and define an action using code.

## WHAT YOU HAVE LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Delegate files | The delegate files contain code that is typically executed during the loading/unloading of the application. |
| View Controllers | View Controllers manage views as well as perform navigation and memory management. |
| Action | An action is a method that can handle events raised by views (for example, when a button is clicked, etc.) in the View window. |
| Outlet | An outlet allows your code to programmatically reference a view on the View window. |
| Adding outlet using code | Use the `IBOutlet` keyword:<br>`IBOutlet UITextField *nameTextField;` |
| Adding action using code | Use the `IBAction` keyword:<br>`- (IBAction)btnClicked:(id)sender;` |
| Connecting actions | To link actions, you always drag from the view in the View window onto the File's Owner item. |
| Connecting outlets | To link outlets, you always drag from the File's Owner item onto the required view in the View window. |

- 3. Press Command-R to test the application on the iPhone Simulator. When the application is loaded, you see the alert view as shown in Figure 4-2.

![](img/16991b58db5894715c4a443315e06a22_109_0.png)

- 4. Back in Xcode, modify the otherButtonTitles parameter by setting it with the value shown in bold:

```objc
UIAlertView *alert = [[UIAlertView alloc]
initWithTitle:@"Hello"
message:@"This is an alert view"
delegate:self
cancelButtonTitle:@"OK"
otherButtonTitles:@"Option 1",
@"Option 2", nil];
```

- 5. In the UsingViewsViewController.h file, add the following line that appears in bold:

```objc
#import <UIKit/UIKit.h>

@interface UsingViewsViewController : UIViewController
<UIAlertViewDelegate> {
}

@end
```

- 6. In the UsingViewsViewController.m file, add the following method:

```objc
- (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:
(NSInteger)buttonIndex {

NSLog([NSString stringWithFormat:@"%d", buttonIndex]);
}
```

![](img/16991b58db5894715c4a443315e06a22_109_1.png)

- 7. Press Command-R to test the application in the iPhone Simulator. Notice that there are now two additional buttons besides the OK button (see Figure 4-3).

- 8. Click any one of the buttons — Option 1, Option 2, or OK.

- 9. In Xcode, press Command-Shift-R to view the Debugger Console window. Observe the values printed. You can rerun the application a number of times and click the different buttons to observe the values printed.

- 10. You should observe the values printed for each button clicked:
    - OK button — 0
    - Option 1 — 1
    - Option 2 — 2

## How It Works

To use UIAlertView, you first instantiate it and initialize it with the various arguments:

```objc
UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Hello"
message:@"This is an alert view"
delegate:self
cancelButtonTitle:@"OK"
otherButtonTitles:nil];
```

The first parameter is the title of the alert view, which you set to "Hello". The second is the message, which you set to "This is an alert view". The third is the delegate, which you need to set to an object that will handle the events fired by the UIAlertView object. In this case, you set it to self, which means that the event handler will be implemented in the current class, that is, the View Controller. The cancelButtonTitle parameter displays a button to dismiss your alert view. Last, the otherButtonTitles parameter allows you to display additional buttons if needed. If no additional buttons are needed, simply set this to nil.

To show the alert view modally, use the show method:

```objc
[alert show];
```

For simple use of the alert view, you don't really need to handle the events fired by it. Tapping the OK button (as set in the cancelButtonTitle parameter) simply dismisses the alert view.

If you want more than one button, you need to set the otherButtonTitles parameter, like this:

```objc
UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Hello"
message:@"This is an alert view"
delegate:self
cancelButtonTitle:@"OK"
otherButtonTitles:@"Option 1", @"Option 2", nil];
```

Note that you need to end the otherButtonTitles parameter with a nil or a runtime error will occur.

Now that you have three buttons, you need to be able to know which button the user pressed — in particular, whether Option 1 or Option 2 was pressed. To do so, you need to handle the event raised by the UIAlertView class. You do so by ensuring that your View Controller conforms to the UIAlertViewDelegate protocol:

```objc
@interface UsingViewsViewController : UIViewController <UIAlertViewDelegate> {
    //...
}
```

The UIAlertViewDelegate protocol contains several methods associated with the alert view. To know which button the user tapped, you need to implement the alertView:clickedButtonAtIndex: method:

```objc
- (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:
(NSInteger)buttonIndex {
    NSLog([NSString stringWithFormat:@"%d", buttonIndex]);
}
```

The index of the button clicked will be passed in via the clickedButtonAtIndex: parameter.

> **NOTE** Refer to Appendix D for a discussion of the concept of protocols in Objective-C.

## Using the Action Sheet

Although the Alert view can display multiple buttons, its primary use is still as a tool to alert users when something happens. If you need to display a message with multiple choices for the user to select, you should use an action sheet rather than the Alert view. An *action sheet* displays a collection of buttons among which the user can select one. It always emerges from the bottom of the screen and is anchored to the sides of the screen, giving the cue to the user that the action sheet's details are connected to the current application. A good example of the use of an action sheet is when you tap on the "+" button in Safari. Tapping on the "+" button displays an action sheet where you add a bookmark, add the current page to the Home Screen, or mail the link of the current page. The following Try It Out puts you to work with an action sheet.

## TRY IT OUT Using an Action Sheet

- 1. Using the same project created in the previous section, modify the `viewDidLoad` method (in the `UsingViewsViewController.m` file) as follows:

```objc
- (void)viewDidLoad {

    UIActionSheet *action = [[UIActionSheet alloc]
        initWithTitle:@"Title of Action Sheet"
        delegate:self
        cancelButtonTitle:@"OK"
        destructiveButtonTitle:@"Delete Message"
        otherButtonTitles:@"Option 1", @"Option 2", nil];
    [action showInView:self.view];
    [action release];
    [super viewDidLoad];
}
```

- 2. In the `UsingViewsViewController.h` file, add the following statement that appears in bold:

```objc
#import <UIKit/UIKit.h>

@interface UsingViewsViewController : UIViewController
<UIActionSheetDelegate> {
}

@end
```
