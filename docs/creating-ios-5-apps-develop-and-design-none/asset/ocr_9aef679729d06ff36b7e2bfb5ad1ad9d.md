directly inside it. Instead, we must create a nested write block and perform our write operations there.

In our code, we load the history array from our current version. Then we get a list of all the conflicting versions. We iterate over these versions, calling mergeCurrentHistory:withConflictingVersion:coordinator: with each of the conflicting versions. As we will see shortly, this will make sure our current version contains all the entries from all the conflicting versions.

Unfortunately, the merge process may leave our history array out of order. So, we sort it by date. We create a sort descriptor, which uses key-value coding to access our weight entries’ date property and sorts them in descending order.

Finally, we call saveMergedHistory:toURL:coordinator:oldVersions: to save our new, merged history and then clean up all the old, conflicted versions. Note that internally, this method will create the nested coordinated write block.

Now let’s look at mergeCurrentHistory:withConflictingVersion:coordinator:.

```
~~~objective-c
- (void)mergeCurrentHistory:(NSMutableArray*)currentHistory
    withConflictingVersion:(NSFileVersion*)version
              coordinator:(NSFileCoordinator*)coordinator {
    NSError* readError;
    [coordinator
     coordinateReadingItemAtURL:version.URL
     options:0
     error:&readError
     byAccessor:^(NSURL *oldVersionURL) {
        NSData* oldData =
        [NSData dataWithContentsOfURL:oldVersionURL];
        NSArray* oldHistory =
        [NSKeyedUnarchiver unarchiveObjectWithData:oldData];
        [currentHistory unionWith: oldHistory];
    }];
    if (readError) {
~~~
```