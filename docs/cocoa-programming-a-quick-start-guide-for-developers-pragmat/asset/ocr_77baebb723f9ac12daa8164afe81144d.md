Open the MobileBrowserViewController nib file, and use the Connections inspector to wire those outlets from the File’s Owner to the corresponding components in the view.³ Save and quit Interface Builder.

Back in Xcode, we want to create a method that can load a URL that we will pass in as a string. Let’s head to the docs for UIWebView and see whether there’s a method that will do what we want.

Hmmm. When I look under Tasks > Loading Content, the closest thing I find is this:

```
```objective-c
- (void)loadRequest:(NSURLRequest *)request
```
```

That’s pretty close, but it takes an NSURLRequest and not a string as its parameter. Let’s follow the link to the NSURLRequest docs and see whether there’s anything there. This time when I look at Tasks > Creating Requests, I find this:

```
```objective-c
+ (id)requestWithURL:(NSURL *)theURL
```
```

It feels as if we’re getting closer, but now we have to figure out how to create an NSURL from a string. Follow the link to the NSURL docs, and look under Tasks > Creating an NSURL. There it is!

```
```objective-c
+ (id)URLWithString:(NSString *)URLString
```
```

Put these together to create our loadURLFromTextField method.⁴ Add this just after the @synthesize line in MobileBrowserViewController.m:

```
Download iPhoneBrowser/MobileBrowser1/Classes/MobileBrowserViewController.m
```

```
```objective-c
- (void) loadURLFromTextField {
    NSURL *url = [NSURL URLWithString:self.address.text];
    NSURLRequest *request = [NSURLRequest requestWithURL:url];
    [self.webView loadRequest:request];
}
```
```

We create the URL using the text property of our text field. We create the URL request from the URL, and then we send the message to the webView outlet to have it load the URL using the request we created.

We’re almost there—we just need somebody to call our loadURLFromTextField after the application launches. In the desktop version, we used the awakeFromNib method. In iPhone development, you often do this as

+   3. We know to use the File’s Owner because of its type.
+   4. Note that we’re using class methods to construct autoreleased instances of the request and the URL. We don’t need to release them ourselves.