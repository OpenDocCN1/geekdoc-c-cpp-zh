```
@implementation UsingViews2ViewController

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

7. Press Command-R to test the application on the iPhone Simulator. You should see the application loading the page from Apple.com (see Figure 3-19).

![](bbox=[0.18, 0.52, 0.55, 0.9])

FIGURE 3-19