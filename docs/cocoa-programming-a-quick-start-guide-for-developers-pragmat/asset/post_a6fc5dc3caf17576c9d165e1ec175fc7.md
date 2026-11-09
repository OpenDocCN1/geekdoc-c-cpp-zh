
![](img/9355405953264484a02198b0e3d25b7e_229_0.png)

The ActivityController is a bridge between two worlds. It needs to communicate with the components of the view to display the icon in the image well and a message in the text field. We'll put these components into one nib. The ActivityController object also needs to communicate with the model. We're going to split the nib into these two pieces with the same instance of the ActivityController living in each:

![](img/9355405953264484a02198b0e3d25b7e_229_1.png)

The ActivityView is a cohesive collection of objects. It's the components of the view along with the view controller. The MainMenu.xib can be further split to move the NSWindow into its own nib. We'll need to introduce a window controller to manage our window the same way we use a view controller to manage our view.

![](img/9355405953264484a02198b0e3d25b7e_229_2.png)

The object I’ve positioned at the top of each nib is the File’s Owner. You’ll soon see that the File’s Owner is the object that will connect the new nib file to the rest of the application. So, we’ve broken our single nib into three smaller pieces that are connected via their File’s Owners. Let’s start splitting off our first nib.

## 14.3 Preparing to Split Out the View

Let’s start by splitting out the view. The whole key to this operation is the view controller. We’re going to move the text field and the image well that the view controller controls into a new nib that contains a view. We’ll add this view to the window, but we’re not going to move the window, the model, or the app delegate. Here are the ActivityController’s current connections:

![](img/9355405953264484a02198b0e3d25b7e_230_0.png)

Notice that our ActivityController is connected to four objects that will soon be contained in two different nibs. The trick is to make sure that the same instance of ActivityController will be able to communicate with both nibs. We’ll create the ActivityController in the MainMenu nib and use it as our File’s Owner in our new nib. One of my goals in this exercise is to help you understand the role of the File’s Owner.

We’ve been using the ActivityController as a view controller, but so far it hasn’t extended the NSViewController class. Let’s fix that by changing the superclass in the ActivityController header file:

```objc
#import "MultipleNibs/HelloApplication19/ActivityController.h"

@interface ActivityController : NSViewController <ActivityMonitorDelegate> {
```

Now if you check out the ActivityController’s outlets in the Connections inspector, you’ll see a new view outlet. We’ll use that in the next section when we split this nib in two.

## 14.6 The File’s Owner

One advantage of having small focused nib files like ActivityView.xib is that we can choose a File’s Owner that better fits. Here the nib file is currently the view that we’ll be displaying in the main window, so our File’s Owner will be in charge of managing the view and its contents. The natural choice for the File’s Owner is the ActivityController object we created in MainMenu.xib.

To set the File’s Owner, select File’s Owner in the ActivityView.xib’s Document window. Use the Identity inspector to change the class name of the File’s Owner to ActivityController, and save your work.

![](img/9355405953264484a02198b0e3d25b7e_234_0.png)

Let’s connect up the ActivityController. There are five possible connections. The two reference outlets are connected in MainMenu.xib.

![](img/9355405953264484a02198b0e3d25b7e_234_1.png)

We need to connect the three outlets in ActivityView.xib. Connect the view outlet to the Custom View, the imageView outlet to the NSImageView, and the activityDisplay outlet to the NSTextView.

![](img/9355405953264484a02198b0e3d25b7e_235_0.png)

Your ActivityController object has a foot in both nibs so you can make some of the connections in the first nib and other connections in the second nib. The ActivityController object is the link between these two worlds.

I want to stress an important point here. The File’s Owner ActivityController is a proxy to the ActivityController instance you created in the MainMenu.nib. It is the same object.

If instead you had dragged an ActivityController into the ActivityView nib, you would have been creating a new instance of the ActivityController. These would have been two separate objects, so the connections in one nib and the connections in the other nib would not have helped communicate at all.

## 14.7 Exercise: Loading the View

Click Build & Run, and the code should compile, build, and run, and an empty window should appear.

![](img/9355405953264484a02198b0e3d25b7e_235_1.png)

We need to fix this. Which object can communicate with the window and the view controller? Use that object to set the window’s content view to be the view controller’s view. We could do this in IB, but let’s do it in code.

You’ll know you’ve gotten it right when you click Build & Run and the text field and image will be visible again and filled in.

## 14.8 Solution: Loading the View

Your application delegate is the object with properties for the window and the view controller. All you need to do is import the ActivityController header file and connect the view to be the view controller’s view like this:

```objc
#import "HelloApplicationAppDelegate.h"
#import "ActivityController.h"

@implementation HelloApplicationAppDelegate

@synthesize window, ac, currentApp;

- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    self.window.contentView = ac.view;
}
@end
```

Click Build & Run, and our application should run just as it did at the end of the previous chapter.

## 14.9 Creating the Window Nib

We’re going to split the MainMenu nib into two pieces again. We’ll create a new nib that contains this window. Let’s create a window controller that we can use as the File’s Owner. In Xcode, select the Classes folder in Groups & Files, create a new file of type Mac OS X > Cocoa Class > Objective-C Class, and use the drop-down list to select NSWindowController. Name your class MyWindowController.

- There were a lot of steps used to create and use the new nib. Remember, you can look at the downloadable code to compare this version with the previous one.

![](img/9355405953264484a02198b0e3d25b7e_237_0.png)

![](img/9355405953264484a02198b0e3d25b7e_237_1.png)

![](img/9355405953264484a02198b0e3d25b7e_237_2.png)

An Objective-C class file, with an optional header which includes the <Cocoa/Cocoa.h> header.

Now select the Resources folder, and create a new file using the Mac OS X > User Interface > Window XIB template. Name the nib MainWindow.xib. Use the Identity inspector to change the type of the File’s Owner to MyWindowController.

![](img/9355405953264484a02198b0e3d25b7e_237_3.png)

![](img/9355405953264484a02198b0e3d25b7e_237_4.png)

Use the Attributes inspector to change the window’s title to Hello Application. Connect your File’s Owner’s window outlet to your window, and save your work. We’ll come back to this nib in a little bit, but first let’s back up and clean out the MainMenu nib.

## 14.10 Loading the Window Nib

Open MainMenu.xib. Delete the CurrentApp object, the ActivityController object, and the NSWindow object along with the ContentView inside of it. There’s not much left—just the app delegate, the menu, and a couple of stock items.

![](img/9355405953264484a02198b0e3d25b7e_238_0.png)

HelloApplication.xcodeproj

The app delegate no longer has a connection to the model, the window, or the view controller. We’ll figure out where to reconnect all of these objects in a bit. Right now we can clear out the header file for our app delegate:

Download MultipleNibs/HelloApplication20/HelloApplicationAppDelegate.h

```objective-c
#import <Cocoa/Cocoa.h>

@interface HelloApplicationAppDelegate : NSObject <NSApplicationDelegate> {
}

@end
```

In the implementation file, we’ll instantiate the window controller and load its nib file:

Download MultipleNibs/HelloApplication20/HelloApplicationAppDelegate.m

```objective-c
#import "HelloApplicationAppDelegate.h"
#import "MyWindowController.h"

@implementation HelloApplicationAppDelegate

- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    [[MyWindowController alloc] initWithWindowNibName:@"MainWindow"];
}
@end
```

The initWithWindowNibName: takes the name of the nib as an NSString. This means there can’t be any compile-time checking that you’ve typed the name correctly. You type in the name of the nib but not the suffix
