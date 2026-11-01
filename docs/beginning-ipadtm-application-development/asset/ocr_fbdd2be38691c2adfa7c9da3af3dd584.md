```
//---create a Label view---
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

//---add the views to the current View---
[self.view addSubview:label];
[self.view addSubview:button];

[super viewDidLoad];
}
```

# Creating and Connecting Actions

In the previous example, you saw how you can add a Label and Button view to the main View window. However, you need to handle the events raised by the Button view so that when the user presses it, you can perform some work. Chapter 3 covered using outlets and actions and how you connect your code to them using Interface Builder, but in the following Try it Out, the views are created using code, and hence you cannot use Interface Builder to connect the actions and outlets — you have to do it by code, too.

# TRY IT OUT  Linking Actions to Views

+   1. Continuing with the windowBasedApp project, declare the buttonClicked: action (shown in bold) in the MySecondViewController.h file as follows:

```
#import <UIKit/UIKit.h>

@interface MySecondViewController : UIViewController {
//---create two outlets - label and button---
UILabel *label;
UIButton *button;
}

//---expose the outlets as properties---
@property (nonatomic, retain) UILabel *label;
@property (nonatomic, retain) UIButton *button;

//---declaring the IBAction---
-(IBAction) buttonClicked: (id) sender;

@end
```