We could just regenerate the list each time an application launches or terminates from NSWorkspace’s runningApplications array. My goal here, though, is to show you how to add to and remove from the underlying data source of a table view and then update the view.

You already have delegate methods that respond when an application is launched or terminates. Implement one to add the launching application to the bottom of the table view by adding an entry to the end of runningApps and updating the table view. Similarly, implement the other to remove the terminating application from the table view by removing the appropriate entry from runningApps and updating the table view.

# ## 16.10 Solution: Adding and Removing Rows

We are going to need to contact the table view from our ActivityController. Add an outlet to the header file:

Download Tables/HelloApplication35/ActivityController.h

```
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
```

In Interface Builder, connect this outlet to your table view.

Back in Xcode, you should have added these two methods to your implementation file for ActivityController. Then add and remove the appropriate entry to the runningApps array, and tell the table view to reload.^5

Download Tables/HelloApplication35/ActivityController.m

```
```objective-c
- (void) applicationDidLaunch: (NSRunningApplication *) app {
    [self.runningApps addObject:app];
    [self.table reloadData];
}
```
```

5. Also, you should remember that every time we add a property in a header file that you need to synthesize it in the corresponding implementation file.