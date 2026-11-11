```
```objc
SEL select = @selector(exportSaveDidEnd:returnCode:contextInfo:);
[savePanel beginSheetForDirectory:nil
                             file:nil
                    modalForWindow:window
                     modalDelegate:self
                    didEndSelector:select
                       contextInfo:[exportIDs retain]];
[exportArrayController setContent:nil];
}
```
```

# ## Kicking Off the NSOperation

The last change we need to make to the AppDelegate is the callback for our NSSavePanel. In this last method, we are grabbing both the filename and the context from the NSSavePanel and constructing an instance of a new class: PPExportOperation. During the initialization, we are passing in a reference to the AppDelegate, the save path, and the NSManagedObjectID objects for the recipes that need to be exported. After the PPExportOperation has been constructed, we can hand it off to an NSOperationQueue. This will cause the PPExportOperation to be run on another thread, allowing the UI to proceed.

```
```objc
Download Multithreading/AppDelegate.m

- (void)exportSaveDidEnd:(NSSavePanel*)savePanel
             returnCode:(NSInteger)returnCode
            contextInfo:(NSArray*)exportIDs
{
    if (returnCode == NSCancelButton) {
        [exportIDs release];
        return;
    }

    PPExportOperation *op = nil;
    op = [[PPExportOperation alloc] initWithDelegate:self
                                       objectIDs:exportIDs
                                      saveFilePath:[savePanel filename]];

    if (!genericOperationQueue) {
        genericOperationQueue = [[NSOperationQueue alloc] init];
    }

    [genericOperationQueue addOperation:op];
    [exportIDs release];
    [op release];
}
```
```