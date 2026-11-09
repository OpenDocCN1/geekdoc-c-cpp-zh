Once you've removed these, you'll need to refactor the awakeFromNib method to pass the URL to the web view without going through one of the methods we just deleted. Here's the current state of the implementation file:

```
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
```

Here's the current header file:

```
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
```