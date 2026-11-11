
## 7.1 Integrating with Spotlight

The issue, as mentioned, is one of multiple files. Ideally, for our recipe application, we want one Spotlight “record” for each recipe in our Core Data repository. For Spotlight to work properly, we would need one file on the disk for each recipe along with its associated metadata. Therefore, to make Spotlight happy, we will do exactly that. However, since all our data is being stored in a Core Data repository, there is no reason to store any data in these files. These additional files exist purely for Spotlight (and Quick Look) to utilize. Since Spotlight does not need any data in the files to work (it just needs metadata), we will create very simple files and link them back to our Core Data repository.

The other gotcha with Spotlight is that the importer needs to be as fast as possible. What might be acceptable for processing one file or ten files is not going to fly when Spotlight has to chug through thousands of files. Since the same importer that we are writing for use inside our application could potentially be used in a server situation, it needs to be as fast as we can make it. Therefore, we will cheat a bit. Instead of looking up the metadata in our Core Data repository upon request from Spotlight, we will instead store that metadata in the files we are creating for Spotlight. That way, our importer has to touch the metadata files only and does not need to initialize the entire Core Data “stack” (NSManagedObjectContext, NSPersistentStoreCoordinator, and NSManagedObjectModel).

### Creating the Metadata Files

We first need to produce and update the metadata files on the fly. To keep them as simple as possible, we will just use plist files as opposed to a binary representation or some other format. Since NSDictionary understands plist files, it will reduce the amount of overhead we have for loading and saving the files.

To begin with, we will create our first NSManagedObject subclass. This subclass will handle producing the NSDictionary that will contain all the metadata. Since we are creating a subclass, we might as well implement some of the properties we will be using to reduce the code complexity and make it easier to maintain.

![](img/ffa5f756dbdb501d7886468ffb761ad4_116_0.png)

Figure 7.1: Changing the entity's class

Therefore, our header file will look as follows:

```objc
// Download Spotlight/PPRecipe.h
#import <Cocoa/Cocoa.h>

extern NSString *kPPImagePath;
extern NSString *kPPObjectID;
extern NSString *kPPServes;

@interface PPRecipe : NSManagedObject {

}

@property (assign) NSString *desc;
@property (assign) NSString *name;
@property (assign) NSString *type;
@property (assign) NSManagedObject *author;
@property (assign) NSDate *lastUsed;

- (NSDictionary*)metadata;
- (NSString*)metadataFileName;

@end
```

We need to make sure that we change the class setting in the latest data model so that Core Data will use our subclass rather than the default NSManagedObject. See Figure 7.1.

### Implementing the Metadata Method

The goal of this metadata file is to contain just enough information to populate Spotlight and Quick Look but not too much information that the files become large and cumbersome. We always have to pretend that there will be thousands of these files (even if in reality that would be impractical), and we do not want to impact the user’s performance or their hard drive capacity. For our metadata files, we really need only the following information:

- The name of the recipe
- The number of people it serves
- The image for the recipe
- The last time it was served
- The description of how to prepare it

Most of that list is very light—just text. However, the image is probably too large to cram into the plist file, especially since we cannot be sure how large those files will be. In addition, it would complicate the file format by including binary data. Therefore, we will put in its path instead of the actual image. Since the image is stored on disk anyway, we can just access that copy.

In addition to this list, we need to add one more item that is not user facing. We want a way to link back to the recipe record in our Core Data repository so that if the user tries to open the metadata file, it will instead open our application and select the correct record. To do this, we will use the NSManagedObjectID of the recipe and store its URIRepresentation (which is actually an NSURL) as a string in the metadata.

```objc
- (NSDictionary*)metadata
{
    NSMutableDictionary *metadataDict = [NSMutableDictionary dictionary];

    [metadataDict setValue:[self name]
                    forKey:(id)kMDItemTitle];
    [metadataDict setValue:[self desc]
                    forKey:(id)kMDItemTextContent];
    [metadataDict setValue:[[self author] valueForKey:@"name"]
                    forKey:(id)kMDItemAuthors];
    [metadataDict setValue:[self valueForKey:@"imagePath"]
                    forKey:kPPImagePath];
    [metadataDict setValue:[self lastUsed] forKey:(id)kMDItemLastUsedDate];
    [metadataDict setValue:[self valueForKey:@"serves"] forKey:kPPServes];
    [metadataDict setValue:[NSString stringWithFormat:@"Recipe: %@", [self name]]
                    forKey:(id)kMDItemDisplayName];
    [metadataDict setValue:[[[self objectID] URIRepresentation] absoluteString]
                    forKey:kPPObjectID];
    return metadataDict;
}
```

### Implementing the metadataFileName Method

Because we want users to be able to view the actual metadata files in the Finder, the filenames should represent the recipe rather than an abstract name. Therefore, we will use the name attribute of the recipe itself as the filename:

```objc
// Download Spotlight/PPRecipe.m
- (NSString*)metadataFileName
{
    return [[self name] stringByAppendingPathExtension:@"grokkingrecipe"];
}
```

### Generating and Updating the Metadata Files

Now that we have an implementation for generating the metadata per recipe, we need to add the ability to populate these files and keep them up-to-date. Ideally, we want to refresh the metadata files every time that the NSManagedObjectContext is saved. To do this, we will add a new `-save:` method to our AppDelegate and route all of our saves through it:

```objc
// Download Spotlight/AppDelegate.m
- (BOOL)save:(NSError**)error
{
    NSManagedObjectContext *moc = [self managedObjectContext];
    if (!moc) return YES;

    if (![moc hasChanges]) return YES;

    // Grab a reference to all of the objects we will need to work with
    NSSet *deleted = [moc deletedObjects];
    NSMutableSet *deletedPaths = [NSMutableSet set];
    for (NSManagedObject *object in deleted) {
        if (![object isKindOfClass:[PPRecipe class]]) continue;
        [deletedPaths addObject:[object valueForKey:@"metadataFileName"]];
    }

    NSMutableSet *updated = [NSMutableSet setWithSet:[moc insertedObjects]];
    [updated unionSet:[moc updatedObjects]];

    // Save the context
    if (![moc save:error]) {
        return NO;
    }
    return [self updateMetadataForObjects:updated
                andDeletedObjects:deletedPaths
                             error:error];
}
```

Next, we need to confirm that the cache directory is in place and either our metadata directory is in place or we can create it. If any of this fails, we update the NSError object and return.

```objc
// Download Spotlight/AppDelegate.m
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

```objc
// Download Spotlight/AppDelegate.m
if (!updatedObjects || ![updatedObjects count]) return YES;

NSNumber *_YES = [NSNumber numberWithBool:YES];
NSDictionary *attributesDictionary = [NSDictionary dictionaryWithObject:_YES forKey:NSFileExtensionHidden];

for (NSManagedObject *object in updatedObjects) {
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
