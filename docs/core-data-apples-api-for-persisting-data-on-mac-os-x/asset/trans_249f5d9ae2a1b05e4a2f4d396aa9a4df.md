
模式注册完成后，现在需要注册我们的客户端。这里我们获取之前创建的 `ClientDescription.plist` 的引用，并将其连同我们的唯一标识符一起传给 ISyncManager。这会注册我们的客户端，并返回对我们 ISyncClient 对象的引用。现在客户端已注册，我们需要开启与所有其他客户端类型的同步。这样我们就能决定要参与哪些同步。同样，由于我们是数据的发起方，我们希望参与每一次同步。

```objc
[client setShouldSynchronize:YES
              withClientsOfType:ISyncClientTypeApplication];
[client setShouldSynchronize:YES
              withClientsOfType:ISyncClientTypeDevice];
[client setShouldSynchronize:YES
              withClientsOfType:ISyncClientTypeServer];
[client setShouldSynchronize:YES
              withClientsOfType:ISyncClientTypePeer];
```

此方法的最后一步是捕获并处理我们收到的任何异常。在本书写作时，这个过程仍可能抛出少数异常，因此我们要确保捕获这些异常，将它们封装进 NSError，并交回给调用方。假设没有出问题，我们就返回 ISyncClient。

```objc
} @catch (NSException *exception) {
    dict = [NSDictionary dictionaryWithObject:[exception reason]
                         forKey:NSLocalizedDescriptionKey];
    *error = [NSError errorWithDomain:@"PragProg"
                                  code:8002
                              userInfo:dict];
    return nil;
}
return client;
}
```

## 执行同步

既然已经注册了模式和同步客户端，我们需要能够处理同步可能发生的两种方式。我们可以主动发起同步，也可以接收即将发生同步的通知。幸运的是，我们以相同方式处理这两种情况。

2. 反正它们本来就该在那里。

当同步即将开始时，我们要做的第一件事是对 NSManagedObjectContext 执行保存。保存完成后，就可以告诉 Sync Services 我们已准备好执行同步。因此，我们需要对全局保存方法做一点小改动。既然我们已经在第 7 章 *Spotlight、Quick Look 与 Core Data* 第 114 页把所有保存逻辑放进了一个方法中，那么从那里启动同步操作就非常合理。

下载 `SyncServices/AppDelegate.m`

```objc
NSLog(@"%@:%s Performing sync", [self class], _cmd);
if (![_syncHelper performSync:&error]) {
    return NO;
}
```

保存操作一返回，我们就想调用 SyncHelper，并让它执行 -performSync:。我们向该方法传入一个 NSError，以便在同步期间发生错误时能获知。

下载 `SyncServices/SyncHelper.m`

```objc
- (BOOL)performSync:(NSError **)err
{
    ISyncClient *client = [self syncClient:err];
    if (!client) return NO;

    NSLog(@"Starting sync");
    NSPersistentStoreCoordinator *store = [delegate persistentStoreCoordinator];
    return [store syncWithClient:client
                     inBackground:YES
                           handler:self
                            error:err];
}
```

在 -performSync: 方法中，我们获取 ISyncClient 的新引用以及 NSPersistentStoreCoordinator 的引用。借助这两个引用，我们将使用 Sync Services 类别中为 NSPersistentStoreCoordinator 添加的第二个方法，并通过 syncWithClient:inBackground:handler:error: 方法请求同步。如果同步失败，则向调用方返回 NO，并填充 NSError。由于我们把 SyncHelper 作为此次同步的处理程序传入，而它实现了 NSPersistentStoreCoordinatorSyncing 协议，因此它将收到前面讨论的所有通知。

为了确保元数据是最新的，我们需要完善其中一个委托回调方法，具体来说是 -persistentStoreCoordinator:didFinishSyncSession:。在该方法中，我们要检查 NSManagedObjectContext 中是否有更改；如果有，就更新元数据并保存上下文。

我们需要做的最后一件事是处理外部同步请求。既然我们已经将 `-client:mightWantToSyncEntityNames:` 定义为外部同步启动时要调用的方法，那么此时就需要请求一次保存。

```objc
- (void)client:(ISyncClient *)client mightWantToSyncEntityNames:(NSArray *)names
{
    NSError *error = nil;
    if (![delegate save:&error]) {
        [NSApp presentError:error];
    }
}
```

由于我们保存 NSManagedObjectContext 的调用也会启动同步，因此无需再做其他事情。

## 8.7 Syncrospector 工具

Sync Services 还额外复杂，调试和测试都相当困难。由于 truth 实际上是一个黑盒，通常我们只能试探它并观察响应。幸运的是，在较新的 Xcode 构建版本中，Apple 提供了一个名为 Syncrospector 的开发工具的可用副本。你可以在 Developer 目录（取决于你安装的位置，通常在 /Developer）、Applications 文件夹，最后在 Utilities 子文件夹中找到 Syncrospector。这个工具让我们可以窥探 truth 内部，甚至重置数据或强制进行不同类型的同步。

### 客户端面板

客户端面板显示 Sync Services 的所有已知客户端。在此面板中，我们可以查看客户端是否已正确注册、它注册了哪些数据类，以及每个实体的状态。我们还可以从此面板强制同步客户端。参见下页的图 8.3。在 Syncrospector 内所有可用面板中，这是我最常用的两个面板之一。

![](img/ffa5f756dbdb501d7886468ffb761ad4_158_0.png)

图 8.3：Syncrospector 的客户端面板

### Truth 面板

Truth 面板允许我们查看当前位于 truth 中的数据。对于每个实体，我们可以看到它最后更新于何时，以及是谁更改了它。当我试图弄清楚数据出了什么问题并查看是谁弄乱它时，我发现这个面板很有用。

### 历史面板

历史面板允许我们查看 truth 内部曾经发生过的每一个事务。借助此面板，无论事情发生得多久以前，都可以追踪数据在何处被搞乱以及被谁搞乱。

### 模式面板

模式面板是我非常频繁使用的另一个面板。它显示 truth 中注册的所有模式，并允许我们检查它们的全部详细信息。此外，还可以通过此面板从 truth 中删除某个模式。最后，此面板可用于清除 truth 和客户端中的数据。这在测试期间非常有用。

![](img/ffa5f756dbdb501d7886468ffb761ad4_159_0.png)

图 8.4：Syncrospector 的模式面板

## 8.8 小结

由于本书聚焦于 Core Data，我们尚未涵盖 Sync Services 的不少领域。若想全面掌握该框架的知识，你应更深入地研究以下主题。

### 模式版本管理

这一主题目前仍在不断变化，到本书出版时可能已经改变。就目前而言，如果你的模式需要更改，那么理想情况下，该数据的所有客户端都应更新到最新模式。如果它们不更新，用户可能会得到不一致的结果。

此外，模式绑定到 NSManagedObjectModel 的特定版本。因此，如果数据模型发生变化，很可能需要新的模式，或者至少模式需要引用最新的数据模型。

## 第 9 章

## 多线程与 Core Data

你的主力机器很可能至少有两个核心。如果你开发用的每台机器都至少有两个甚至更多核心，我也不会感到惊讶。对于运行在 Mac OS X 上的每个中等复杂度应用来说，多线程很快将成为必需。这是我们开发人员在开发应用时需要接受并规划的事情。幸运的是，Mac OS X 中的新特性使我们更容易进行多线程，也更不容易出错。

然而，问题在于 Core Data 本质上并非线程安全。它仍然希望并期望在单线程中运行。因此，当我们开始为应用引入多线程时，必须注意正确使用 Core Data，以避免线程问题。

### 9.1 为什么 Core Data 不是线程安全的？

你可能会惊讶地发现，Cocoa 和 Objective-C 中有很多东西并非线程安全，而 Core Data 只是众多例子之一。例如，每当你更改 GUI 控件时，都建议在主线程上执行，因为 UI 不是线程安全的。

在多线程中处理 Core Data 的最大问题是保持 NSManagedObjectContext 同步。当在不同于创建 NSManagedObjectContext 的线程上对 NSManagedObject 做出更改时，上下文不会感知到该更改，并可能持有过期数据。这就是 Core Data 中非线程安全的部分。NSPersistentStore、NSPersistentStoreCoordinator 和 NSManagedObjectModel 都完全线程安全，但 NSManagedObjectContext 不是。
