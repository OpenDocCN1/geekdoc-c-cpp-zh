
## Loading a Web Page in a Browser

Loading a URL (Uniform Resource Locator) into a Web browser is one of the most common Internet-related tasks that you'll want to perform. It comes in handy for directing users to online documentation, to a download page where they can get the latest version of your application, or even to your Web-based store to purchase software.

Because viewing Web pages is a task that you perform so frequently, Cocoa provides a class to handle the dirty work for you: `NSWorkspace`. The `NSWorkspace` class gives users easy access to miscellaneous utilities. Every application has one, and only one, `NSWorkspace` object. By calling the `openURL:` method of the `NSWorkspace` instance, you can load and view a URL with the default Web browser.

To use your application's `NSWorkspace` instance, and, more important, its `openURL:` method, use code like this:

```objectivec
[[NSWorkspace sharedWorkspace] openURL:theURL];
```

This code snippet works by calling the `sharedWorkspace` class method of `NSWorkspace`. From there, it's a simple matter of calling the `openURL:` method and passing it a valid URL in the form of an `NSURL`. The `NSURL` class lets you wrap a traditional URL in a Cocoa object. You can define an `NSURL` with a hard-coded URL:

```objectivec
NSURL *theURL = [NSURL URLWithString:@"http://www.wiley.com"];
```

If you want users to supply the URL in an `NSTextField` (with a `theURLField` outlet) in your app's interface, you might do something like this instead:

```objectivec
NSURL *theURL = [NSURL URLWithString:[theURLField stringValue]];
```

Because `openURL:` returns a Boolean value, you can determine whether the command executed successfully. For example, if you create a `loadWebPage:` action, the code might look like this:

```objectivec
- (IBAction)loadWebPage:(id)sender {
    NSURL *theURL = [NSURL URLWithString:[theURLField stringValue]];
    
    if ([[NSWorkspace sharedWorkspace] openURL:theURL]) {
        NSLog(@"URL Loaded");
    }
}
```

If the `openURL:` method performs as it should, the code displays a `URL Loaded` message on the screen.

## Downloading Files

Another important feature that you may want to add to your Cocoa applications is the capability to download files from the Internet without using a browser. You can use download functionality for a variety of situations:

- Offer instant one-click access to the latest version of your application on the Web.
- Download and display HTML help files from your Web site.
- Retrieve a file from the Web that lists the current version of your application.

Cocoa makes it easy to offer all these features and more. With only two lines of code, you can download a file from the Web to your hard drive. This example loads the *For Dummies* home page:

```objectivec
NSURL *theURL = [NSURL URLWithString:@"http://www.dummies.com"];
NSData *pageData = [theURL resourceDataUsingCache:YES];
```

Like the browser code from earlier in this chapter, you first define an `NSURL`. In this example, the URL is hard-coded to www.dummies.com. Although hard-coding may suffice for some purposes, other times you'll want to be more flexible in your approach to creating a URL. Because the `URLWithString:` parameter is an `NSString`, you can use any of the usual `NSString` functions with it, including retrieving the URL from the interface.

![](img/ea40cad434a338535474e82c1a6ace20_300_0.png)

Don't forget that an `NSURL` doesn't necessarily have to point to a file somewhere on the Web. It can also point to a file on your local hard drive. For example, you can use the `initFileURLWithPath:` method of `NSURL` to build a URL to a local file, based on its path. Check the built-in Cocoa documentation in Xcode to see the complete list of `NSURL` methods.

After you create and define an `NSURL`, call its `resourceDataUsingCache:` method to begin downloading the file into memory. In the preceding code snippet, `pageData` points to data in memory. From there, transferring that data from memory to a file on your hard drive is a simple matter. For example, if you want to save a simple HTML document to your desktop, call the `writeToFile:` method of the `NSData` class.

If you pass a relative path (for example, `~/Downloads/download.html`) to the `writeToFile:` method, you must expand it into a full URL with the `stringByExpandingTildeInPath` method:

```objectivec
if ([pageData writeToFile:[@"~/Downloads/download.html"
    stringByExpandingTildeInPath]
    atomically:YES]) {
    NSLog(@"download successful");
}
```

One shortcoming of this download-and-save-to-disk approach is that it functions in a synchronous manner. Your application won't do anything else until the file has finished downloading. This may suffice for small downloads, but larger downloads become troublesome. The solution is to use the `loadResourceDataNotifyingClient:usingCache:` method instead of `resourceDataUsingCache:`:

```objectivec
[theURL loadResourceDataNotifyingClient:self
    usingCache:YES];
```

This method enables you to perform other functions while downloading the file. If you implement the `URLResourceDidFinishLoading:` method, Cocoa notifies you when the download finishes, giving you the chance to access the data. For example, to save the download to an HTML file on the desktop, implement the `URLResourceDidFinishLoading:` method like this:

```objectivec
- (void)URLResourceDidFinishLoading:(NSURL *)sender {
    NSData *pageData = [sender resourceDataUsingCache:YES];
    if ([pageData writeToFile:[@"~/Downloads/download.html"
        stringByExpandingTildeInPath] atomically:YES]) {
        NSLog(@"download successful");
    }
    else {
        NSLog(@"download failed");
    }
}
```

Just because you're downloading and saving an HTML file in this example doesn't mean that you're limited to HTML downloads. You can download any kind of file that you want. To download a JPG image, for instance, simply change the URL and name of the destination file to indicate that it's a JPG file:

```objectivec
NSURL *theURL = [NSURL
    URLWithString:@"http://purplee.net/images/cocoa_cover.jpg"];
...
```

```objectivec
if ([pageData writeToFile:[@"~/Downloads/download.jpg"
    stringByExpandingTildeInPath]
    atomically:YES])
...
```

# Building a Web Browser

You could use the code from earlier in this chapter to download an HTML file from the Web and display it with a Cocoa control. Doing so is possible, but it requires a lot of work. Fortunately, the WebKit Framework gives you the ability to load and display Web content very easily. So easily in fact, you can do so without writing a single line of code.

At the heart of the WebKit is the `WebView` control, which has built-in methods for a variety of Web-related functions that you’d find in a typical Web browser:

- Load a Web page
- Go back one page in the history
- Go forward one page in the history
- Reload a Web page
- Stop a Web page from loading
- Print a Web page

Are some of these functions sounding familiar? They should because not only are they the staple of most Web browsers, but they’re used in Apple’s own Safari Web browser. Safari uses the same exact rendering features that are available to you with WebKit. And because these functions are so common, WebKit has them ready to go without nary a line of code.

To see how the WebKit Framework works, create a new Cocoa application project in Xcode (see Chapter 2). Then, add the WebKit Framework to the project by following these steps:

1. Control-click the Frameworks Group in the project window, as shown in Figure 15-1, and then choose Add > Existing Frameworks from the menu.
2. Navigate to `/System/Library/Frameworks/WebKit.framework` and click the Add button, as shown in Figure 15-2.
   The WebKit Framework enables the powerful `WebView` control. Because the framework isn’t used in most projects, it isn’t part of a standard Cocoa project. Believe it or not, this is all you need to do in Xcode!
3. Double-click the `MainMenu.xib` file in the Xcode project to open it in Interface Builder.
