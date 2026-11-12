
```objc
[super viewDidLoad];
id graphView = self.view;
[graphView setWeightEntries:self.weightHistory
                    andUnits:getDefaultUnits()];

// Register to receive notifications when the default unit changes.
[[NSNotificationCenter defaultCenter]
 addObserverForName:NSUserDefaultsDidChangeNotification
 object:[NSUserDefaults standardUserDefaults]
 queue:nil
 usingBlock:^(NSNotification *note) {
     [graphView setWeightEntries:self.weightHistory
                         andUnits:getDefaultUnits()];
 }];
}
```

Next, find the observeValueForKeyPath:ofObject:change:context: method. Delete it. We won't be using KVO in this implementation.

Finally, just as with the other view controllers, we need to convert our setWeightHistory: custom accessor into setDocuments:. This is long, but we've seen most of it before.

```objc
#pragma mark - Custom Accessor
- (void)setDocument:(UIManagedDocument*)document {
    NSNotificationCenter* center =
    [NSNotificationCenter defaultCenter];
    // If we're assigning the same history, don't do anything.
    if ([_document isEqual:document]) {
        return;
    }
    // Clear any notifications for the old history, if any.
    if (_document != nil) {
        [center
            removeObserver:self
                      name:NSManagedObjectContextObjectsDidChangeNotification
                    object:self.document.managedObjectContext];
    }
    _document = document;

    // Add new notifications for the new history, if any,
    // and set the view's values.
    if (_document != nil) {
        // Create the fetch request.
        NSFetchRequest *fetchRequest = [NSFetchRequest
            fetchRequestWithEntityName:[WeightEntry entityName]];

        // Set up sort descriptor.
        NSSortDescriptor *sortDescriptor =
            [[NSSortDescriptor alloc] initWithKey:@"date" ascending:NO];
        NSArray *sortDescriptors =
            [[NSArray alloc] initWithObjects:sortDescriptor, nil];
        [fetchRequest setSortDescriptors:sortDescriptors];
        NSError* error;
        self.weightHistory =
            [self.document.managedObjectContext
                executeFetchRequest:fetchRequest
                error:&error];
        if (self.weightHistory == nil) {
            // We may want more-thorough error checking; however,
            // at this point, the main cause for errors tends to be
            // invalid keys in the sort descriptor. Let's fail fast
            // so we're sure to catch that during development.
            [NSException
                raise:NSInternalInconsistencyException
                format:@"An error occurred when performing our fetch %@",
                [error localizedDescription]];
        }
        [center
            addObserverForName:
            NSManagedObjectContextObjectsDidChangeNotification
            object:self.document.managedObjectContext
            queue:nil
            usingBlock:^(NSNotification* notification) {
                NSError* fetchError;
                self.weightHistory =
                [self.document.managedObjectContext
                    executeFetchRequest:fetchRequest
                    error:&fetchError];
                if (self.weightHistory == nil) {
                    // We may want more-thorough error checking; however,
                    // at this point, the main cause for errors tends
                    // to be invalid keys in the sort descriptor. Let's
                    // fail fast so we're sure to catch that during development.
                    [NSException
                        raise:NSInternalInconsistencyException
                        format:@"An error occurred when performing "
                                @"our fetch %@",
                        [fetchError localizedDescription]];
                }
                // If the view is loaded, we need to update it.
            }];
    }
}
```

Of course, there's a lot of room for improvements. We could share a single fetch request between both the HistoryViewController and the GraphViewController. Better yet, we could use an NSFetchedResultsController here as well, sharing the same cache as the HistoryViewController. Having the caching and the built-in support for change detection would be nice. We don't need the section or index path support, and it would be a little harder to get our array of WeightEvents, but it might be worth the effort.

Still, users often only enter a single weight per use. This means we only call the fetch request once. So, go easy with the changes. Unless we find a compelling reason to make changes (after profiling and stress testing, that is), it's probably best to just leave things alone.

## WRAPPING UP

That's it. Run the application. Try adding and deleting weights. Navigate to the history view, and shake to undo. Everything should work as expected. Launch it on a second device; all the weights should transfer over. Put the first device on the graph view. Then enter a new weight on the second device, and put that app into the background. Within a minute or so, the first device's screen should change. If everything looks good, commit your changes.

Of course, there is one big difference between this version and the last. Shake to undo no longer asks for permission before making a change. It immediately undoes the last action. It turns out that we threw out most of our undo support code when we deleted the old WeightHistory class. That means we didn't even register any actions for undo, or create the inverse undo methods. Core Data handled everything for us automatically.

I'll leave the alerts as homework. It shouldn't be hard to move the relevant WeightHistory code over to the HistoryViewController. Just be sure to set the undo action name every time you save the context. Then add the alert methods.

Next chapter, we will take a break from the Health Beat application to look at custom controls. In particular, we will focus on using Core Motion and custom gestures. Finally, in Chapter 9, we will look at all the little details that need to be completed before submitting your app to the App Store.

## 8 DESIGNING CUSTOM CONTROLS

This chapter covers a broad range of advanced topics that focus on creating an immersive custom user interface. We start by building a view hierarchy that divides our dynamic and static elements into separate layers, allowing us to rapidly redraw the interface as changes occur. We also create a custom UIViewController container to manage our subviews, while using Core Animation to control the transition between these views. Next, we respond to user input using gesture recognizers to track different touch-based commands and Core Motion to monitor the device’s rotation. Finally, we will use Core Location to geotag images, then export those images by saving them to the photo library, attaching them to email, or tweeting them using the new integrated Twitter API.

![](img/fe9fea534a8e7868f811f7cd33da015f_450_0.png)

## INTRODUCING GRAVITYSCRIBBLER

![](img/fe9fea534a8e7868f811f7cd33da015f_451_0.png)

**FIGURE 8.1** GravityScribbler in action

This chapter is going to be somewhat different from the rest of the book. We’re going to take a break from our Health Beat application to examine a number of advanced topics: from custom view hierarchies and animation to motion detection and geotagging. Since most of these topics cannot be easily shoehorned into our existing application, we will look at a new, immersive application: GravityScribbler.

GravityScribbler is a simple drawing application (**Figure 8.1**). It begins with a cursor in the center of the screen, and the user can direct the cursor by tipping and tilting their phone. The cursor will roll downhill, drawing a line behind it. The user can also utilize an assortment of gestures to control the application. A single-finger horizontal pan will control the cursor’s speed. A two-finger touch will pause and restart the application, while a three-finger swipe will drag out the export menu. Finally, shaking the phone clears the current drawing, letting the user start over.

Unlike what we’ve done thus far, we won’t go through a step-by-step walk-through and build the entire application from scratch. There is just too much ground to cover. Instead, we will focus more tightly on the individual topics. If you want to see how these topics integrate into a completed application, check out the complete source code from http://freelancemadscience.com/source.

Additionally, since GravityScribbler depends so strongly on touch gestures and device motion, we cannot effectively test it in the simulator. You must run it on the device itself. This means you must have a valid iOS Developer Program membership, as well as the proper provisioning profiles for your device. We examined this in detail in the section “Running and Testing on iOS Devices” in Chapter 3.

Let’s start by looking at techniques for creating a truly custom dynamic user interface.
