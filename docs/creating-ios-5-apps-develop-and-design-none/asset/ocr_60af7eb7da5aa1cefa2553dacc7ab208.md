```
```objc
NSData* dataToSave =
    [NSKeyedArchiver
        archivedDataWithRootObject:currentHistory];
NSError* innerWriteError;
BOOL success = [dataToSave
                    writeToURL:outputURL
                    options:NSDataWritingAtomic
                    error:&innerWriteError];
```
```

Here, we create our coordinated write block and save our currentHistory array. We do this as a two-step process. First, we use an NSKeyedArchiver to create an NSData object from our array. Then we save the NSData to disk. We could have used the keyed archiver to perform this in one step—but doing it this way gives us more-informative error messages.

```
```objc
if (success) {
    // Mark the conflicting versions as resolved.
    for (NSFileVersion* version in oldVersions) {
        version.resolved = YES;
    }

    // Remove old versions.
    NSError* removeError;
    BOOL removed =
        [NSFileVersion
            removeOtherVersionsOfItemAtURL:outputURL
            error:&removeError];
    if (!removed) {
        NSLog(@"*** Error: Could not erase outdated "
              @"versions! %@",
              [removeError localizedDescription]);
    }
}
```
```