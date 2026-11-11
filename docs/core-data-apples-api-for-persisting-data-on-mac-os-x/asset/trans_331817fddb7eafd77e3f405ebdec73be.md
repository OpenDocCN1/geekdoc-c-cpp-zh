
```xml
<string>Grokking Recipes</string>
<key>ImagePath</key>
<string>App.icns</string>
<key>Type</key>
<string>app</string>
<key>Entities</key>
<dict>
  <key>com.pragprog.GrokkingRecipes.Author</key>
  <array>
    <string>com.apple.syncservices.RecordEntityName</string>
    <string>name</string>
    <string>recipes</string>
  </array>
  <key>com.pragprog.GrokkingRecipes.Ingredient</key>
  <array>
    <string>com.apple.syncservices.RecordEntityName</string>
    <string>cost</string>
    <string>name</string>
    <string>quantity</string>
    <string>recipes</string>
    <string>unitOfMeasure</string>
  </array>
  <key>com.pragprog.GrokkingRecipes.Recipe</key>
  <array>
    <string>com.apple.syncservices.RecordEntityName</string>
    <string>desc</string>
    <string>lastUsed</string>
    <string>name</string>
    <string>serves</string>
    <string>type</string>
    <string>author</string>
    <string>ingredients</string>
    <string>image</string>
  </array>
  <key>com.pragprog.GrokkingRecipes.RecipeIngredient</key>
  <array>
    <string>com.apple.syncservices.RecordEntityName</string>
    <string>quantity</string>
    <string>unitOfMeasure</string>
    <string>ingredient</string>
    <string>recipe</string>
  </array>
  <key>com.pragprog.GrokkingRecipes.Type</key>
  <array>
    <string>com.apple.syncservices.RecordEntityName</string>
    <string>name</string>
  </array>
  <key>com.pragprog.GrokkingRecipes.UnitOfMeasure</key>
  <array>
    <string>com.apple.syncservices.RecordEntityName</string>
    <string>name</string>
<string>ingredients</string>
<string>recipeIngredients</string>
</array>
</dict>
</dict>
</plist>
```

## 8.5 修改NSPersistentStoreCoordinator

关于Sync Services，有一点必须始终牢记：我们希望它快速——越快越好。如果它变慢，各种坏事都可能发生。例如，电脑可能在同步过程中进入睡眠，用户可能退出应用程序，网络连接可能中断——这样的例子不胜枚举。因此，我们要确保当同步真正发生时，它能够非常迅速。不幸的是，Core Data虽然在自身环境下算得上快速，但对于同步来说可能太慢。为了解决这个问题，NSPersistentStoreCoordinator在Sync Services框架的类别中附带了一个额外的方法。这个方法`setStoresFastSyncDetailsAtURL:forPersistentStore:`定义了一个额外的存储，供Sync Services在准备下一次同步操作时存储信息。这个额外存储不是数据的副本，而是类似于关于NSPersistentStore中各种对象的备注，可在同步过程中用来加快速度。

需要注意，没有这个额外设置，Core Data存储库的同步将无法工作。如果你遇到其他应用程序的同步无法工作的问题，务必检查快速同步存储是否已设置并创建。

将这种存储添加到我们的应用程序，需要对我们的-persistentStoreCoordinator方法做一处小幅改动。

```objective-c
NSPersistentStore *store;
store = [persistentStoreCoordinator addPersistentStoreWithType:NSXMLStoreType
                                                     configuration:nil
                                                                  URL:nil
                                                               options:nil
                                                                  error:&error];

if (!store) {
    NSLog(@"%@:%s presenting error no store", [self class], __cmd);
    [[NSApplication sharedApplication] presentError:error];
    return nil;
}

NSString *fss = @"GrokkingRecipes.fastsyncstore";
fss = [applicationSupportFolder stringByAppendingPathComponent:fss];
NSURL *fsdURL = [NSURL fileURLWithPath:fss];

[persistentStoreCoordinator setStoresFastSyncDetailsAtURL:fsdURL
                                      forPersistentStore:store];

return persistentStoreCoordinator;
```

在这段代码片段中，有两个重要变化。首先，我们不再检查对addPersistentStoreWithType:configuration:URL:options:error:的调用是否返回nil，而是将其结果赋给一个局部变量。我们这样做是为了能在后面将它传递给setStoresFastSyncDetailsAtURL:forPersistentStore:方法。接下来，我们为快速同步存储构建一个写入路径。由于我们将数据存储在Application Support文件夹中，因此将它放在主持久化存储旁边是合理的。如果我们使用的是文档应用程序，那么将它存储在其他地方或使用唯一文件名可能更合适。路径构建好后，我们将该路径以及对NSPersistentStore的引用一起传递给NSPersistentStoreCoordinator上的类别方法setStoresFastSyncDetailsAtURL:forPersistentStore:。这就是我们为启用Sync Services支持而对Core Data栈所做的唯一修改。

## 8.6 创建同步助手

现在是将所有部分组合起来的时候了。虽然这段代码几乎可以放在任何地方，但为了清晰起见，我决定将所有同步代码分离到单独的类中。最初编写这段代码时，我把它放到了AppDelegate.m中，但很快就发现这导致该对象过于复杂、难以理解。因此，我决定将同步代码分离成一个小型辅助类。

### NSPersistentStoreCoordinatorSyncing

正如我在基础知识（第8.1节，*同步服务基础知识*，第141页）中提到的，Sync Services需要一个回调来让我们的客户端了解正在发生的事情。准确地说，我们既需要一个回调，也需要一个协议。回调由Sync Services使用，让我们的应用程序知道同步即将发生。协议允许我们监听该同步，并在同步过程中回答问题。我们的同步助手将实现名为NSPersistentStoreCoordinatorSyncing的协议。

```objc
for (NSError *suberror in [ui valueForKey:NSDetailedErrorsKey]) {
    NSLog(@"%@", suberror);
}
[NSApp presentError:error];
}
error = nil;
```

我们的SyncHelper在初始化时接受两个参数：一个是对AppDelegate的引用，一个是指向NSError的指针。如果注册过程出现问题，NSError会被填充，SyncHelper将返回nil。如果发生这种情况，我们将向用户呈现错误并继续。

在SyncHelper内部，我们将对AppDelegate的引用赋给一个ivar，并尝试将我们自己注册为Sync Services的客户端，然后开始同步。

```objc
// Download SyncServices/SyncHelper.m
- (id)initWithDelegate:(id)_delegate error:(NSError**)error
{
    if (!(self = [super init])) return nil;
    delegate = _delegate;

    ISyncClient *client = [self syncClient:error];
    if (!client) {
        [self autorelease];
        return nil;
    }
    [client setSyncAlertHandler:self
            selector:@selector(client:mightWantToSyncEntityNames:)];
    if (![self performSync:error]) {
        [self autorelease];
        return nil;
    }

    return self;
}
```

在这个方法中，我们将SyncHelper的这个实例设置为Sync Services的回调，以便在同步即将于我们的应用程序外部启动时通知我们。当这发生时，我们会收到发送到-client:mightWantToSyncEntityNames:的消息，并做出相应的反应。这个对象初始化中最复杂的部分是如何获取对ISyncClient对象的引用。由于在我们的应用程序生命周期中会多次获取这个引用，因此已将它放在单独的方法中。

```objective-c
(ISyncClient *)syncClient:(NSError **)error
{
    NSString *ident = [[NSBundle mainBundle] bundleIdentifier];
    ISyncClient *client;
    NSDictionary *dict;
    ISyncManager *manager = [ISyncManager sharedManager];
    NSBundle *mainBundle = [NSBundle mainBundle];

    @try {
        client = [manager clientWithIdentifier:ident];
        if (client) return client;
```

尝试获取ISyncClient引用时，我们做的第一件事是使用我们的包标识符作为名称，向ISyncManager请求它。如果我们之前已经在ISyncManager注册过，那么这次调用将返回我们的客户端，我们就完成了。如果这是我们第一次经历这个过程，那么该调用将返回nil，我们将不得不在ISyncManager处注册。

```objective-c
NSString *path = [mainBundle pathForResource:@"GrokkingRecipes"
                                      ofType:@"syncschema"];
if (![manager registerSchemaWithPath:path]) {
    NSString *err = NSLocalizedString(@"Failed to register the schema",
                      @"Failed to register the schema");
    dict = [NSDictionary dictionaryWithObject:err
                        forKey:NSLocalizedDescriptionKey];
    *error = [NSError errorWithDomain:@"PragProg"
                                  code:8001
                              userInfo:dict];

    return nil;
}
```

这就是我们构建的同步模式发挥作用的地方。由于我们的客户端尚未注册，所以我们知道，因为我们是数据的发起者，我们的模式也尚未注册。因此，第一步是在我们的应用程序中找到GrokkingRecipes.syncschema包，并在ISyncManager中注册它。如果这步不成功，我们就会填充NSError并返回nil。假设成功了，下一步就是注册我们的客户端。

```objective-c
path = [mainBundle pathForResource:@"ClientDescription"
                             ofType:@"plist"];
client = [manager registerClientWithIdentifier:ident
                              descriptionFilePath:path];
```

