
## Chapter 8 Creating a Controller

You can’t accomplish everything you want your application to do just by dragging connections between the visual elements in Interface Builder. On the one hand, it’s pretty amazing how easily we created a simple web browser in Chapter 2, Using What’s There, on page 24 just using visual tools. On the other hand, the browser leaves a lot to be desired. There are some things we’re just going to need to code ourselves.

In this chapter, we’ll create a controller for our SimpleBrowser example. To keep things simple, we won’t have a model—we’ll just have a view and a controller. The main point of this example is creating a new class and instantiating it to communicate with objects you created in Interface Builder.

### 8.1 How We’ve Created Objects

We have created and connected objects in two different ways. In the SimpleBrowser example, all of our objects are created in the nib. We dragged in buttons, a text field, and a web view, and they joined the SimpleBrowserAppDelegate and all of the other objects that are created in the nib.

![](img/9355405953264484a02198b0e3d25b7e_141_0.png)

There is effectively no code for this application. All of the connections between the objects have been made in Interface Builder. Here are the actions that the web view receives. It gets the goBack: message from the Back button, the goForward: message from the Forward button, and the takesStringURLFrom: message from the text field.

![](img/9355405953264484a02198b0e3d25b7e_141_1.png)

Contrast this with the “Hello, World!” application we built in Chapter 4, *Classes and Objects*, on page 62. There we created a text field in code in our application delegate. We then created a custom Greeter. We instantiated it in code in our app delegate, and all of our communication among the objects we created was in code.

In Chapter 7, *Outlets and Actions*, on page 124, you learned how to connect code that you created with objects that were created in Interface Builder. If you needed to talk to a widget from your code, you created an outlet for that widget in your header file and then connected the

At first, this will feel a bit odd. After all, you are creating an instance of a class that this book gives you a visual representation using a tool named *Interface Builder*. In no time, this will feel completely natural to you.

### 8.3 Creating an Instance of Our Controller in IB

We’re now going to create an instance of the BrowserController class in Interface Builder.^2

When we created instances of our buttons, we just looked in the Library for an NSButton that looked like the one we wanted and dragged it into our window. We can’t do that with our BrowserController because there’s no way that Interface Builder’s Library would contain our BrowserController class—we just made it up. Fortunately, Snow Leopard and Xcode 3.2 have made this a lot easier for us.^3

Double-click MainMenu.xib to open the nib file in IB. You aren’t interested in the Window view anymore because there is no visual representation of the controller for the end user to see. Instead, bring up the Document window in Interface Builder with the key sequence ⌘0 or Window > Document.

Interface Builder provides us with a representation of our BrowserController object. In IB, go to the Library, and this time choose the Classes tab and look for BrowserController.

2. Actually, the instance isn’t really created until the nib is unarchived when the application starts up. We can think of the instance being created at this point in the same way we talked about creating an object in code when we learned to use a call like this `[[BrowserController alloc] init]`.

3. If you are running an earlier version of Xcode, you will need to adjust the directions that follow so that you drag an NSObject into the Document window and change its type using the Identity Inspector.

BrowserController in the nib. Here is the icon view of your Document window with the newly added instance of the BrowserController:

![](img/9355405953264484a02198b0e3d25b7e_145_0.png)

I prefer using the list view but wanted to show you this view in case you like it better.

### 8.4 Declaring an Outlet and an Action

Right now the Back button is connected to the web view's goBack: method. Let's insert the BrowserController in between. We're going to need a method in the controller that we use for loading the previous web page. It will be called by the Back button and will, in turn, have to send the message goBack: to the web view. This means we'll need an outlet for the web view and an action for the method.

Back in Xcode, add an IBAction named loadPreviousPage: to BrowserController.h. You'll also need to add an IBOutlet named myWebView using an instance variable and a property.^4 The myWebView variable is a pointer to a WebView object.

![](img/9355405953264484a02198b0e3d25b7e_145_1.png)

4. If you are using and are targeting 64-bit, you can create your property without declaring the instance variable.

With this set up, when the Back button is clicked, the loadPreviousPage: method will be called on the BrowserController object. The loadPreviousPage: method will call the goBack: method on the myWebView variable. Since the myWebView variable is also an outlet that is connected to the WebView object, this has the effect of calling the goBack: method on this WebView object. You can read more about objects and actions in Apple’s *Communicating with Objects* [App08c].

Remember to synthesize myWebView in the implementation file. Here’s the header:

![](img/9355405953264484a02198b0e3d25b7e_146_0.png)

```objective-c
#import <Cocoa/Cocoa.h>

@interface BrowserController : NSObject {
    WebView *myWebView;
}
@property(assign) IBOutlet WebView *myWebView;

-(IBAction) loadPreviousPage: (id) sender;

@end
```

Before you hit Build & Run, can you see any problems? If you can, fix them. If not, I’ll explain how in a minute. Hit Build & Run, and you should get the message “Build failed (9 errors, 6 warnings).” In the bottom right of your open window, you should see this:

![](img/9355405953264484a02198b0e3d25b7e_146_1.png)

You can click Failed, the yellow triangle with the exclamation point that indicates warnings, or the red circle with the ! that indicates errors to take you to a window that contains more details about what went wrong. These three errors and two warnings are repeated three times:

![](img/9355405953264484a02198b0e3d25b7e_146_2.png)

Let’s deal with the error first. Your IBOutlet uses the WebView class. But your program doesn’t know anything about the WebView class. You have to import the appropriate header file. At the top of the WebView docs, you can see that it is part of the WebKit framework and is declared in WebView. One solution is to add this import to BrowserController.h below the line importing the Cocoa headers:

```objc
#import <Cocoa/Cocoa.h>
#import <WebKit/WebKit.h>
@interface BrowserController : NSObject {
    WebView *myWebView;
}
@property(assign) IBOutlet WebView *myWebView;
-(IBAction) loadPreviousPage: (id) sender;
@end
```

### Joe Asks…

**What’s the Difference Between a Warning and an Error?**

An error means that there is something that keeps your code from compiling. It’s a showstopper. Your code won’t compile, so there’s no app to run. You don’t have any choice but to fix errors.

A warning lets you know there may be a problem, but it wasn’t severe enough to keep your code from compiling. This could mean that everything will be fine, or it could mean that you end up with a runtime error. A warning could be a note at compile time telling you that you’ve sent a message to an object that didn’t declare a method with that signature. It doesn’t mean that the object can’t handle the message, just that the compiler can’t verify that the object can.

It is easy to ignore warnings. Your code compiles—why worry? Some experienced developers think that it’s too easy to ignore these warnings, so they select the option that Treat Warnings as Errors.

Select the menu item Project > Edit Project Settings, go to the Build tab, and select the Treat Warnings as Errors checkbox. Search on the word treat.

Click Build & Run again. This time the build will succeed. There will be two unique warnings because the header file promised there would be a method named loadPreviousPage and we haven’t implemented it yet. Even with this unfinished work, the program builds and launches and
