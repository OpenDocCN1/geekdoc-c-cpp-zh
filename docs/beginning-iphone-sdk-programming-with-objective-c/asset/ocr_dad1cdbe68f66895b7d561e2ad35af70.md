> **NOTE** Refer to Appendix D for a discussion of the concept of protocols in Objective-C.

# Using the Action Sheet

Although the Alert view can display multiple buttons, its primary use is still as a tool to alert users when something happens. If you need to display a message with multiple choices for the user to select, you should use an action sheet rather than the Alert view. An action sheet displays a collection of buttons among which the user can select one. It always emerges from the bottom of the screen and is anchored to the sides of the screen, giving the cue to the user that the action sheet's details are connected to the current application. A good example of the use of an action sheet is when you tap on the "+" button in Safari. Tapping on the "+" button displays an action sheet where you add a bookmark, add the current page to the Home Screen, or mail the link of the current page. The following Try It Out puts you to work with an action sheet.

# **TRY IT OUT** Using an Action Sheet

+   1. Using the same project created in the previous section, modify the viewDidLoad method (in the UsingViewsViewController.m file) as follows:

```
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

+   2. In the UsingViewsViewController.h file, add the following statement that appears in bold:

```
#import <UIKit/UIKit.h>

@interface UsingViewsViewController : UIViewController
<UIActionSheetDelegate> {
}
@end
```