
When a Cocoa Touch application quits or is sent to the background, it sends its delegate a message from the `UIApplicationDelegate` protocol so that the delegate can take care of business and respond to these events gracefully. In BNRAppDelegate.m, fill in the stubs of these two application delegate callbacks to save the to-do list:

```objc
- (void)applicationDidEnterBackground:(UIApplication *)application
{
    // This method is only called in iOS 4.0+

    // Save our tasks array to disk
    [tasks writeToFile:docPath() atomically:YES];
}

- (void)applicationWillTerminate:(UIApplication *)application
{
    // This method is only called in iOS versions prior to 4.0

    // Save our tasks array to disk
    [tasks writeToFile:docPath() atomically:YES];
}
```

Now build and run your completed application. This exercise was intended to give you a taste of iOS development. There's much, much more out there to do and learn.

## For the More Curious: What about `main()`?

When you began learning C and Objective-C, you learned that the entry point into your program's code is the `main()` function. It's absolutely true in Cocoa / Cocoa Touch development as well, although it's extremely rare to edit this function in Cocoa and Cocoa Touch applications. Open main.m, and you'll see why:

```objc
return UIApplicationMain(argc, argv, nil,
                         NSStringFromClass([BNRAppDelegate class]));
```

Well, that was anti-climactic. Only one line of actual code.

The `UIApplicationMain()` function creates the necessary objects for your application to run. First, it creates a single instance of the `UIApplication` class. Then, it creates an instance of whatever class is denoted by the fourth and final argument and sets it to be the application's delegate, so that it can send its delegate messages when memory gets low, when the application is quit or backgrounded, or when it finishes launching.

And that's the trail from `main()` to `application:didFinishLaunchingWithOptions:` and your custom code.

## 28

## Your First Cocoa Application

In this chapter, you are going to create **TahDoodle**, a desktop Cocoa application. Like iTahDoodle, **TahDoodle** is a simple to-do list application that stores its data as a property list; however, there are some differences. In the iOS application, you used instances of **UITableView**, **UITextField**, and **UIButton**. In this desktop application, you will place the task list in an **NSTableView** where it can be edited directly. You will also have an **NSButton** that will insert a new row in the table view where you can add a new task.

![](img/5f9368899ebf8d92fc145f8def1e89f8_201_0.png)

In addition, in the last chapter, you built your user interface programmatically. In this chapter, you will use a tool included in *Xcode* called **Interface Builder** to create, configure, and connect the elements of your user interface.

In *Xcode*, choose **File → New → New Project...**. Under the Mac OS X section, click on **Application**. From the template choices that appear, select **Cocoa Application** and name the project **TahDoodle**. **TahDoodle** is *document-based*, which means the user can have multiple to-do lists open simultaneously.

**Document Extension** refers to the filename extension to be used when saving your documents (to-do lists) to disk. Set the extension for your data files to be tdl. TahDoodle will not use Core Data or need unit tests.

### Figure 28.2 Creating a new Cocoa Application

![](img/5f9368899ebf8d92fc145f8def1e89f8_202_0.png)

### Edit BNRDocument.h

Open BNRDocument.h and add a method and two instance variables: todoItems will be a mutable array of strings and itemTableView will be a pointer to the NSTableView object that will display the strings in todoItems. Also, declare that BNRDocument conforms to the NSTableViewDataSource protocol.

```objc
#import <Cocoa/Cocoa.h>

@interface BNRDocument : NSDocument <NSTableViewDataSource>
{
    NSMutableArray *todoItems;
    IBOutlet NSTableView *itemTableView;
}
- (IBAction)createNewItem:(id)sender;

@end
```

Note that there is no instance variable for the Insert button. (You’ll see why later.) There is, however, an action for the button – the createNewItem: method.

In the last chapter, the target of the button’s action was the instance of the application delegate class, BNRAppDelegate. A document-based application doesn’t have an application delegate object and instead is built around a subclass of NSDocument. For TahDoodle, that class is BNRDocument.

In a document-based application, the user can have multiple instances of document objects open at the same time. So when TahDoodle is running, you can have multiple instances of BNRDocument (multiple to-do lists). Each instance will have its own table view, button, tasks array, and window. Each instance will respond to messages independently of the others, and each instance will be its own button’s target.

In the declarations you entered, there are also two new terms: **IBOutlet** and **IBAction**. These tell Xcode “This is a pointer (**IBOutlet**) or an action method (**IBAction**) that the developer will use Interface Builder to connect rather than doing so programmatically.”

## A look at Interface Builder

In the project navigator, find and select a file named `BNRDocument.xib`. When you select a file in the project navigator that ends in `.xib` (XML Interface Builder document), Interface Builder appears in the editor pane, displaying a layout grid.

Right now, there is only one view object on the layout grid – a window object. That’s an instance of `NSWindow`, to which you’ll add other view objects shortly.

Now, in the upper-right corner of the Xcode window, click on the righthand **View** button to reveal the Utilities. At the top of Utilities, click the `i` button to reveal the *inspector*.

The inspector is subdivided into separate inspectors. In this chapter, you’ll use the attributes, size, and connections inspectors.

### Figure 28.3 Attributes, size, and connections inspectors

![](img/5f9368899ebf8d92fc145f8def1e89f8_203_0.png)

At the bottom of the Utilities pane, below the inspector, is the *library*, which is also divided into tabs. Select the `box` button to reveal the *object library*. This library presents a list of all of the different object types that Interface Builder knows about, and it's where you get the interface elements to drag and drop on the window object.

At the bottom of the library is a search field. Type table to filter the list of objects. The first item, Table View, represents an instance of the NSTableView class. You can click on it to see its details.

### Edit BNRDocument.xib

Drag an instance of **NSTableView** from the object library onto the window object. Resize the table to fill most of the window but leave room on the bottom for a button.

#### Figure 28.4 Adding an NSTableView

![](img/5f9368899ebf8d92fc145f8def1e89f8_204_0.png)

Notice that the object's edges snap to guides when they approach the edges of the window or other objects. These guides align view objects in accordance with Apple's *Human Interface Guidelines*, or *HIG*. These are the rules that any developer should follow when designing user interfaces for the Mac. There are also HIGs for the iPhone and iPad. You can find all of the HIGs in the developer documentation.

Now you're going to set some of the table view's attributes in the *attributes inspector*. Normally, you click on an object on the layout grid, and the inspector changes context to show you the attributes of that object. Getting to the attributes of an instance of **NSTableView** is trickier. The table view object that you dragged onto the window is actually a collection of nested objects: an **NSScrollView**, an **NSTableView**, and one or more **NSTableColumn** instances. To get to a particular object in this collection, hold down the Control and Shift keys while clicking on the table view. You will see a list of the objects under the cursor, and from there, you can select the object you’re really interested in. Select the NSTableView.

### Figure 28.5 Selecting a view from a stack

![](img/5f9368899ebf8d92fc145f8def1e89f8_205_0.png)

In the attributes inspector, set the table view to have one column. Then, back in the editor, select the table view’s header and resize the lone column to be the full width of the table view.

### Figure 28.6 Resizing columns

![](img/5f9368899ebf8d92fc145f8def1e89f8_205_1.png)
