
Declare the following methods in the header file:

```objc
+ (NSString*)entityName;
+ (WeightEntry*)addEntryToDocument:(UIManagedDocument*)document
                  usingWeightInLbs:(CGFloat)weight
                              date:(NSDate*)date;
```

Our entityName implementation is, not surprisingly, very simple.

```objc
+ (NSString*)entityName {
    return @"WeightEntry";
}
```

Unfortunately, addEntryToDocument:usingWeightInLbs:date: requires a bit more work. Let’s go over this implementation a step at a time.

```objc
#pragma mark - Convenience Methods
+ (WeightEntry*)addEntryToDocument:(UIManagedDocument*)document
                  usingWeightInLbs:(CGFloat)weight
                              date:(NSDate*)date
{
    NSManagedObjectContext* context = document.managedObjectContext;
    NSAssert(context != nil,
             @"The managed object context is nil");
```

This is just a bit of sanity checking. We’re getting a local reference to the managed object context, and we check to make sure it isn’t set to nil. We cannot create new managed objects without the context.

```objc
NSEntityDescription* entity =
    [NSEntityDescription entityForName:[WeightEntry entityName]
                    inManagedObjectContext:context];
NSAssert1(entity != nil,
          @"The entity description for WeightEntry in %@ is nil",
          context);
WeightEntry* entry =
[[WeightEntry alloc] initWithEntity:entity
    insertIntoManagedObjectContext:context];
```

Next, we grab our entity description from the context, and then we use that description to instantiate a new WeightEntry object. WeightEntry is automatically inserted into our context as part of its initialization.

```objc
entry.weightInLbs = weight;
entry.date = date;
// Save a snapshot to the parent context.
NSError *error = nil;
if (![context save:&error]) {
    // Ideally, we should replace this
    // with more-robust error handling.
    // However, we're not saving to disk,
    // we're just pushing the change
    // up to the parent context--so most errors should be
    // caused by mistakes in our code.
    [NSException
        raise:NSInternalInconsistencyException
        format:@"An error occurred when saving the context: %@",
        [error localizedDescription]];
}
return entry;
}
```

Finally, we push the change up to the parent context and then return our new entry. Remember, we're working with a child managed object context, so we aren't actually saving anything. We're just updating the document's snapshot.

Actually, this save isn’t strictly necessary. UIManagedDocument will handle all the saves automatically. However, this helps make our intentions clear and will assist the undo manager. Without the explicit saves, the undo manager will register all changes as undo actions—including the undo actions themselves. This means that our shake will undo and then redo the same action repeatedly. By explicitly adding these saves, the undo actions are not recorded, letting us undo multiple changes.

That’s it. Our WeightEntry is complete, and we’re done with the OldWeightEntry class. Delete OldWeightEntry.h and OldWeightEntry.m from the project. Now we just need to update our view controllers.

## UPDATING THE VIEW CONTROLLERS

Let’s start with EnterWeightViewController. Open the header file, and delete the forward declaration and the property. In the implementation file, start by deleting the import and synthesize lines. Repeat this procedure for the GraphViewController and HistoryViewController classes. If we try to build the application now, we will see a number of orphaned weightHistory references in our implementation file. That’s OK. We will use these as guideposts, helping us find all the methods that need to be modified.

Next, we need to add the following document property to our enter weight, graph, and history view controllers:

```objc
@property (strong, nonatomic) UIManagedDocument* document;
```

Be sure to synthesize it in all three implementation files. With that out of the way, the real work can begin.

### ENTERWEIGHTVIEWCONTROLLER

Now, open EnterWeightViewController.m. Start by importing WeightEntry.h. Next, we want to clear out all our error messages. Navigate down to the saveWeight: method. Replace the existing implementation with the following:

```objc
- (IBAction)saveWeight:(id)sender {
    CGFloat weight =
        [[self.numberFormatter
            numberFromString:self.weightTextField.text]
            floatValue];
    if (getDefaultUnits() != LBS) {
        weight = [WeightEntry convertKgToLbs:weight];
    }
    // This creates a new weight entry and adds
    // it to our document's managed object context.
    [WeightEntry addEntryToDocument:self.document
                    usingWeightInLbs:weight
                              date:self.currentDate];
    // Automatically move to the second tab.
    // Should be the graph view.
    self.tabBarController.selectedIndex = 1;
}
```

Here, we call the convenience method we just wrote, adding a new WeightEntry to our document. Once that's done, we tell the tab bar controller to shift to the graph view.

Next, scroll down to the setWeightHistory: method. We just need to convert this to use UIManagedDocument instead. That essentially means replacing all the weight history references with document references.

```objc
#pragma mark - Custom Accessor
- (void)setDocument:(UIManagedDocument *)document {
    NSNotificationCenter* notificationCenter =
    [NSNotificationCenter defaultCenter];
    // If we're assigning the same document, don't do anything.
    if ([_document isEqual:document]) {
        return;
    }
    // Clear any notifications for the old document, if any.
    if (_document != nil) {
        [notificationCenter
            removeObserver:self
                      name:UIDocumentStateChangedNotification
                    object:_document];
    }
    _document = document;
    // Add new notifications for the new document, if any,
    // and set the view's values.
    if (_document != nil) {
        // Register for notifications.
        [notificationCenter
            addObserver:self
               selector:@selector(updateSaveAndEditStatus)
                   name:UIDocumentStateChangedNotification
                 object:_document];
        // Update our save and edit status.
        [self updateSaveAndEditStatus];
    }
}
```

Both UIManagedDocument and our old WeightHistory class are subclasses of UIDocument—so everything should still work fine. Specifically, we still want to watch the document's state, and disable editing or display save warnings when necessary.

Finally, look at the updateSaveAndEditStatus method. We need to change self.weightHistory to self.document in the first few lines.

```objc
- (void)updateSaveAndEditStatus {
    if (self.document == nil) {
        // Disable editing.
        [self.weightTextField resignFirstResponder];
        self.weightTextField.enabled = NO;
        return;
    }
    UIDocumentState state =
        self.document.documentState;
```

Our EnterWeightViewController class is now finished and ready to go. Next, let's look at the history view.

### HISTORYVIEWCONTROLLER

We need to modify the history view controller so that it uses an NSFetchedResultsController. As we will see, the NSFetchedResultsController manages data from Core Data, letting us easily display the data in a UITableView. We can also assign a delegate to the fetched request controller, letting us respond to any changes in the underlying data.

To begin, open HistoryViewController.h. Import the Core Data framework, and have HistoryViewController adopt the NSFetchedResultsControllerDelegate protocol.

```objc
#import <UIKit/UIKit.h>
#import <CoreData/CoreData.h>
@interface HistoryViewController : UITableViewController
    <NSFetchedResultsControllerDelegate> {
}
@end
```

Switch to the implementation file. We start by updating our #import directives. Make sure we are importing WeightEntry.h.

```objc
#import "HistoryViewController.h"
#import "DetailViewController.h"
#import "HistoryCell.h"
#import "WeightEntry.h"
```
