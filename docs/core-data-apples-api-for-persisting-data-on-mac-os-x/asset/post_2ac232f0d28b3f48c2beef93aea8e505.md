
### 9.6 Wrapping Up

In this chapter, we reviewed how to use Core Data in a multithreaded application and added some very useful features to our recipes application. We have learned that each thread needs to have its own NSManagedObjectContext and that NSManagedObject instances should never cross threads. We also learned how to send notifications across threads so that changes in one NSManagedObjectContext can be updated in other NSManagedObjectContext instances.

![](img/ffa5f756dbdb501d7886468ffb761ad4_184_0.png)

Figure 10.1: iPhone OS New Project dialog box

## Upgrading an Existing Application to Core Data

Many of us have been developing iPhone applications since the SDK’s original release, so it is quite likely that you have an existing application that you want to integrate with Core Data. Fortunately, it does not take very much code to build up the Core Data stack in an existing project.

### Adding a Data Model to the Project

Just like on the desktop, Core Data on Cocoa Touch requires a data model to define the structure of the data entities. Therefore, the first step is to add a data model to the project by selecting File > New File. Within the dialog box that appears, if we select the Resources section, we can then create a new data model, as shown in Figure 10.2, on the next page.

In addition to creating a new data model, we can also use an existing data model from an existing application. Later in this chapter, in Section 10.4, *Recipes for the iPhone*, on page 195, we use the data model from our desktop recipes application in our new iPhone application. The data models are compatible between the desktop and Cocoa Touch, which allows us to share not only models but the underlying persistent stores as well.

![](img/ffa5f756dbdb501d7886468ffb761ad4_185_0.png)

Figure 10.2: Adding a data model to the project

### Adding the Core Data Code

Once we have a data model to work with, we next need to add the code to load the Core Data stack. The exact placement of this code depends on the design of your application. Since there are no document-style applications on the iPhone, it is most common to have a single data model and a single persistent store per Cocoa Touch application. Although I still like to put the Core Data code in the application delegate, it might make sense to put it somewhere else. No matter where the code is placed, it is very similar to the desktop. First we need to initialize the data model.

Download RecipeCT/Classes/AppDelegate.m

```objective-c
- (NSManagedObjectModel *)managedObjectModel
{
    if (managedObjectModel) return managedObjectModel;

    NSString *path = [[NSBundle mainBundle] pathForResource:@"DataModel"
                                                     ofType:@"momd"];
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

This should look quite familiar because it is identical to the way you would build the NSManagedObjectModel on the desktop. We get the path for the .mom file (or the .momd if there are multiple versions of the data model) and use it to initialize the NSManagedObjectModel.

Download Recipe/Classes/AppDelegate.m

```objective-c
- (NSString*)documentsFolder
{
    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory,
                                                         NSUserDomainMask, YES);
    NSString *filePath = [paths objectAtIndex:0];
    return filePath;
}
```

Before we construct the NSPersistentStoreCoordinator, we need to decide where to store the persistent store file. On the desktop in an application with a single persistent store, we would save the file to the Application Support folder. However, on Cocoa Touch devices, there is no such location. Instead, each application has its own sandboxed Documents directory designed for the storage of files. This is where we will write our persistent store. Using code similar to what we used on the desktop to find the Application Support folder, we will find the Documents folder specific to our application.

Download Recipe/Classes/AppDelegate.m

```objective-c
- (NSPersistentStoreCoordinator*)persistentStoreCoordinator
{
    if (persistentStoreCoordinator) return persistentStoreCoordinator;

    NSFileManager *fileManager = [NSFileManager defaultManager];
    NSString *docFolder = [self documentsFolder];
    if (![fileManager fileExistsAtPath:docFolder]) {
        [fileManager createDirectoryAtPath:docFolder attributes:nil];
    }

    NSString *filePath = nil;
    filePath = [docFolder stringByAppendingPathComponent:@"recipes.sqlite"];
    if (![fileManager fileExistsAtPath:filePath]) {
        NSString *defaultDB = [[NSBundle mainBundle] pathForResource:@"recipes"
                                                            ofType:@"sqlite"];
        NSError *error = nil;
        if (![[NSFileManager defaultManager] copyItemAtPath:defaultDB
                                                   toPath:filePath
                                                    error:&error]) {
            NSLog(@"%@:%s Error copying file %@", [self class], __cmd, error);
        }
    }

    NSURL *url = [NSURL fileURLWithPath:filePath];
    NSManagedObjectModel *mom = [self managedObjectModel];
    persistentStoreCoordinator = [[NSPersistentStoreCoordinator alloc]
                                  initWithManagedObjectModel:mom];

    NSError *error = nil;
    if (![persistentStoreCoordinator addPersistentStoreWithType:NSSQLiteStoreType
                                                  configuration:nil
                                                           URL:url
                                                       options:nil
                                                         error:&error]) {
        return persistentStoreCoordinator;
    }

    [persistentStoreCoordinator release], persistentStoreCoordinator = nil;
    NSDictionary *ui = [error userInfo];
    if (![ui valueForKey:NSDetailedErrorsKey]) {
        NSLog(@"%@:%s Error adding store %@", [self class], __cmd,
              [error localizedDescription]);
    } else {
        for (NSError *suberror in [ui valueForKey:NSDetailedErrorsKey]) {
            NSLog(@"%@:%s Error: %@", [self class], __cmd,
                  [suberror localizedDescription]);
        }
    }
    NSAssert(NO, @"Failed to initialize the persistent store");
    return nil;
}
```

Once we have the NSManagedObjectModel constructed, the next step is to build the persistent store coordinator. Again, this code is nearly identical to the desktop version but with a few differences. First, for the moment, I have turned off the versioning check because we have only one version on the iPhone. When we release version 2 in the future, we will need to turn that back on.

The second major difference has to do with default settings. We initially check for the existence of a database file in the application's Documents directory, but if it does not exist, then we copy one from within the bundle of the application itself. This gives us a set of “defaults” or “samples” for the user who is accessing the iPhone application for the very first time. By doing this, we can present the user with an inviting list of recipes when they launch our application instead of an empty table view.

Download Recipe07/Classes/AppDelegate.m

```objective-c
- (NSManagedObjectContext *)managedObjectContext
{
    if (managedObjectContext) return managedObjectContext;

    NSPersistentStoreCoordinator *coord = [self persistentStoreCoordinator];
    if (!coord) return nil;

    managedObjectContext = [[NSManagedObjectContext alloc] init];
    [managedObjectContext setPersistentStoreCoordinator:coord];

    return managedObjectContext;
}
```

The last method we need to implement is the -managedObjectContext method. Since we did all the hard work either in the -managedObjectModel method or in the -persistentStoreCoordinator method, this method is even simpler than its desktop cousin. We request a reference to the NSPersistentStoreCoordinator, and assuming that it is not nil, we initialize an NSManagedObjectContext, add the NSPersistentStoreCoordinator to it, and return the resulting NSManagedObjectContext. Since we will either have an existing persistent store from the last time the user ran the application or have a default store copied over, there is no need to check the Type table as we have previously. It is guaranteed either to be there or to be intentionally cleared out by the user.

### Persistent Store Formats

Similar to Core Data on the desktop, several persistent formats are available on Cocoa Touch devices. However, one format is missing that I have grown to love. The XML format is not available currently on the iPhone. I suspect this is to force us to use something that is far more memory efficient such as the SQLite store. It is also possible that it was skipped because of dependencies on other APIs that are also not available at this time. Whatever the reason, the XML store is not available to us, and we should be using the SQLite store in every situation possible.

Besides the SQLite persistent store format, we also have access to the binary and in-memory formats. However, both of these formats require
