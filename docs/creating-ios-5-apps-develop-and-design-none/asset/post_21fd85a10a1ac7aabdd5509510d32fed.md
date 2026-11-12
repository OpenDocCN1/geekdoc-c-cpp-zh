
```objc
for (id entry in toAdd) {
    if (![self containsObject:entry]) {
        [self addObject:entry];
    }
}
```

Here our mutable array iterates over all the items in the incoming array. We check to see if the mutable array contains each item. If it doesn't, we save a reference to the item, then add it to the mutable array.

Again, there's one small catch. Our WeightEntry's default implementation will simply compare the object pointers. However, since our arrays were loaded from disk, we will undoubtedly have different WeightEntry instances that actually contain the same value (same date and weightInLbs). We need to override the default isEqual: method and provide an implementation that performs a deep comparison.

Switch to the WeightEntry.m file and add a new isEqual: method.

```objc
#pragma mark - Equality
- (BOOL)isEqual:(id)object {
    if (![object isKindOfClass:[WeightEntry class]]) return NO;
    return [self.date isEqual:[object date]] &&
        (self.weightInLbs == [object weightInLbs]);
}
```

We start by verifying that our incoming object argument belongs to the WeightEntry class. If it does, we simply compare the date and weightInLbs properties. If they are both the same, we return YES. Otherwise, we return NO.

That's simple enough. However, whenever we override the isEqual: method we also need to override the hash method.

```objc
- (NSUInteger)hash {
    size_t size = sizeof(NSUInteger);
    NSUInteger weight = (int)self.weightInLbs * 100;
    return [self.date hash] ^ (weight << (size / 2));
}
```

The hash method returns an integer. We use these values as the object’s address in a hash table or similar collection. Ideally, each unique object should return a unique hash value. More importantly, if two objects are equal they must return the same hash value.

Our calculation simply converts our weight value to an integer and shifts it over by half the integer’s size. We then combine it with the date’s hash using the bitwise XOR operator. This should provide a reasonably good hash value. Our weight values should be (relatively speaking) low values—so shifting it won’t lose any information.

I don’t know how NSDate implements its hash method. A simple implementation would just convert the internal NSTimeInterval to a hash value. This means the lowest bits may be the most important—we shouldn’t alter them. However, a more thorough implementation would create more-random hash values (ensuring that date objects get more evenly spread over the available hash space). In that case, it doesn’t really matter which bits we alter.

Either way, we don’t need high-performance hashing, so this implementation will work fine. OK, let’s get back to WeightHistory.m. First things first, we need to import our new category.

```objc
#import "NSMutableArray+Union.h"
```

Now we still have to save our merged data. This gets a bit long, so let’s take it one step at a time.

```objc
- (void)saveMergedHistory:(NSArray *)currentHistory
                    toURL:(NSURL *)url
              coordinator:(NSFileCoordinator *)coordinator
              oldVersions:(NSArray *)oldVersions {
    NSError *writeError;
    [coordinator
        coordinateWritingItemAtURL:url
        options:NSFileCoordinatorWritingForMerging
        error:&writeError
        byAccessor:^(NSURL *outputURL) {
            NSData *dataToSave =
                [NSKeyedArchiver
                    archivedDataWithRootObject:currentHistory];
            NSError *innerWriteError;
            BOOL success = [dataToSave
                                writeToURL:outputURL
                                options:NSDataWritingAtomic
                                error:&innerWriteError];
```

Here, we create our coordinated write block and save our currentHistory array. We do this as a two-step process. First, we use an NSKeyedArchiver to create an NSData object from our array. Then we save the NSData to disk. We could have used the keyed archiver to perform this in one step—but doing it this way gives us more-informative error messages.

```objc
            if (success) {
                // Mark the conflicting versions as resolved.
                for (NSFileVersion *version in oldVersions) {
                    version.resolved = YES;
                }

                // Remove old versions.
                NSError *removeError;
                BOOL removed =
                    [NSFileVersion
                        removeOtherVersionsOfItemAtURL:outputURL
                        error:&removeError];
                if (!removed) {
                    NSLog(@"*** Error: Could not erase outdated "
                          @"versions! %@",
                          [removeError localizedDescription]);
                }
```

If we successfully save the merged data, we mark all the conflicting versions as resolved. This means they will no longer appear in any future reports about conflicts. Then we remove the old versions. It’s important to note that removing old versions must be performed within a coordinated write block. We also deliberately delay modifying the conflicting versions until we’re sure the conflict is completely resolved.

```objc
            } else {
                NSLog(@"*** Error: Unable to save our merged "
                      @"history! %@ ***",
                      [innerWriteError localizedDescription]);
            }
```

Now, we force our UIDocument to reload itself. In the normal day-to-day operations of a UIDocument subclass, we never call readFromURL:error: directly. Instead, the system calls this method whenever it needs to load our document. This is, however, a somewhat exceptional situation. So far, we’ve been reading and writing our data directly to disk—we haven’t involved the UIDocument at all. As a result, it doesn’t know anything about the changes we’ve made. By calling readFromURL:error: here, we force our document to update itself.

```objc
            // And reload our document.
            NSError *reloadError;
            BOOL reloaded = [self readFromURL:self.fileURL
                                        error:&reloadError];

            if (!reloaded) {
                NSLog(@"*** Error: Unable to reload our "
                      @"UIDocument! %@ ***",
                      [reloadError localizedDescription]);
            }
```

Also note that we don’t need a coordinated read block here. We’re still inside our original read block. Yes, we’re using the write block’s URL, but this should be the most up-to-date URL pointing back to our original file. So we should be good to go.

```objc
        }];
    if (writeError != nil) {
        NSLog(@"*** Error: Unable to perform a coordinated write "
              @"on our merged version: %@ ***",
              [writeError localizedDescription]);
    }
}
```

The rest of this is simply error handling. Honestly, we're not doing much, just logging the error to the console. Still, if we do run into any problems, the conflicts will simply linger. The next time our file is modified, it will trigger the conflict notification again, and we can try one more time to merge everything.

That's it. We've implemented all of our WeightHistory's basic features. Next, let's look at the procedures involved in creating and opening our document.

## LOADING iCLOUD DOCUMENTS

Health Beat is a single-document application. This makes managing our files a little complicated. When the application launches, we need to search for any existing documents. If we find an existing document, we open it. If not, we create a new document and save it to disk.

**NOTE:** In this version of Health Beat, we automatically upload the file to iCloud if we can. However, this isn't the best design. Each user only has 5 GB of free iCloud document storage. We really should ask the user before using up some of that space. Furthermore, they should be able to change their mind later on, moving their files back and forth as necessary. Unfortunately, this makes the application a lot more complex. I will leave that as an extra-credit assignment for the truly determined reader.

![](img/fe9fea534a8e7868f811f7cd33da015f_331_0.png)

### FIGURE 6.4 Opening the document

![](img/fe9fea534a8e7868f811f7cd33da015f_332_0.png)

To further complicate things, documents may be stored either in the local sandbox or in iCloud storage. We need a slightly different procedure for searching, opening, and saving at each location. In fact, all the possible permutations can get quite complex. Figure 6.4 shows the basic steps we need to follow.

OK, I have some good news and some bad news. The good news is that we can hide all this complexity behind a single WeightHistory convenience method. This will allow us to open (or create if necessary) our file with a single method call. The bad news is that we still have to write all this code.
