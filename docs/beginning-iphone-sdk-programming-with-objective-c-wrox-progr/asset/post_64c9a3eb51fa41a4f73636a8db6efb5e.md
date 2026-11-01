
8. In Xcode, add the following statements that appear in bold to the UsingViews2ViewController.m file:

```objectivec
#import "UsingViews2ViewController.h"

@implementation UsingViews2ViewController
@synthesize segmentedControl;
@synthesize view1, view2;

- (void)viewDidLoad {
    //---add the event handler for the segmented control---
    [segmentedControl addTarget:self action:@selector(segmentChanged:) forControlEvents:UIControlEventValueChanged];
    
    [super viewDidLoad];
}

//---when the segment has changed---
- (IBAction)segmentChanged:(id)sender {
    NSInteger selectedSegment = segmentedControl.selectedSegmentIndex;
    if (selectedSegment == 0) {
        //---toggle the correct view to be visible---
        [self.view1 setHidden:NO];
        [self.view2 setHidden:YES];
    }
    else{
        //---toggle the correct view to be visible---
        [self.view1 setHidden:YES];
        [self.view2 setHidden:NO];
    }
}

- (void)dealloc {
    [segmentedControl release];
    [view1 release];
    [view2 release];
    [super dealloc];
}
```

9. Press Command-R to test the application on the iPhone Simulator.

10. When you tap the First segment, the First View label appears. When you tap the Second segment, you see the Second View label (see Figure 4-15).

![](img/16991b58db5894715c4a443315e06a22_124_0.png)

## How It Works

When the View is loaded, you first wire it up so that when the user taps one of its buttons, it triggers a method. In this case, the method is `segmentChanged:`.

```objectivec
[segmentedControl addTarget:self action:@selector(segmentChanged:)
          forControlEvents:UIControlEventValueChanged];
```

In the `segmentChanged:` method, you determine which button was clicked (via the `selectedSegmentIndex` property of the segmented control) and show and hide the relevant views:

```objectivec
- (IBAction) segmentChanged: (id) sender {
    NSInteger selectedSegment = segmentedControl.selectedSegmentIndex;
    if (selectedSegment == 0) {
        //---toggle the correct view to be visible---
        [self.view1 setHidden:NO];
        [self.view2 setHidden:YES];
    }
    else {
        //---toggle the correct view to be visible---
        [self.view1 setHidden:YES];
        [self.view2 setHidden:NO];
    }
}
```

## Using the Web View

If you want to load Web pages from within your application, you can embed a Web browser in your application through the use of the UIWebView. Using the Web view, you can send a request to load Web content, which is very useful if you want to convert an existing Web application into a native application (such as those written using Dashboard). All you need to do is to embed all the HTML pages into your Resources folder in your Xcode project and load the HTML pages into the Web view during runtime.

> NOTE Of course, depending on how complex your Web applications are, you may have to do some additional work to port your Web application to a native application if it involves server-side technologies such as CGI, PHP, or others.

The following Try It Out shows how to use the Web view to load a Web page.

### Try It Out Loading a Web Page Using the Web View

*Code file [UsingViews3.zip] available for download at Wrox.com*

1. Using Xcode, create a new View-based Application project and name it UsingViews3.
2. Double-click the UsingViews3ViewController.xib file to edit it using Interface Builder.
3. In the View window, add a Web view from the Library (see Figure 4-16). In the Attributes Inspector window for the Web view, check the Scales Page to Fit property.

![](img/16991b58db5894715c4a443315e06a22_125_0.png)

FIGURE 4-16

4. In the UsingViews3ViewController.h file, declare an outlet for the Web view:

```objectivec
#import <UIKit/UIKit.h>

@interface UsingViews3ViewController : UIViewController {
    IBOutlet UIWebView *webView;
}
@property (nonatomic, retain) UIWebView *webView;
@end
```

5. Back in Interface Builder, connect the webView outlet to the Web view.

6. In the UsingViews3ViewController.m file, add the following statements that appear in bold:

```objectivec
#import "UsingViews3ViewController.h"

@implementation UsingViews3ViewController

@synthesize webView;

- (void)viewDidLoad {
    NSURL *url = [NSURL URLWithString:@"http://www.apple.com"];
    NSURLRequest *req = [NSURLRequest requestWithURL:url];
    [webView loadRequest:req];
    [super viewDidLoad];
}

- (void)dealloc {
    [webView release];
    [super dealloc];
}
```

![](img/16991b58db5894715c4a443315e06a22_126_0.png)

7. Press Command-R to test the application on the iPhone Simulator. You should see the application loading the page from Apple.com (see Figure 4-17).

## How It Works

To load the Web view with a URL, you first instantiate an NSURL object with a URL via the URLWithString method:

```objectivec
NSURL *url = [NSURL URLWithString:@"http://www.apple.com"];
```

You then create an NSURLRequest object by passing the NSURL object to its requestWithURL: method:

```objectivec
NSURLRequest *req = [NSURLRequest requestWithURL:url];
```

Finally, you load the Web view with the NSURLRequest object via the loadRequest: method:

```objectivec
[webView loadRequest:req];
```

## Adding Views Dynamically Using Code

Up to this point, all the UIs of your application have been created visually using Interface Builder. Although Interface Builder makes it relatively easy to build your UI using drag-and-drop, sometimes you are better off creating the UI using code. One such instance is when you need to create a dynamic UI, such as for games.

> **NOTE** I know of developers who swear by creating their UI using code. Interface Builder may be easy to use, but it can be confusing to some people. Because you often have more than one way of doing things in Interface Builder, it can create unnecessary complications.

In the following Try It Out, you learn how to create views dynamically from code, which will help you understand how views are constructed and manipulated.

### Try It Out Creating Views from Code

*Code file [UsingViews4.zip] available for download at Wrox.com*

1. Using Xcode, create a View-based Application project and name it UsingViews4.

2. In the UsingViews4ViewController.m file, add the following statements that appear in bold:

```objectivec
#import "UsingViews4ViewController.h"

@implementation UsingViews4ViewController

- (void)loadView {

    //---create a UIView object---
    UIView *view =
    [[UIView alloc] initWithFrame:[[UIScreen mainScreen] applicationFrame]];
    view.backgroundColor = [UIColor lightGrayColor];

    //---create a Label view---
```

One important point to note here is that within the loadView method, you should not get the value of the view property (setting it is all right), like this:

```objectivec
[self.view addSubview: label];   //---this is not OK---
self.view = view;                //---this is OK---
```

Trying to get the value of the view property in this method will result in a circular reference and cause memory overflow.

## Understanding View Hierarchy

As views are created and added, they are added to a tree data structure. Views are displayed in the order that they are added. To verify this, modify the location of the UIButton object you created earlier by changing its location to CGRectMake(10, 30, 300, 50), as in the following:

```objectivec
//---create a Button view---
frame = CGRectMake(10, 30, 300, 50);
UIButton *button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
button.frame = frame;
[button setTitle:@"Click Me, Please!" forState:UIControlStateNormal];
button.backgroundColor = [UIColor clearColor];
button.tag = 2000;
[button addTarget:self action:@selector(buttonClicked:) forControlEvents:UIControlEventTouchUpInside];
```

When you now run the application again, you will notice that the button overlaps the label control (see Figure 4-19) since the button was added last:

```objectivec
[view addSubview:label];
[view addSubview:button];
```

![](img/16991b58db5894715c4a443315e06a22_130_0.png)

FIGURE 4-19

If you want to switch the order in which the views are displayed after they have been added, you can use the exchangeSubviewAtIndex:withSubviewAtIndex: method, like this:

```objectivec
[self.view addSubview:label];
[self.view addSubview:button];

[self.view exchangeSubviewAtIndex:1 withSubviewAtIndex:0];

[button release];
[label release];
```

The preceding statement in bold swaps the order of the Label and Button views. When the application is run again, the Label view will now appear on top of the Button view (See Figure 4-20).

![](img/16991b58db5894715c4a443315e06a22_130_1.png)

FIGURE 4-20
