# Figure 10.15

Setting the autosizing options for a WebView forces it to follow the window size. If you don’t set this feature, the size of the WebView remains fixed, which is sometimes, but not usually, a desirable property.

![](bbox=[0.268, 0.217, 0.79, 0.572])

Save the file. In IB, link the WebView outlet to the WebView object. Then, edit the WebViewAppDelegate.m file as follows:

```
```objc
#import "WebViewAppDelegate.h"
#import <WebKit/WebKit.h>
@implementation WebViewAppDelegate
@synthesize window, webView;
- (void)applicationDidFinishLaunching:(NSNotification *)
    aNotification {
        WebFrame *mainFrame = [webView mainFrame];
        NSURL *url = [NSURL URLWithString:@"http://www.apple.com"];
        NSURLRequest *aRequest = [NSURLRequest requestWithURL:url];
        [mainFrame loadRequest: aRequest];
}
```
```

Build and run the application and wait for the page to load. Then click the Store link. You should see the result shown in Figure 10.16.