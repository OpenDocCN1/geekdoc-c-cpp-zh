+   4. In the UsingViews3ViewController.h file, declare an outlet for the Web view:

```
```objc
#import <UIKit/UIKit.h>

@interface UsingViews3ViewController : UIViewController {
    IBOutlet UIWebView *webView;
}

@property (nonatomic, retain) UIWebView *webView;

@end
```
```

+   5. Back in Interface Builder, connect the webView outlet to the Web view.

+   6. In the UsingViews3ViewController.m file, add the following statements that appear in bold:

```
```objc
#import "UsingViews3ViewController.h"

@implementation UsingViews3ViewController

@synthesize webView;

- (void)viewDidLoad {
    NSURL *url = [NSURL URLWithString:@"http://www.apple.
    com"];
    NSURLRequest *req = [NSURLRequest requestWithURL:url];
    [webView loadRequest:req];

    [super viewDidLoad];
}

- (void)dealloc {
    [webView release];
    [super dealloc];
}
```
```

+   7. Press Command-R to test the application on the iPhone Simulator. You should see the application loading the page from Apple.com (see Figure 4-17).

![](bbox=[0.731, 0.398, 0.948, 0.731])

# How It Works

To load the Web view with a URL, you first instantiate an NSURL object with a URL via the URLWithString method:

```
```objc
NSURL *url = [NSURL URLWithString:@"http://www.apple.com"];
```
```

You then create an NSURLRequest object by passing the NSURL object to its requestWithURL: method:

```
```objc
NSURLRequest *req = [NSURLRequest requestWithURL:url];
```
```

Finally, you load the Web view with the NSURLRequest object via the loadRequest: method:

```
```objc
[webView loadRequest:req];
```
```