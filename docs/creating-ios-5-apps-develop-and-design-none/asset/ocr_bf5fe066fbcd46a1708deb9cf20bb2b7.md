We pass our WeightHistory object as the file presenter. This means our WeightHistory class won’t receive any notifications about changes made during our coordinated blocks. In general, this is exactly what we want—but it also means we may need to update the UI manually once we’re done.

Finally, we call the resolveConflictsWithCurrentURL:coordinator: method on a background queue. It’s very important to use a background thread here. Obviously, from a performance standpoint, we never want to do any file input/output operations in the main thread—that could dramatically hurt our user interface’s performance. Instead, we should always read and write data in the background. More pragmatically, however, creating coordination blocks on the main thread can cause the application to deadlock. We definitely don’t want that.

Next, let’s look at resolveConflictsWithCurrentURL:coordinator::

```
```objc
- (void)resolveConflictsWithCurrentURL:(NSURL*)currentURL
                 coordinator:(NSFileCoordinator*)coordinator {
    NSError* error;
    [coordinator
        coordinateReadingItemAtURL:currentURL
        options:0
        writingItemAtURL:currentURL
        options:NSFileCoordinatorWritingForMerging
        error:&error
        byAccessor:^(NSURL *inputURL, NSURL *outputURL) {
            // Load our data.
            NSData* data =
                [NSData dataWithContentsOfURL:inputURL];
            NSMutableArray* currentHistory =
                [NSKeyedUnarchiver unarchiveObjectWithData:data];
            // Read in all the old versions.
            NSArray* unresolvedVersions =
```
```