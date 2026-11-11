next need to confirm that the cache directory is in place and either our metadata directory is in place or we can create it. If any of this fails, we update the NSError object and return.

```
Download Spotlight/AppDelegate.m
```

```
NSString *filePath = nil;
if (deletedObjects && [deletedObjects count]) {
    for (NSString *filename in deletedObjects) {
        filePath = [path stringByAppendingPathComponent:filename];
        if (![fileManager fileExistsAtPath:filePath]) continue;
        if (![fileManager removeItemAtPath:filePath error:error]) return NO;
    }
}
```

The next part of updating the metadata is to remove any files that are no longer appropriate. Therefore, if the passed-in deletedObjects set contains any objects, we need to loop over it. Since we know that the name of the metadata file is stored in the deletedObjects variable, we append it to the metadata directory path and check for the existence of the file. If it exists, we delete it.¹ If we run into an issue deleting the file, then we abort the update and let the calling method handle the error.

```
Download Spotlight/AppDelegate.m
```

```
if (!updatedObjects || ![updatedObjects count]) return YES;

NSNumber *_YES = [NSNumber numberWithBool:YES];
NSDictionary *attributesDictionary = [NSDictionary dictionaryWithObject:_YES forKey:NSFileExtensionHidden];

for (NSString *filename in updatedObjects) {
    if (![object isKindOfClass:[PPRecipe class]]) continue;
    PPRecipe *recipe = (PPRecipe *)object;
    NSDictionary *metadata = [recipe metadata];
    filePath = [recipe metadataFileName];
    filePath = [path stringByAppendingPathComponent:filePath];
    [metadata writeToFile:filePath atomically:YES];
    [fileManager changeFileAttributes:attributesDictionary atPath:filePath];
}

return YES;
```

The last part of updating the metadata files is to process existing or new recipes. As with the deleted objects earlier, we first check to see whether there are any objects to update, and if there are not, we are

1. It may be possible that a recipe got created and deleted without ever being saved to disk. It's unlikely, but why take chances?