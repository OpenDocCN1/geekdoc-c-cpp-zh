+   1. Select the File’s Owner, and connect the backButton outlet to the Back button and the forwardButton outlet to the Forward button.
+   2. Select the web view, and connect its delegate to the File’s Owner.
+   3. Still in the web view, connect the goBack received action to the Back button and the goForward to the Forward button.

Save your work. Now let’s implement the button reset exactly as we did in the desktop browser. Don’t forget to synthesize your properties. Next, we’ll call a method that we create named resetButtons: from the delegate method that tells us when the web page is done loading. In the case of the iPhone, that method is webViewDidFinishLoad:.

```
```objective-c
-(void) resetButtons:(UIWebView *)theWebView {
    [self.backButton setEnabled:[theWebView canGoBack]];
    [self.forwardButton setEnabled:[theWebView canGoForward]];
}
-(void)webViewDidFinishLoad:(UIWebView *)theWebView {
    [self resetButtons:theWebView];
}
```
```

Run the browser, and navigate or enter the URL for a second web page. Once the page loads, the Back button should be enabled. Click the Back button; you will be taken to the previous page, and the Forward button will be enabled. We have a basic web browser working on the iPhone.

# 10.8  Exercise: Adding an Activity Indicator

Add a UIActivityIndicatorView to your application. In Interface Builder, set its Style to Large White, and select the Hide When Stopped checkbox.

Your activity indicator should spin while the website is loading. The web view should remain disabled until the page is done loading. Finally, if you navigate to a page, the text field should display the URL of this page instead of continuing to contain the last web address the user typed in.