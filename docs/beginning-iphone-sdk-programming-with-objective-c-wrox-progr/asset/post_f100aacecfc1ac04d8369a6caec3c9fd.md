
![](img/16991b58db5894715c4a443315e06a22_72_0.png)

## Outlets, Actions, and View Controllers

### WHAT YOU WILL LEARN IN THIS CHAPTER

- How to declare and define outlets
- How to declare and define actions
- How to connect outlets and actions to the views in your View window
- How to add a new View Controller to your application

In the previous chapter, you built a simple Hello World! iPhone application without understanding much of the underlying details of how things work together. In fact, one of the greatest hurdles in learning iPhone programming is the large number of details you need to learn before you can get an application up and running. This book aims to make the iPhone programming experience both fun and bearable. Hence, this chapter starts with the basics of creating an iPhone application. You learn about the various files that make up an iPhone application project, as well as how your code is connected with the graphical widgets you see on an iPhone application.

## BASIC CODE AND UI INTERACTIONS

A View-based Application project is a good starting point for developing a single-view application and provides an excellent opportunity for you to understand some of the important concepts in iPhone programming, so that's what you'll work with in this section. You will need to download the code.

To start, launch Xcode and create a new View-based Application project (see Figure 3-1) and name it BasicUI.

Codefile [BasicUI.zip] available for download at Wrox.com

![](img/16991b58db5894715c4a443315e06a22_73_0.png)

### FIGURE 3-1

Xcode displays the list of files in the project (see Figure 3-2).

![](img/16991b58db5894715c4a443315e06a22_73_1.png)

### FIGURE 3-2

As you can see, many files are created for you by default when you create a new project. The iPhone SDK tries to make your life simple by creating some of the items that you will use most often when you develop an iPhone application. Table 3-1 describes the use of the various files created in the project.

### TABLE 3-1: The Various Files Created in the Project

| FILE | DESCRIPTION |
|---|---|
| BasicUI.app | The application bundle (executable), which contains the executable as well as the data that is bundled with the application. |
| BasicUI_Prefix.pch | Contains the prefix header for all files in the project. The prefix header is included by default in the other files in the project. |
| BasicUIAppDelegate.h | Headers file for the application delegate. |
| BasicUIAppDelegate.m | Implementations file for the application delegate. |
| BasicUIViewController.h | Headers file for a View Controller. |
| BasicUIViewController.m | Implementations file for a View Controller. |
| BasicUIViewController.xib | The XIB file containing the UI of a view. |
| CoreGraphics.framework | C-based APIS for low-level 2D rendering. |
| Foundation.framework | APIs for foundational system services such as data types, XML, URL, and so on. |
| Info.plist | A dictionary file that contains information about your project, such as icon, application name, and others; information is stored in key/value pairs. |
| main.m | The main file that bootstraps your iPhone application. |
| MainWindow.xib | The XIB file for the main window of the application. |
| UIKit.framework | Provides fundamental objects for constructing and managing your application's UI. |

> NOTE The numbers and types of files created are dependent on the type of project you have selected. The View-based Application template is a good starting point to understanding the various files involved.

The main.m file contains code that bootstraps your application. It contains the following code, and you rarely need to modify it:

```
#import <UIKit/UIKit.h>

int main(int argc, char *argv[]) {
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
    int retVal = UIApplicationMain(argc, argv, nil, nil);
    [pool release];
    return retVal;
}
```

Most of the hard work is done by the UIApplicationMain() function, which examines the Info.plist file to obtain more information about the project. In particular, it looks at the main nib file you will use for your project. Figure 3-3 shows the content of the Info.plist file. Notice that the Main nib file base name key is pointing to MainWindow, which is the name of the NIB file to load when the application is started.

### WHAT DO XIB AND NIB STAND FOR?

In your journey of iPhone application development, you will always come across files with the .xib extension (sometimes also known as NIB files). So, what do the NIB and .xib stand for, exactly? To understand this, a little history lesson is in order. Turns out that the current Mac OS X was built upon an operating system called NeXTSTEP, from a company known as NeXT (founded by Apple’s cofounder, Steve Jobs, in 1985). The N in NIB stands for NeXTSTEP. As for .xib, the x in presumably stands for XML, because its content is saved as an XML file. The IB stands for Interface Builder, the application that allows you to visually construct the UI for your application.

![](img/16991b58db5894715c4a443315e06a22_75_0.png)

## Editing XIB Files

Double-click the MainWindow.xib file to edit it using Interface Builder. As mentioned, the XIB file represents the UI of your application, and it is used almost exclusively by Interface Builder.

> **NOTE** An XIB file is actually an XML file. You can view and edit it using applications such as TextEdit. However, most of the time, you use Interface Builder to visually modify the UI of your applications.

When the MainWindow.xib file is opened by Interface Builder, you see a window with the same title as the name of the file (see Figure 3-4).

This window contains five items:

- The File's Owner item represents the object that is set to the owner of the user interface (i.e., the class that is responsible for managing the content of the XIB file).
- The First Responder item represents the object that the user is currently interacting with. Chapter 4 discusses first responder objects in more detail.
- The BasicUI App Delegate item points to the BasicUIAppDelegate class. (More on this topic shortly.)
- The BasicUI View Controller item points to a View Controller that you will be using to display your UI.
- The Window item is the screen that you will see when the application is launched.

![](img/16991b58db5894715c4a443315e06a22_76_0.png)

### FIGURE 3-4

## Delegates

The BasicUIAppDelegate.m file contains code that is typically executed after the application has finished loading, or just before it is being terminated. For this example, the content of it is as follows:

```
#import "BasicUIAppDelegate.h"
#import "BasicUIViewController.h"

@implementation BasicUIAppDelegate

@synthesize window;
@synthesize viewController;

- (void)applicationDidFinishLaunching:(UIApplication *)application {
    // Override point for customization after app launch
    [window addSubview:viewController.view];
    [window makeKeyAndVisible];
}

```

When the application has finished launching, it sends its delegate the applicationDidFinishLaunching: message. In the preceding case, it uses a View Controller to obtain its view and then adds it to the current window so that it can be displayed.

The BasicUIAppDelegate.h file contains the declaration of the members of the BasicUIAppDelegate class:

```
#import <UIKit/UIKit.h>

@class BasicUIViewController;

@interface BasicUIAppDelegate : NSObject <UIApplicationDelegate> {
    UIWindow *window;
    BasicUIViewController *viewController;
}

@property (nonatomic, retain) IBOutlet UIWindow *window;
@property (nonatomic, retain) IBOutlet BasicUIViewController *viewController;

@end
```

Of particular interest is this line:

```
@interface BasicUIAppDelegate : NSObject <UIApplicationDelegate> {
```

The <UIApplicationDelegate> statement specifies that the class implement the UIApplicationDelegate protocol. Put simply, it means that you can now handle events (or messages) defined in the UIApplicationDelegate protocol. Examples of events in the UIApplicationDelegate protocol are the following:

- `applicationDidFinishLaunching:` (You saw this implemented in the BasicUIAppDelegate.m file.)
- `applicationWillTerminate:`
- `applicationDidReceiveMemoryWarning:`

> **NOTE** Protocols are discussed in more detail in Appendix D.

## View Controllers

In iPhone programming, you typically use a View Controller to manage a view as well as perform navigation and memory management. In the project template for a View-based Application, Xcode automatically uses a View Controller to help you manage your view. Think of a view as a screen (or window) you see on your iPhone.

> **NOTE** This section is an introduction to the basics of View Controllers; Chapter 7 covers more advanced View Controller topics and includes multi-view application instructions.
