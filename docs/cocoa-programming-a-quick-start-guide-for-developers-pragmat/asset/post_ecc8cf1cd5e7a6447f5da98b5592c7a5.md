
dictionary to eliminate an if in another part of our code. This time we'll use another technique.

### 16.7 Table Column Identifiers as Keys

Instead of using the column header titles in our if statement, we can use another property of table columns called the *identifier*. The title is text that is visible at the top of the column in the header cell. That text is meant to communicate with the application user. The identifier is invisible to the end user. The data source uses it to identify the column. We can use the identifier as a key in a dictionary or as a name of a property or method.

So, select the table’s first column in Interface Builder, and use the Attributes inspector to set the Identifier to icon. Similarly, set the Identifier in the second column to localizedName. I haven’t chosen those names at random; these are the names of the properties in the NSRunningApplication class that I want to appear in each of the columns.

![](img/9355405953264484a02198b0e3d25b7e_264_0.png)

Now we can call the method with the same name as the identifier. It is just the getter for the property with that name.

```objective-c
- (id)tableView:(NSTableView *)aTableView
       objectValueForTableColumn:(NSTableColumn *)aTableColumn
                              row:(NSInteger)rowIndex {
    return [[self.runningApps objectAtIndex:rowIndex]
        performSelector:NSSelectorFromString([aTableColumn identifier])];
}
```

Here’s roughly what has to happen to fill the table with icons and names. First the table view asks its data source how many rows are in this table. The data source replies [runningApps count]. Then for each cell in the table, the table view asks its data source, “What goes here?” The data source now answers with the information for the application whose index in the array matches the row number.^4 And in each cell the data source responds with the value of the property that matches the cell's column's identifier. Pretty nifty.

Look how this simplifies the code—there are no choices to make. Better yet, we don't have to change this code if we introduce new columns.

### 16.8 Previews of Coming Attractions

It turns out that one advantage of properties is that they follow a certain naming convention that allows us to treat objects as if they were dictionaries. In other words, we can pass in the name of the property whose value we want the same way we pass in keys to a dictionary. You'll learn a lot more about this in Chapter 19, *Key Value Coding*, on page 298.

This is such a great place to apply the technique that I just can't wait until we get there. You don't need to understand KVC to appreciate this application. Instead of converting the identifier to a SEL and then performing that selector, we use the `valueForKey:` method and pass in the identifier as the key.

Download Tables/HelloApplication34/ActivityController.m

```objective-c
- (id)tableView:(NSTableView *)aTableView
    objectValueForTableColumn:(NSTableColumn *)aTableColumn
        row:(NSInteger)rowIndex {
    return [[self.runningApps objectAtIndex:rowIndex]
        valueForKey:[aTableColumn identifier]];
}
```

This is yet another thing about programming with Cocoa that makes me smile.

### 16.9 Exercise: Adding and Removing Rows

Our mini-Dock now shows a snapshot of the icons and names of the applications that are running when our application launches. Next, let's update the list by adding launching apps and removing terminating apps.

4. Fortunately, the count for each of them begins with 0.

We could just regenerate the list each time an application launches or terminates from NSWorkspace’s runningApplications array. My goal here, though, is to show you how to add to and remove from the underlying data source of a table view and then update the view.

You already have delegate methods that respond when an application is launched or terminates. Implement one to add the launching application to the bottom of the table view by adding an entry to the end of runningApps and updating the table view. Similarly, implement the other to remove the terminating application from the table view by removing the appropriate entry from runningApps and updating the table view.

### 16.10 Solution: Adding and Removing Rows

We are going to need to contact the table view from our ActivityController. Add an outlet to the header file:

Download Tables/HelloApplication35/ActivityController.h

```objective-c
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface ActivityController : NSViewController <ActivityMonitorDelegate,
NSTableViewDelegate, NSTableViewDataSource> {
    NSMutableArray *runningApps;
    NSTableView *table;
}
@property(retain) NSMutableArray *runningApps;
@property IBOutlet NSTableView *table;
@end
```

In Interface Builder, connect this outlet to your table view.

Back in Xcode, you should have added these two methods to your implementation file for ActivityController. Then add and remove the appropriate entry to the runningApps array, and tell the table view to reload.^5

Download Tables/HelloApplication35/ActivityController.m

```objective-c
- (void) applicationDidLaunch: (NSRunningApplication *) app {
    [self.runningApps addObject:app];
    [self.table reloadData];
}

-(void) applicationDidTerminate: (NSRunningApplication *) app {
    [self.runningApps removeObject:app];
    [self.table reloadData];
}
```

5. Also, you should remember that every time we add a property in a header file that you need to synthesize it in the corresponding implementation file.

### 16.11 Manually Removing Rows

So far, we have initiated changes in the data source that are reflected in the table. In this section, we’re also going to take advantage of the fact that we set the ActivityController to also be the delegate for the table view.

Let’s add a Remove button to our application. This will allow the user to remove applications from the list. The button will become visible only when the user selects an application in the table view. Then if the user clicks the button, the selected application will disappear from the list, and we’ll hide the button again.

Start by adding an outlet and an action to your ActivityController header file. The outlet will connect to the new button, and the action will be the method that gets called when the button is clicked.

```objective-c
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface ActivityController : NSViewController <ActivityMonitorDelegate, NSTableViewDelegate, NSTableViewDataSource> {
    NSMutableArray *runningApps;
    NSTableView *table;
    NSButton *deleteButton;
}
@property(retain) NSMutableArray *runningApps;
@property IBOutlet NSTableView *table;
@property IBOutlet NSButton *deleteButton;
-(IBAction)removeRow:(id)sender;
@end
```

In Interface Builder, add a little square button below the table view. Instead of giving it a title, we’ll display a minus sign on it. To do this, open the Attributes Inspector, and set the button’s image to NSRemoveTemplate. Also select the Hidden checkbox.

![](img/9355405953264484a02198b0e3d25b7e_268_0.png)

Connect the ActivityController’s deleteButton outlet to the button, and wire up the removeRow: action as well. Save.

You now have two methods to implement in ActivityController. The first is a delegate method that is called when the user selects a row. All we want to do is make the button visible when a row is selected.

Download Tables/HelloApplication35/ActivityController.m

```objective-c
- (void)tableViewSelectionDidChange:(NSNotification *)notification {
    [self.deleteButton setHidden:NO];
}
```

When the user clicks the Delete button, we remove the selected row from the runningApps array and reload the table view. We also make sure no row is selected in the table view anymore and hide the button.

Download Tables/HelloApplication35/ActivityController.m

```objective-c
- (IBAction)removeRow:(id)sender {
    [self.runningApps removeObjectAtIndex:[self.table selectedRow]];
    [self.table deselectAll:nil];
    [self.table reloadData];
    [self.deleteButton setHidden:YES];
}
```

Again, I love that the code reads pretty much like the description of what we're trying to accomplish.

Click Build & Run, and you will be able to select rows and remove them from the list. Unfortunately, if you quit HelloApplication and start it up again, the items you removed are back again. In the next chapter, we'll add persistence and preferences to this example.
