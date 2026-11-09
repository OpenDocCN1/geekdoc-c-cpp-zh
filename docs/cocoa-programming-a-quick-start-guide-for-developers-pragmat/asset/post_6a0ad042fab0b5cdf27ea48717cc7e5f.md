
Once you've removed these, you'll need to refactor the awakeFromNib method to pass the URL to the web view without going through one of the methods we just deleted. Here's the current state of the implementation file:

```objective-c
#import "BrowserController.h"
#import <WebKit/WebKit.h>

@implementation BrowserController

@synthesize myWebView, address, backButton, forwardButton;

- (void)resetButtons {
    [self.backButton setEnabled:[self.myWebView canGoBack]];
    [self.forwardButton setEnabled:[self.myWebView canGoForward]];
}

- (void)awakeFromNib {
    [self.address setStringValue:@"http://pragprog.com"];
    [self.myWebView takeStringURLFrom:self.address];
}

- (void)webView:(WebView *)sender
 didReceiveTitle:(NSString *)title
        forFrame:(WebFrame *)frame {
    [[sender window] setTitle:title];
}

- (void)webView:(WebView *)sender
 didFinishLoadForFrame:(WebFrame *)frame {
    [self.address setStringValue:[sender mainFrameURL]];
    [self resetButtons];
}
@end
```

Here's the current header file:

```objective-c
#import <Cocoa/Cocoa.h>
@class BrowserController;
@interface BrowserController : NSObject {
    NSTextField *address;
    NSButton *backButton;
    NSButton *forwardButton;
    WebView *myWebView;
}
@property(assign) IBOutlet NSButton *backButton;
@property(assign) IBOutlet NSButton *forwardButton;
@property(assign) IBOutlet NSTextField *address;
@property(assign) IBOutlet WebView *myWebView;
@end
```

Take a minute to look at how little code we need when we work *with* the existing Apple frameworks. Whenever your code gets long and complicated, you should pause and consider whether there’s an easier way to accomplish what you are trying to do. Your goal is to write simple code that is clear and understandable. Cocoa programmers do not value code that is short and clever to the point of being obscure.

## 9.12 Exercise: Adding a Progress Indicator

A lot of what we’re doing at this point is adding muscle memory as we jump back and forth between Xcode and Interface Builder. Let’s take this example one step further—at least on the desktop.

Add a small circular progress indicator to the top-right side of your browser. It should be initially hidden. When a user enters a new URL or navigates to a different page, the progress indicator should appear and start to spin. We want to give the user some feedback that something is happening. Once the page has fully loaded, the progress indicator should stop spinning and should be hidden again.

Think through the steps. You need to place a progress indicator using IB. You need to add an outlet for that indicator in the BrowserController header file and then connect it in IB. You need to synthesize the property you just created and use it when the page starts and stops loading.

## 9.13 Solution: Adding a Progress Indicator

You can look at the solution provided in the code download to investigate the nib and header file. Here’s the Attributes inspector settings for the progress indicator:

![](img/9355405953264484a02198b0e3d25b7e_172_0.png)

Under Behavior, I’ve unselected Display When Stopped, and under Drawing, I’ve unselected Hidden.

Here’s the final version of the implementation file. We need to add a couple of lines of code to the webView:didFinishLoadForFrame: method to stop the progress bar’s animation and hide it. We also need to unhide the progress indicator and start it spinning in the webView:didStartProvisionalLoadForFrame: method.

```objective-c
#import "BrowserController.h"
#import <WebKit/WebKit.h>

@implementation BrowserController

@synthesize myWebView, address, backButton, forwardButton, progress;

- (void)resetButtons {
    [self.backButton setEnabled:[self.myWebView canGoBack]];
    [self.forwardButton setEnabled:[self.myWebView canGoForward]];
}

- (void)awakeFromNib {
    [self.address setStringValue:@"http://pragprog.com"];
    [self.myWebView takeStringURLFrom:self.address];
}

- (void)webView:(WebView *)sender
 didReceiveTitle:(NSString *)title
        forFrame:(WebFrame *)frame {
    [[sender window] setTitle:title];
}

- (void)webView:(WebView *)sender
 didFinishLoadForFrame:(WebFrame *)frame {
    [self.address setStringValue:[sender mainFrameURL]];
    [self resetButtons];
    [self.progress stopAnimation:self];
}

- (void)webView:(WebView *)sender
 didStartProvisionalLoadForFrame:(WebFrame *)frame {
    [self.progress startAnimation:self];
}
@end
```

That’s still not much code. In the next chapter, we’ll see what needs to be changed to implement our SimpleBrowser for the iPhone.

More formally, when the browser application starts up, an instance of the UIApplication class is created, and the MainWindow nib is loaded.²

![](img/9355405953264484a02198b0e3d25b7e_175_0.png)

![](img/9355405953264484a02198b0e3d25b7e_175_1.png)

The nib contains an object that represents the application whose delegate outlet is connected to the MobileBrowserAppDelegate. The nib file also contains the MobileBrowserViewController. In the app delegate's applicationDidFinishLaunching: method, the view controller's view is added to the window.

```objective-c
BrowserAppDelegate.m

- (void)applicationDidFinishLaunching:(UIApplication *)application {
    // Override point for customization after app launch
    [window addSubview:viewController.view];
    [window makeKeyAndVisible];
}
```

This is the way most iPhone apps work. They have a single window for the entire application. What you think of as a screen are the contents of a view, and when you switch from one screen to another using the tab bar, nav bar, or some other means, you are replacing the window's old view with the new view by working with their view controllers.

Generally, each of these top-level views is contained in its own nib file with its view controller as the File's Owner. I'm not going to talk about the File's Owner yet. Let's just say that most of our work for this application will happen in the second nib file and in the view controller.

A view controller's job, as you might have guessed, is to control a view. While the view is all about appearance, the controller defines the behavior. To start with, as you saw in the applicationDidFinishLaunching: method, when you want to add a view to a window as its subview, you ask the view controller for the view it controls. Once everything is arranged, you can reveal the window and its contents to the user and set it to accept touches and other input.

2\. iPhone-specific classes often begin with UI and not NS as you saw in desktop applications.

We're not going to customize the application's behavior at launch time, so let's move our attention to the nib containing the view and its controller to create our web browser.

## 10.2 Creating the Look of Our Browser

Double-click MobileBrowserViewController.xib to open it in IB. We're going to transform this empty view into something that looks like this:

![](img/9355405953264484a02198b0e3d25b7e_176_0.png)

As before, you drag components out of the library and position them on the view. Place a UIToolbar at the top of the view. Drag a UITextField on top of it to the left of the UIBarButtonItem that was at the left of the UIToolbar. Drag another UIBarButtonItem and place it to the right of the text field. In our desktop version, we had room for the words *Forward* and *Back*. Here we'll borrow images provided for audio interfaces. Open the inspector.

It looks a little different than the inspector window when you are creating Mac OS X applications. You have four tabs that you'll use to inspect and change the attributes, connections, size, and identity. Choose the Attributes inspector for the Back button.

![](img/9355405953264484a02198b0e3d25b7e_177_0.png)

Use the pull-down menu to set Identifier to Rewind. While you're at it, unselect the Enabled checkbox so that initially the user can't click the Back button. Similarly, set the Forward button's Identifier to Fast Forward, and unselect the Enabled checkbox.

Lastly, select a UIWebView, and position it to occupy all of the view below the toolbar. Open the Attributes inspector for the web view, and check the box Web View > Scales Page to Fit. Save your work. That's our interface for now.

Let's click Build & Run and see what happens. Our app should start up fine. The Forward and Back buttons are disabled. Try to enter a URL. Click the text field. This looks promising. The text field clears, and the keypad appears. You can type in a new URL.

Now what?

You hit ↵, and nothing happens. If you click in another area of the screen, the keyboard is dismissed, but the next time you select the text field, the URL will be cleared, and you need to start all over again. How can you enter a URL and navigate to the site? It turns out, we're going to need two more delegates.

## 10.3 The WebView's Limitations

A UIWebView can't do as much as the WebView that we looked at before. You can see that in the Connections inspector for our UIWebView.
