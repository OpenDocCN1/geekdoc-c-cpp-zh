```
```objective-c
if (!path) {
    path = [[NSBundle mainBundle] pathForResource:@"DataModel"
                                             ofType:@"mom"];
}
NSAssert(path != nil, @"Unable to find DataModel in main bundle");
NSURL *url = [NSURL fileURLWithPath:path];
managedObjectModel = [[NSManagedObjectModel alloc] initWithContentsOfURL:url];
return managedObjectModel;
}
```
```

This should look quite familiar because it is identical to the way you would build the NSManagedObjectModel on the desktop. We get the path for the .mom file (or the .momd if there are multiple versions of the data model) and use it to initialize the NSManagedObjectModel.

Download Recipe/Classes/AppDelegate.m

```
```objective-c
- (NSString*)documentsFolder
{
    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory,
                                                         NSUserDomainMask, YES);
    NSString *filePath = [paths objectAtIndex:0];
    return filePath;
}
```
```

Before we construct the NSPersistentStoreCoordinator, we need to decide where to store the persistent store file. On the desktop in an application with a single persistent store, we would save the file to the Application Support folder. However, on Cocoa Touch devices, there is no such location. Instead, each application has its own sandboxed Documents directory designed for the storage of files. This is where we will write our persistent store. Using code similar to what we used on the desktop to find the Application Support folder, we will find the Documents folder specific to our application.

Download Recipe/Classes/AppDelegate.m

```
```objective-c
- (NSPersistentStoreCoordinator*)persistentStoreCoordinator;
{
    if (persistentStoreCoordinator) return persistentStoreCoordinator;

    NSFileManager *fileManager = [NSFileManager defaultManager];
    NSString *docFolder = [self documentsFolder];
    if (![fileManager fileExistsAtPath:docFolder]) {
        [fileManager createDirectoryAtPath:docFolder attributes:nil];
    }

    NSString *filePath = nil;
    filePath = [docFolder stringByAppendingPathComponent:@"recipes.sqlite"];
```
```