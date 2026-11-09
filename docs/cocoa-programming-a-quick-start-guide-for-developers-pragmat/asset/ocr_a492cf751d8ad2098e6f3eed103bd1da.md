Try implementing this on your own before reading on because the solution is included with the following code.

We’ll need to send messages to the two buttons, so add two outlets to your header file:

```
```objective-c
#import <Cocoa/Cocoa.h>
@class WebView;
@interface BrowserController : NSObject {
    WebView *myWebView;
    NSTextField *address;
    NSButton *backButton;
    NSButton *forwardButton;
}
@property(assign) IBOutlet WebView *myWebView;
@property(assign) IBOutlet NSButton *backButton;
@property(assign) IBOutlet NSButton *forwardButton;
@property(assign) IBOutlet NSTextField *address;

-(IBAction) loadPreviousPage: (id) sender;
-(IBAction) loadNextPage: (id) sender;
-(IBAction) loadURLFrom: (id) sender;
@end
```
```

Save the header file, and move back to Interface Builder’s Document window. Select the Browser Controller, and open the Connections inspector. You should have new outlets labeled backButton and forwardButton. Connect them to their buttons. The Browser Controller should now have four outlets and three received actions.

![](bbox=[0.26, 0.622, 0.652, 0.814])

Before you move on, click the Back button, and open the Attributes inspector (click the leftmost icon at the top of the inspector window). Look most of the way down to find the Enabled checkbox in the Control group. Unselect the check box. Do the same for the Forward button. Save your work. Now your browser will start up with the two buttons disabled.