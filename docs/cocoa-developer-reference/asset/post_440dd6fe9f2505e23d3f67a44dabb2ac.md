
You can use controllers to produce complex applications with very little code. For example, NSTableView is the standard Cocoa object used to display and manage tables. It's a complex class with many features and delegate methods. To implement a TableView without bindings, you must write glue code — code that connects two objects or features together and translates data between them. For example, an array can be translated into a list of values. The code is embedded in delegate methods that are called when the table needs to display, refresh, or modify data. It can easily become very complex.

Controller objects can minimize the glue code. In some applications, they can eliminate it completely. To demonstrate, the example below demonstrates how you can create an application that displays a list of running processes in OS X — with exactly one line of active code.

The App Delegate header file looks like this:

```
#import <Cocoa/Cocoa.h>
@interface TableBindingAppDelegate : NSObject
    <NSApplicationDelegate> {
    NSArray *runningApps;
    NSWindow *window;
}
@property (assign) IBOutlet NSWindow *window;
@property (nonatomic, retain) NSArray *runningApps;
@end
```

It’s a copy of the standard template, with an added NSArray property called runningApps.

The App Delegate implementation looks like this:

```
#import "TableBindingAppDelegate.h"
@implementation TableBindingAppDelegate
@synthesize window, runningApps;
- (void)applicationDidFinishLaunching:
    (NSNotification *)aNotification
{
    self.runningApps =
        [[NSWorkspace sharedWorkspace] launchedApplications];

    NSLog(@"%@", runningApps);
}
@end
```

This code doesn’t do much. It calls the NSWorkspace object and asks for a list of running applications, which is copied to the array. An NSLog call lists the running apps to the console. The logging is optional, but it’s very useful, as you’ll see next.

Figure 13.15 shows the finished application. It has the following features:

- There are three independent columns of data showing values from the `runningApps` array.
- The table dividers can be moved.
- Rows can be selected by clicking on them, and there is an optional selection index used to return information about the number of the current selection.
- Columns can be sorted by clicking on each column header to select ascending or descending sorting.

The application has some limitations. It doesn’t auto-refresh the table; the array is loaded once at launch, and isn’t updated. In its basic state, it’s a display-only app. There are no features for starting and stopping apps, saving the list to a file, maintaining a log file, and so on.

But it’s doing a lot with very little code. And most of the intelligence is built into a controller object, coupled to the array and the table view via bindings.

**Figure 13.15**

Filling a table view with bindings. Most of the active code is built into a controller object and runs automatically.

![](img/2b293e29fc15b0797f113b85dd429b6e_353_0.png)

### Adding a controller object

Figure 13.16 shows the project nib file. The table view automatically adds a surrounding scroll view. The default table view has two columns. Another column has been added by copying and pasting it. Each column’s name — the text string that appears in the divider, at the top of the header — is set in the Attributes pane in Inspector. The size pane sets the default width and optional width limits. Take some time to explore these features before continuing.

Figure 13.16 shows the list of controller objects in the Library window. In this example, you’re using an array as a data source, so you add an instance of `NSArrayController` to the project by dragging it from the Library.

Remember that adding an object to a nib automatically generates an instance in memory when the nib loads. You don’t need to alloc/init the controller in your code — it’s already loaded from the nib.

Optionally, you could subclass it to access its internal features, adding a supporting subclass — perhaps called `ArrayControllerSubclass` — and using IB’s Identity tab to reclass the default controller as your subclass. You don’t need to do that here. Instead, you’ll discover how to use the new controller.

> **TIP**
>
> When you add a column, its default width may be so wide you can’t see it, because it has fallen off the right-hand edge of the table. Setting the widths manually can recover it. Once a column is visible, you can set its width by dragging it with the mouse. This is a tricky process: you’ll need to click on the header tab between two and four times, depending on the table’s selection state.

**Figure 13.16**

Filling a table view with bindings. Most of the active code is built into a controller object and runs automatically.

![](img/2b293e29fc15b0797f113b85dd429b6e_354_0.png)

**Figure 13.18**

Binding to the Controller Content property of the controller, so that it uses the `runningApps` array as a data source

![](img/2b293e29fc15b0797f113b85dd429b6e_356_0.png)

### Reading data from the controller into a view

Reading translated data from the controller is more difficult. Instead of following through with the Controller Content metaphor, this side of the process uses different properties. Effectively, you’re going to look inside the Controller Content object and pull out various slices through the data.

The first — critical — point is that it’s only possible to pull data out of the array if its objects support key-value property access. Figure 13.19 shows a log of the contents of the `runningApps` array. Usually, this array is a collection of dictionary objects, one for each running app. It’s easy to pick out the relevant keys from the log; for example, `NSApplicationName` is the application name. However, not all objects support this kind of access. If they don’t, you can’t use bindings to display their data.

**Figure 13.19**

Understanding the format of the data in the `runningApps` array. Every item is a dictionary.

![](img/2b293e29fc15b0797f113b85dd429b6e_357_0.png)

When using bindings, this point is crucial. You *must* be able to specify a keypath for each displayed property, and it must return a useful value. If you want to use bindings with custom objects, you must design them in a way that supports keypath value access. Dictionaries are ideal for this because they explicitly implement key-value access.

You can’t, however, access a simple linear array of strings, because the strings won’t have an associated key. An array index isn’t enough to support bindings, and bindings don’t support index access. You can’t use `someArray.0` as a keypath.

This complicates the design of applications, because typically you need to pack array data into a dictionary before it can be accessed. Other workarounds are possible, but wrapping content into a dictionary is often the simplest solution.

In this example, dictionaries are already available. So you can move on to the second part of the problem: selecting the formatted data. Figure 13.20 shows the Controller Key combo box. This is another element that seems mysterious, but it is quite simple in practice.

**Figure 13.20**

Listing the possible Controller Key options to select how you want to view the data in the source array

![](img/2b293e29fc15b0797f113b85dd429b6e_358_0.png)

### Understanding controller keys

In the same way that the controller abstracts data from the data source, it also abstracts its display. Each item in this combo box is one possible interpretation or view of the data copied to the controller. Again, these items aren’t related to specific named properties in the original data, and the controller takes no interest in what the data represents or how it’s named.

Instead, these Controller Keys select one particular summary or element of the data. Table 13.2 describes the more useful items in this list.

A key feature of all controller keys is that the data selected by these keys is determined by the user’s actions. The data source array doesn’t change, but the view of the data is modified as the user interacts with the table view or other display object. Figure 13.21 illustrates the process graphically.
