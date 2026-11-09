
```objc
- (void)connectionDidFinishLoading:(NSURLConnection *)connection
{
    // Process the data here
}
```

Key features of the code include:

- The connection requires two objects: a URL request and a URL connection.
- The NSURLRequest object defines the properties of the connection, including the URL and the timeout interval. If the request doesn't complete before the end of the timeout interval, the request fails.
- The request object also defines the caching policy. Here, the cache is set to reload at every attempt because caching API returns can be risky, especially if the remote data is transient.
- The request is passed to an NSURLConnection object, which initiates the connection. It specifies a delegate object for the connection, which monitors the connection status and receives data as it arrives.
- Four delegate methods manage the connection.
- `connection:didReceiveResponse:` is triggered by an active new connection, and it resets the data receiver object.
- `connection:didReceiveData:` appends data to the data object as it arrives.
- `connection:didFailWithError:` reports an error code.
- `connectionDidFinishLoading:` is triggered after the data has been received successfully.

Although this is byte-level Web access — you can use NSData in a general way to receive data of any format — you can use this code to manage almost any asynchronous Web request.

## Using Cocoa’s XML classes

Cocoa’s XML implementation is complex, partly because XML can be complex. The core class is NSXMLDocument, which can be loaded using the initWithData: method. While it’s possible to extract data into supporting data types such as NSXMLElement and NSXMLNode, this isn’t necessary for a simple task, such as retrieving the text between two tags. It’s possible to scan the XML document directly using a query framework called XPath, which is built into NSXMLDocument.

XPath is a standard Web technology. A JavaScript version is built into all standard Web browsers. An XPath search assumes that the data in an XML file is formatted in a path-like structure. Queries pass a path to the document, and the search returns the data at that path.

![](img/2b293e29fc15b0797f113b85dd429b6e_282_0.png)

### CAUTION

Neither NSXMLDocument nor nodeForXPath: are available on the iPhone. Use NSXMLParser—a dynamic parser class that takes an XML string and triggers various delegate methods as it scans it—instead. NSXMLParser is more lightweight than NSXMLDocument, but less convenient. To extract specific elements, you must add explicit switches or conditional tests to the delegate methods.

Sample code to extract a text string from the url tag follows:

```objc
theDocument = [[NSXMLDocument alloc] initWithData:theData
    options:NSXMLDocumentTidyXML error:&theError];

if (theDocument) {
    // We have a valid document
    NSLog(@"The XML doc: \r%@", theDocument);
    // Get the text string within the url tags
    NSArray *someNodes = [theDocument
        nodesForXPath:@"/response/data/url/text()"
        error:&theError];
    // This is the string we're looking for
    bitlyURL.stringValue = [someNodes objectAtIndex:0];
} else {
    bitlyURL.stringValue = @"Doc error";
    return;
}
```

Key features of the code include:

- The document is created with the NSXMLDocumentTidyXML option, which tidies the document format and can eliminate minor errors.
- The nodesForXPath array returns the elements at the search path.
- Accessing a text() element returns a text object that can be read from the array. No further processing or extraction is required.
- The project code includes a spinner activity indicator, a very simple but effective addition that illustrates the download state.

![](img/2b293e29fc15b0797f113b85dd429b6e_282_1.png)

### TIP

To find the path you need, review the order of the indented tags in the raw XML. XPath can perform many tricks, including reading multiple returns with the same tag. For more information, see the XPath tutorial at www.w3schools.com/xpath/xpath_examples.asp.

## Using WebView

No discussion of URLs would be complete without an introduction to WebView, Cocoa’s Web browser. You can use WebView to add a browser window to any application, with full control over the URL, the size of the window — scroll bars appear automatically, as needed — and standard browser features such as forward and back buttons.

Create a new project, and save it as WebView. Right-click Frameworks, select WebKit.framework from the list that appears, and click Add, as shown in Figure 10.14.

### Figure 10.14

Adding the WebKit framework before creating a WebView. WebKit includes a very rich set of features for Web management within Objective-C and JavaScript apps.

![](img/2b293e29fc15b0797f113b85dd429b6e_283_0.png)

In Interface Builder, add a WebView to the Content View object from the library. Set its autosizing options, as shown in Figure 10.15.

Edit the WebViewAppDelegate.h file as follows:

```objective-c
@class WebView;

@interface WebViewAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
    WebView *webView;
}

@property (assign) IBOutlet NSWindow *window;
@property (assign) IBOutlet WebView *webView;

@end
```

### Figure 10.15

Setting the autosizing options for a WebView forces it to follow the window size. If you don’t set this feature, the size of the WebView remains fixed, which is sometimes, but not usually, a desirable property.

![](img/2b293e29fc15b0797f113b85dd429b6e_284_0.png)

Save the file. In IB, link the WebView outlet to the WebView object. Then, edit the WebViewAppDelegate.m file as follows:

```objc
#import "WebViewAppDelegate.h"
#import <WebKit/WebKit.h>

@implementation WebViewAppDelegate

@synthesize window, webView;

- (void)applicationDidFinishLaunching:(NSNotification *)aNotification
{
    WebFrame *mainFrame = [webView mainFrame];
    NSURL *url = [NSURL URLWithString:@"http://www.apple.com"];
    NSURLRequest *aRequest = [NSURLRequest requestWithURL:url];
    [mainFrame loadRequest:aRequest];
}

@end
```

Build and run the application and wait for the page to load. Then click the Store link. You should see the result shown in Figure 10.16.

### Figure 10.16

The WebView running in its window. You can click active links to navigate.

![](img/2b293e29fc15b0797f113b85dd429b6e_285_0.png)

The code is slightly less straightforward than it looks. The key feature is that the `mainFrame` property is the active browser window; a `WebView` is a wrapper for one or more web frames. `mainFrame` is the most important active frame. In most applications you can ignore the others.

`WebView` is a very sophisticated class. You can add browser essentials such as forward, back, and refresh buttons, but you can also implement controlled downloading with various delegate methods. There’s even an `estimatedProgress` method that can drive a progress bar.

As a trivial exercise, you may want to try adding a URL bar and downloading a new page when the user enters a new URL. More sophisticated applications are also possible.

### TIP

Most applications use `WebView` to access Web pages. Because URLs can be local, you can use `WebView` to access local HTML, CSS, or image content.

## Summary

In this chapter, you learned about file paths, URLs, and their similarities and differences. You explored Cocoa’s File Manager class, and you discovered how to compare files and build working open/save panes into your application. You also learned how to load and save data from the local file system, how to create and find valid paths, and how to get started with the file features of Cocoa’s data objects.

Next, you explored NSURL in detail, and you found out how to use URL objects to load online data into Cocoa objects. You experimented with the bit.ly Web API, and you learned how to assemble simple text-based request and complex asynchronous requests that extracted information from an XML return.

Finally, you were introduced to the WebView object in WebKit, and you saw how easy it is to add a simple Web browser to any project.
