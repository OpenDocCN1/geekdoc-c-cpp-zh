
5. Press Command-R to test the application on the iPhone Simulator. You will now see the Label and Button views on the main screen of the application (see Figure 7-13).

## How It Works

In contrast to the previous example, in which you added a View Controller item, an instance of the UIViewController class, and a XIB file to your project, this example simply creates an instance of the UIViewController class and adds the views programmatically to the main View window.

In the application delegate, after the application has finished launching, you create an instance of the UIViewController class that you have created:

```objective-c
//---instantiate the view controller---
mySecondViewController = [[MySecondViewController alloc] initWithNibName:nil bundle:nil];
```

You do not need an XIB file because the various views that you will be using will be added programmatically. Hence the initWithNibName: parameter can be set to nil.

To load the View window represented by the instance of the UIViewController class, you use the addSubview: method of the UIWindow instance:

```objective-c
//---add the view from the view controller---
[window addSubview:mySecondViewController.view];
```

To programmatically create your views during runtime, you need to override the viewDidLoad() method of the UIViewController class. Here, you create instances of the Label and Button views manually, specifying their positions as well as their text captions. Finally, you add them to the main View window:

```objective-c
- (void)viewDidLoad {
  //---create a CGRect for the positioning---
  CGRect frame = CGRectMake(10, 10, 300, 50);
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

![](img/aab2d775c46f70cd606f2e58e2521324_201_0.png)

FIGURE 7-13

## Creating and Connecting Actions

In the previous section, you saw that you can programmatically add views during runtime. Also, in the example, you saw how you can add a Label and Button view to the main View. However, you would need to handle the events raised by the Button view so that when the user presses it, you can perform some work. In Chapter 3, you learned about using outlets and actions and how you connect your code to them using Interface Builder. In the following Try It Out, the views are created using code, and hence you cannot use Interface Builder to connect the actions and outlets — you have to do it by code, too.

### Try It Out | Linking Actions to Views

1. Using the same project created in the previous section, declare the buttonClicked: action (shown in bold) in the MySecondViewController.h file as follows:

```objective-c
#import <UIKit/UIKit.h>

@interface MySecondViewController : UIViewController {
    UILabel *label;
    UIButton *button;
}

@property (nonatomic, retain) UILabel *label;
@property (nonatomic, retain) UIButton *button;

//---declaring the IBAction---
-(IBAction) buttonClicked: (id) sender;

@end
```

2. In the MySecondViewController.m file, you provide the implementation for the buttonClicked: action:

```objective-c
-(IBAction) buttonClicked: (id) sender{
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Action invoked!"
                                      message:@"Button clicked!"
                                      delegate:self
                                      cancelButtonTitle:@"OK"
                                      otherButtonTitles:nil);

    [alert show];
    [alert release];
}
```

3. To connect the relevant event (Touch Up Inside) of the Button view with the buttonClicked: action, add the following code that appears in bold to the viewDidLoad() method:

```objective-c
- (void)viewDidLoad {

    CGRect frame = CGRectMake(10, 10, 300, 50);

    //---create a Label view---
    label = [[UILabel alloc] initWithFrame:frame];
    label.textAlignment = UITextAlignmentCenter;
    label.font = [UIFont fontWithName:@"Verdana" size:20];
    label.text = @"This is a label";

    //---create a Button view---
    frame = CGRectMake(10, 50, 300, 50);
    button = [[UIButton buttonWithType:UIButtonTypeRoundedRect]
              retain];
    [button setTitle:@"OK" forState:UIControlStateNormal];
    button.backgroundColor = [UIColor clearColor];

    //---add the action handler and set current class as target---
    [button addTarget:self
               action:@selector(buttonClicked:)
     forControlEvents:UIControlEventTouchUpInside];

    //---add the views to the current View---
    [self.view addSubview:label];
    [self.view addSubview:button];

    [super viewDidLoad];
}
```

4. That’s it! Press Command-R to test the application on the iPhone Simulator. Pressing the OK button displays an alert view (see Figure 7-14).

![](img/aab2d775c46f70cd606f2e58e2521324_203_0.png)

## Control Events

The list of events you can use for control objects are:

- UIControlEventTouchDown
- UIControlEventTouchDownRepeat
- UIControlEventTouchDragInside
- UIControlEventTouchDragOutside
- UIControlEventTouchDragEnter
- UIControlEventTouchDragExit
- UIControlEventTouchUpInside
- UIControlEventTouchUpOutside
- UIControlEventTouchCancel
- UIControlEventValueChanged
- UIControlEventEditingDidBegin
- UIControlEventEditingChanged
- UIControlEventEditingDidEnd
- UIControlEventEditingDidEndOnExit
- UIControlEventAllTouchEvents
- UIControlEventAllEditingEvents
- UIControlEventApplicationReserved
- UIControlEventSystemReserved
- UIControlEventAllEvents

The use of each event is detailed at: http://developer.apple.com/iphone/library/documentation/UIKit/Reference/UIControl_Class/Reference/Reference.html#/apple_ref/doc/constant_group/Control_Events

## Switching to Another View

So far, you have been learning about single-view applications. However, in real life, you often have a number of views, each representing different pieces of information. Depending on the selections made by the user, you then switch to different views to perform different tasks.

Hence, in this section you learn how you can switch to another view depending on the selection made by the user.

### Try It Out | Switching Views

1. Using the same project created in the previous section, add the following code that appears in bold to the MySecondViewController.m file:

```objective-c
#import "MySecondViewController.h"

#import "MyViewController.h"

@implementation MySecondViewController
@synthesize label, button;

//---create an instance of the view controller---
MyViewController *myViewController;

- (IBAction) buttonClicked: (id) sender{

    //---add the view of the view controller to the current View---
    myViewController = [[MyViewController alloc]
                              initWithNibName:@"MyView" bundle:nil];
    [self.view addSubview:myViewController.view];

    //---comment out this section---
    /*
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Action invoked!"
                         message:@"Button clicked!"
                         delegate:self
                         cancelButtonTitle:@"OK"
                         otherButtonTitles:nil];

    [alert show];
    [alert release];
    */
}

- (void)dealloc {
    [myViewController release];
    [label release];
    [super dealloc];
}
```

2. Declare a btnClicked: action in the MyViewController.h file:

```objective-c
#import <UIKit/UIKit.h>

@interface MyViewController : UIViewController {

}

- (IBAction) btnClicked:(id) sender;

@end
```
