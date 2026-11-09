works the same way it did before. Stop the running application by using the red Tasks stop sign.

# ## 8.5 Forward Declaration

There’s another solution to the errors we were getting in the previous section: You can use the @class directive in the header file in place of the import statement.

```
```objc
#import <Cocoa/Cocoa.h>
@class WebView;
@interface BrowserController : NSObject {
    WebView *myWebView;
}
@property(assign) IBOutlet WebView *myWebView;
-(IBAction) loadPreviousPage: (id) sender;
@end
```
```

In the BrowserController.h file, the compiler only needs to know that WebView is a legitimate class. It doesn’t need to know anything about it. The @class directive does exactly that. It doesn’t bring in the whole header file that tells us what an object of type WebView can do—we don’t need to know that yet. It just reassures us that a class named WebView exists.

Whenever you use the @class directive in a header file, you will most likely need the corresponding import statement in the implementation file. Go ahead and add it now near the top of the implementation file. While you’re at it, stub out the loadPreviousPage: action.

```
```objc
#import "BrowserController.h"
#import <WebKit/WebKit.h>

@implementation BrowserController

@synthesize myWebView;

-(IBAction) loadPreviousPage: (id) sender{
    NSLog(@"loadPreviousPage");
}

@end
```
```