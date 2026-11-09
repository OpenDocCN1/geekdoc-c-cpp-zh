With this set up, when the Back button is clicked, the loadPreviousPage: method will be called on the BrowserController object. The loadPreviousPage: method will call the goBack: method on the myWebView variable. Since the myWebView variable is also an outlet that is connected to the WebView object, this has the effect of calling the goBack: method on this WebView object. You can read more about objects and actions in Apple’s *Communicating with Objects* [App08c].

Remember to synthesize myWebView in the implementation file. Here’s the header:

![](bbox=[0.136, 0.278, 0.511, 0.3])

```
```objective-c
#import <Cocoa/Cocoa.h>

@interface BrowserController : NSObject {
    WebView *myWebView;
}
@property(assign) IBOutlet WebView *myWebView;

-(IBAction) loadPreviousPage: (id) sender;

@end
```
```

Before you hit Build & Run, can you see any problems? If you can, fix them. If not, I’ll explain how in a minute. Hit Build & Run, and you should get the message “Build failed (9 errors, 6 warnings).” In the bottom right of your open window, you should see this:

![](bbox=[0.136, 0.576, 0.288, 0.599])

You can click Failed, the yellow triangle with the exclamation point that indicates warnings, or the red circle with the ! that indicates errors to take you to a window that contains more details about what went wrong. These three errors and two warnings are repeated three times:

![](bbox=[0.136, 0.709, 0.725, 0.834])

Let’s deal with the error first. Your IBOutlet uses the WebView class. But your program doesn’t know anything about the WebView class. You have to import the appropriate header file. At the top of the WebView docs, you can see that it is part of the WebKit framework and is declared in