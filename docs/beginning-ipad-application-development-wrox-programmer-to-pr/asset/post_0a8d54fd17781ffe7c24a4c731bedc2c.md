
![](img/744c5ec15e15ca7891c98be71dc25d13_77_0.png)

FIGURE 2-25

![](img/744c5ec15e15ca7891c98be71dc25d13_77_1.png)

FIGURE 2-26

## 3 Views, Outlets, and Actions

### WHAT YOU WILL LEARN IN THIS CHAPTER:

- How to declare and define outlets
- How to declare and define actions
- How to connect outlets and actions to the views in your View window
- How to use the UIAlertView to display an alert view to the user
- How to use the UIActionSheet to display some options to the user
- How to use the UIPageControl to control paging
- How to use the UIImageView to display images
- How to use the UIWebView to display Web content in your application
- How to add views dynamically to your application during runtime

In the previous chapter, you built a simple Hello World! iPad application without understanding much of the underlying details of how things work together. In fact, one of the greatest hurdles in learning iPad programming is the large number of details you need to learn before you can get an application up and running. This book aims to make the iPad programming experience both fun and bearable. Hence, this chapter starts with the basics of creating the user interface (UI) of an iPad application and how your code connects with the various graphical widgets.

## OUTLETS AND ACTIONS

One of the first things you need to understand in iPad programming is outlets and actions. If you are familiar with traditional programming languages such as Java or C#, this is a concept that requires some time to get used to — the concepts are similar, just that it is a different way of doing things. At the end of this section, you will have a solid understanding of what outlets and actions are and how to create them, and be on your way to creating great iPad applications.

6. Control-click and drag the OK Button view to the File's Owner item (see Figure 3-3). Select the action named `btnClicked:`.

![](img/744c5ec15e15ca7891c98be71dc25d13_83_0.png)

FIGURE 3-3

7. Right-click the OK Button view to display its events (see Figure 3-4). Notice that the Button view has several events, but one particular event — Touch Up Inside — is now connected to the action you specified (`btnClicked:`). Because the Touch Up Inside event is so commonly used, it is automatically connected to the action when you control-click and drag it to the File's Owner item. To connect other events to the action, simply click on the circle displayed next to each event and then drag it to the File's Owner item.

8. That's it! Press Command-R to test the application on the iPhone Simulator. Enter a name in the TextField and tap the OK button. An alert view displays a welcome message (see Figure 3-5).

![](img/744c5ec15e15ca7891c98be71dc25d13_83_1.png)

FIGURE 3-4

![](img/744c5ec15e15ca7891c98be71dc25d13_84_0.png)

FIGURE 3-5

### How It Works

In iPad, you use actions and outlets to connect your code to the various views in your UI. Think of actions as methods in the traditional object-oriented programming world and outlets as objects references. Actions are represented using the IBAction keyword while outlets use the IBOutlet keyword:

```
#import <UIKit/UIKit.h>

@interface OutletsAndActionsViewController : UIViewController {
```

```
//---declaring the outlet---
IBOutlet UITextField *txtName;
}

//---expose the outlet as a property---
@property (nonatomic, retain) UITextView *txtName;

//---declaring the action---
-(IBAction) btnClicked: (id) sender;

@end
```

The IBOutlet identifier is used to prefix variables so that Interface Builder can synchronize the display and connection of outlets with Xcode. The @property keyword indicates to the compiler that you want the txtName outlet to be exposed as a property. The nonatomic keyword indicates that there is no need to ensure that the property is used in a thread-safe manner because it is not used in multiple threads. The default behavior is atomic, and specifying nonatomic actually improves the performance of your application.

> NOTE The IBOutlet tag can also be added to the @property identifier. This syntax is common in the Apple documentation:
> 
> @property (nonatomic, retain) IBOutlet UITextField *txtName;

> NOTE For the use of the nonatomic and retain identifiers, refer to Appendix D, where you can find an introduction to Objective-C, the language used for iPad programming. Also, the @synthesize keyword, discussed shortly, is explained in more detail there as well.

The IBAction identifier is used to synchronize action methods. An action is a method that can handle events raised by views (for example, when a button is clicked) in the View window. An outlet, on the other hand, allows your code to programmatically reference a view on the View window.

Once your actions and outlets are added to the header (.h) file of the View Controller, you then need to connect them to your views in Interface Builder.

When you control-click and drag the File's Owner item to the TextField view and select txtName, you essentially connect the outlet you have created (txtName) with the TextField view on the View window. In general, to connect outlets you control-click and drag the File's Owner item to the view on the View window.

> WARNING A quick tip: to connect outlets to the views, you drag the File's Owner item onto the required view in the View window.

To connect an action, you control-click and drag a view to the File's Owner item. Hence, for the OK Button view, you control-click and drag the OK Button view to the File's Owner item and then select the action named btnClicked.

> **WARNING** A quick tip: to connect actions, you drag from the view in the View window onto the File's Owner item.

In the implementation file (.m), you use the @synthesize keyword to indicate to the compiler to create the getter and setter for the specified property:

> **COMMON MISTAKES** Forgetting to add the @synthesize keyword is one of the most common mistakes that developers make. Remember to add this statement or else you will encounter a runtime error when the application is executed. Appendix D covers getter/setter in more details.

```objc
#import "OutletsAndActionsViewController.h"

@implementation OutletsAndActionsViewController

//---synthesize the property---
@synthesize txtName;

//---displays an alert view when the button is clicked---
-(IBAction) btnClicked:(id) sender {
    NSString *str = [[NSString alloc]
        initWithFormat:@"Hello, %@", txtName.text];
    UIAlertView *alert = [[UIAlertView alloc]
        initWithTitle:@"Hello!"
        message:str
        delegate:self
        cancelButtonTitle:@"Done"
        otherButtonTitles:nil];
    
    [alert show];
    [str release];
    [alert release];
}

- (void)dealloc {
    //---release the outlet---
    [txtName release];
    [super dealloc];
}
```

The btnClicked: action simply displays an alert view with a message containing the user's name. Note that it has a parameter sender of type id. The sender parameter allows you to programmatically find out who actually invokes this action. This is useful when you have multiple views connecting to one single action. For such cases, you often need to know which is the view that invokes this method and the sender parameter will contain a reference to the calling view.

## USING VIEWS

So far, you have seen quite a number of views in action — Round Rect Button, TextField, and Label. All these views are quite straightforward, but they give you a good opportunity to understand how to apply the concepts behind outlets and actions.

To use more views, you can locate them from the Library window in Interface Builder (see Figure 3-6).

![](img/744c5ec15e15ca7891c98be71dc25d13_87_0.png)

FIGURE 3-6

The Library is divided into sections:

- Controllers — Contains views that control other views, such as the View Controller, Tab Bar Controller, Navigation Controller, and so on
- Data Views — Contains views that display data, such as the Image View, Table View, Data Picker, Picker View, and so on
