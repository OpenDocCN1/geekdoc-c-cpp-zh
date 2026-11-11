

### 9.6 小结

在本章中，我们回顾了如何在多线程应用程序中使用 Core Data，并为我们的食谱应用程序添加了一些非常有用的功能。我们了解到，每个线程都需要有自己的 NSManagedObjectContext，并且 NSManagedObject 实例绝不应跨线程传递。我们还学习了如何跨线程发送通知，以便一个 NSManagedObjectContext 中的更改可以在其他 NSManagedObjectContext 实例中更新。

![](img/ffa5f756dbdb501d7886468ffb761ad4_184_0.png)

图 10.1：iPhone OS 新建项目对话框

## 将现有应用程序升级到 Core Data

我们中的许多人从 SDK 最初发布时就开始开发 iPhone 应用程序，因此你很可能有一个现有应用程序，并希望将其与 Core Data 集成。幸运的是，在现有项目中构建 Core Data 栈并不需要很多代码。

### 向项目中添加数据模型

与桌面端一样，Cocoa Touch 上的 Core Data 需要一个数据模型来定义数据实体的结构。因此，第一步是通过选择“文件”>“新建文件”向项目中添加数据模型。在出现的对话框中，如果我们选择“资源”部分，就可以创建一个新的数据模型，如下一页的图 10.2 所示。

除了创建新的数据模型之外，我们还可以使用现有应用程序中的现有数据模型。在本章后面的第 195 页第 10.4 节 *iPhone 食谱* 中，我们将在新的 iPhone 应用程序中使用桌面食谱应用程序的数据模型。数据模型在桌面端和 Cocoa Touch 之间是兼容的，这使我们不仅能够共享模型，还能共享底层的持久化存储。

![](img/ffa5f756dbdb501d7886468ffb761ad4_185_0.png)

图 10.2：向项目中添加数据模型

### 添加 Core Data 代码

一旦有了可用的数据模型，下一步就需要添加代码来加载 Core Data 栈。这段代码的确切位置取决于你的应用程序设计。由于 iPhone 上没有文档式应用程序，因此每个 Cocoa Touch 应用程序通常只有一个数据模型和一个持久化存储。尽管我仍然喜欢把 Core Data 代码放在应用程序委托中，但把它放在其他地方也可能合理。无论代码放在哪里，它都与桌面端非常相似。首先，我们需要初始化数据模型。

下载 RecipeCT/Classes/AppDelegate.m

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

这看起来应该非常熟悉，因为它与你在桌面端构建 NSManagedObjectModel 的方式完全相同。我们获取 .mom 文件（如果数据模型有多个版本，则为 .momd）的路径，并用它来初始化 NSManagedObjectModel。

下载 Recipe/Classes/AppDelegate.m

```objective-c
- (NSString*)documentsFolder
{
    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory,
                                                         NSUserDomainMask, YES);
    NSString *filePath = [paths objectAtIndex:0];
    return filePath;
}
```

在构建 NSPersistentStoreCoordinator 之前，我们需要决定将持久化存储文件存放在哪里。在桌面端，对于只有一个持久化存储的应用程序，我们会把文件保存到 Application Support 文件夹。然而，在 Cocoa Touch 设备上，没有这样的位置。相反，每个应用程序都有自己的沙盒 Documents 目录，专门用于存储文件。我们将在这里写入持久化存储。使用与桌面端查找 Application Support 文件夹类似的代码，我们将找到特定于我们应用程序的 Documents 文件夹。

下载 Recipe/Classes/AppDelegate.m

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

一旦构建好 NSManagedObjectModel，下一步就是构建持久化存储协调器。同样，这段代码与桌面版几乎相同，但有一些差异。首先，目前我已关闭版本检查，因为我们在 iPhone 上只有一个版本。将来发布版本 2 时，我们需要重新开启它。

第二个主要差异与默认设置有关。我们首先检查应用程序的 Documents 目录中是否存在数据库文件，但如果不存在，就从应用程序自身的 bundle 内复制一个。这为用户首次访问 iPhone 应用程序提供了一组“默认值”或“示例”。通过这样做，当用户启动我们的应用程序时，我们可以向他们呈现一份吸引人的食谱列表，而不是一个空表视图。

下载 Recipe07/Classes/AppDelegate.m

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

我们需要实现的最后一个方法是 -managedObjectContext 方法。由于所有繁重工作都已经在 -managedObjectModel 方法或 -persistentStoreCoordinator 方法中完成，因此这个方法甚至比它在桌面端的对应方法更简单。我们请求对 NSPersistentStoreCoordinator 的引用，并假设它不是 nil，然后初始化一个 NSManagedObjectContext，将 NSPersistentStoreCoordinator 添加到其中，并返回得到的 NSManagedObjectContext。由于我们要么拥有用户上次运行应用程序时留下的现有持久化存储，要么已经复制了一个默认存储，因此不需要像之前那样检查 Type 表。可以保证它要么存在，要么已被用户有意清除。

### 持久化存储格式

与桌面端上的 Core Data 类似，Cocoa Touch 设备上也有几种持久化格式可用。然而，有一种我已经逐渐喜欢的格式缺失了。XML 格式目前在 iPhone 上不可用。我怀疑这是为了迫使我们使用内存效率高得多的格式，例如 SQLite 存储。也有可能是因为它依赖于目前同样不可用的其他 API 而被跳过。无论原因是什么，XML 存储对我们不可用，我们应该在所有可能的情况下使用 SQLite 存储。

除了 SQLite 持久化存储格式之外，我们还可以使用二进制格式和内存中格式。然而，这两种格式都需要

