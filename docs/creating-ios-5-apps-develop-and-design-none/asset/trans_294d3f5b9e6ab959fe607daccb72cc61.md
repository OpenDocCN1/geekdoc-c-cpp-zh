
现在，请向下滚动回到 viewDidLoad 方法。我们将在这里创建我们的文档。我们一步一步来。

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    // Override point for customization after application launch.
    NSFileManager* fileManager = [NSFileManager defaultManager];
    NSURL* ubiquitousURL =
    [fileManager URLForUbiquityContainerIdentifier:nil];
```

前几行代码只是获取默认文件管理器的引用，然后查找我们 iCloud 存储容器的 URL。请记住，如果 iCloud 不可用，这将返回 nil。此外，这个方法还会扩展我们的沙盒，使其包含 iCloud 容器——让我们能够调用其他 iCloud 方法。

```objc
NSDictionary *options;
if (ubiquitousURL != nil) {
    options = [NSDictionary dictionaryWithObjectsAndKeys:
        [NSNumber numberWithBool:YES],
        NSMigratePersistentStoresAutomaticallyOption,
        [NSNumber numberWithBool:YES],
        NSInferMappingModelAutomaticallyOption,
        @"com.freelancemadscience.Health_Beat.history",
        NSPersistentStoreUbiquitousContentNameKey,
        ubiquitousURL,
        NSPersistentStoreUbiquitousContentURLKey, nil];
} else {
    // Create options for local sandbox storage only.
    options = [NSDictionary dictionaryWithObjectsAndKeys:
        [NSNumber numberWithBool:YES],
        NSMigratePersistentStoresAutomaticallyOption,
        [NSNumber numberWithBool:YES],
        NSInferMappingModelAutomaticallyOption, nil);
}
```

在这里，我们创建一个选项字典。`UIManagedDocument` 在将 SQLite 持久化存储添加到其持久化存储协调器时，会将这些选项传递给 `addPersistentStoreWithType:configuration:URL:options:error:`。在这两种情况下，我们都启用了自动迁移和轻量级迁移。如果 iCloud 可用，我们还会设置启用自动 iCloud 支持所需的选项。`NSPersistentStoreUbiquitousContentNameKey` 设置内容的名称。这个名称用于在用户的所有不同设备上唯一标识我们的存储，确保应用程序能够找到并同步其更新。毫不奇怪，我们的所有存储都必须具有唯一名称。这里我们使用一个反向域名，后面跟上特定于应用程序的标签 `Health_Beat.history`。

我们还设置了 `NSPersistentStoreUbiquitousContentURLKey`。这个键应该包含我们某个 iCloud 存储容器内一个目录的 URL。我们可以将其放在 Documents 目录中——但这样一来，每一条单独的事务日志都会出现在我们的文档列表中。我们真的不希望用户只删除其中一两条日志——那可能会使我们的数据库处于糟糕的状态。相反，我们只使用 iCloud 容器的 URL。我们的事务日志将保存在容器内的 `com.freelancemadscience.Health_Beat.history` 目录中。

根据文档，Core Data 应该会自动为我们设置 `NSPersistentStoreUbiquitousContentURLKey` 键。然而，我在使用时遇到了问题，它生成的 URL 指向了与我的授权（entitlements）中定义的容器不同的容器。最简单的办法可能就是用一个已知的正确值来设置它。

```objc
NSURL* localURL = [fileManager URLForDirectory:
    NSDocumentDirectory
    inDomain:NSUserDomainMask
    appropriateForURL:nil
    create:NO
    error:nil];
NSURL* localCoreDataURL =
[localURL URLByAppendingPathComponent:@"MyData"];
// Now Create our document.
self.document =
[[UIManagedDocument alloc] initWithFileURL:localCoreDataURL];
self.document.persistentStoreOptions = options;
```

接下来，我们在本地沙盒内为我们的 SQLite 数据库创建一个 URL。我们使用该 URL 实例化我们的文档，然后设置持久化存储选项。再说一次，本地文档与 iCloud 同步文档之间的唯一区别就是持久化存储选项。

```objc
if ([fileManager fileExistsAtPath:[localCoreDataURL path]]) {
    [self.document openWithCompletionHandler: ^(BOOL success) {
        [self passDocumentToSubViewControllers];
    }];
} else {
    // Clean up the container.
    NSFileCoordinator* coordinator =
    [[NSFileCoordinator alloc] initWithFilePresenter:nil];
    [coordinator
     coordinateWritingItemAtURL:ubiquitousURL
     options:NSFileCoordinatorWritingForDeleting
     error:nil
     byAccessor:^(NSURL *newURL) {
        [[NSFileManager defaultManager]
         removeItemAtURL:newURL error:nil];
    }];

    [self.document
        saveToURL:localCoreDataURL
        forSaveOperation:UIDocumentSaveForCreating
        completionHandler:^(BOOL success) {
            [self passDocumentToSubViewControllers];
        }];
}
}
```

最后，如果文件存在，我们就打开它。否则，我们通过调用 saveToURL:forSaveOperation:completionHandler: 来创建一个新文件。在这两种情况下，我们都会在完成处理器中调用 passDocumentToSubViewControllers，将我们的文档传递给其他视图控制器。

请注意，在创建新文档之前，我们会清空容器。我们需要这段代码来绕开一个相当严重的问题。

事实证明，如果用户进入其 iCloud 设置并删除该文档，它将会自动恢复为本地文档。这些设备将不再将其更新同步到 iCloud。然而，我们的 iCloud 容器中仍然有事务日志。如果用户从设备上删除该应用，然后重新安装，它将会进入无效状态。应用将尝试加载事务数据，但无法加载，文档将无法打开。通过在创建新文档之前清空容器，我们可以防止这个问题。

> **注意：** 或者，我们可以使用 `NSMetadataQuery` 来确认文档是否存在于云中。如果找不到文档，我们就清空 iCloud 存储，并询问用户是否要再次上传。此外，`UIManagedDocument` 会为我们的日志创建一个目录。`NSMetadataQuery` 无法搜索目录。相反，我们搜索该软件包中的 `DocumentMetadata.plist` 文件。

![](img/fe9fea534a8e7868f811f7cd33da015f_415_0.png)

我们仍然需要创建 passDocumentToSubViewControllers。在类扩展中声明这个方法，然后按所示实现它。

```objc
- (void)passDocumentToSubViewControllers {
    // Create a stack, and load it with the view
    // controllers from our tabs.
    NSMutableArray* stack =
    [NSMutableArray arrayWithArray:self.viewControllers];
    // While we still have items on our stack.
    while ([stack count] > 0) {
        // Pop the last item off the stack.
        id controller = [stack lastObject];
        [stack removeLastObject];
        // If it is a container object, add its view
        // controllers to the stack.
        if ([controller
            respondsToSelector:@selector(viewControllers)]) {
            [stack addObjectsFromArray:
                [controller viewControllers]];
        }
        // If it responds to setDocument, pass our document.
        if ([controller
            respondsToSelector:@selector(setDocument:)]) {
            [controller setDocument:self.document];
        }
    }
}
```

这个方法的前半部分应该看起来很熟悉。这与我们在第 6 章中用来转发 WeightHistory 对象的代码相同。唯一真正的区别是，这一次我们把它提取成了独立的方法。

```objc
[[NSNotificationCenter defaultCenter]
    addObserverForName:
NSPersistentStoreDidImportUbiquitousContentChangesNotification
      object:[self.document.managedObjectContext
                    persistentStoreCoordinator]
      queue:nil
  usingBlock:^(NSNotification *note) {
          [self.document.managedObjectContext performBlock:^{
                  NSLog(@"Merging Changes");
                  [self.document.managedObjectContext
                    mergeChangesFromContextDidSaveNotification:note];
          }];
  }];
}
```

