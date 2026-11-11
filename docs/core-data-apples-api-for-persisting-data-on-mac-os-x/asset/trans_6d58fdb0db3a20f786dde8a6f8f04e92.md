

```objective-c
selector = @selector(testObjectFetch);
fetchTimer = [NSTimer scheduledTimerWithTimeInterval:15.0
                                                 target:self
                                               selector:selector
                                               userInfo:nil
                                                repeats:YES];
}
```

-startTestTimers 会启动一系列定时器，这些定时器会持续调用我们的测试方法。我们保留对每个定时器的引用，以便之后能够优雅地关闭它们。

### -disconnect 实现

每当我们关闭客户端应用程序时，我们都希望关闭定时器，并关闭与服务器的连接。-disconnect 会逐一处理每个 NSTimer 引用并将其失效。所有定时器都关闭后，它会从服务器代理获取 NSConnection 并将其失效。

下载 DistributedCClient/AppDelegate.m

```objective-c
- (void)disconnect
{
    [pingTimer invalidate], pingTimer = nil;
    [fetchTimer invalidate], fetchTimer = nil;
    [insertTimer invalidate], insertTimer = nil;
    [deleteTimer invalidate], deleteTimer = nil;
    [childDeleteTimer invalidate], childDeleteTimer = nil;
    [childInsertTimer invalidate], childInsertTimer = nil;

    NSConnection *connection = [(NSDistantObject *)server connectionForProxy];
    [connection invalidate];
    server = nil;
}
```

### -testPing 实现

我们的第一个测试方法也是最简单的一个。我们在服务器上调用 -ping 方法，除此之外不做任何事。我们根本不期望服务器返回任何内容。这个方法的作用是让服务器生成一条日志语句。这让我们能够观察服务器，并看到连接确实正在进入。另一个好处是它让测试保持简单。使用这个方法，我们可以确认 Bonjour 服务和分布式对象工作正常，而无需猜测应用程序其他部分的某些其他逻辑是否才是失败的真正原因。如果 ping 无法通过，我们就知道要么是 Bonjour 服务失败，要么是分布式对象失败。

```objective-c
- (void)testPing
{
    [server ping];
}
```

### -testObjectFetch 实现

-testObjectFetch 是我们通过分布式对象链接测试的第一个复杂方法。在这个测试中，我们构造一个 NSPredicate，并将其传给服务器，以便针对 NSManagedObjectContext 执行。正如我之前提到的，将 NSManagedObjectContext 本身通过分布式对象传递，会在 Core Data 栈内部产生一些终止性异常，因此我们通过在服务器上尽可能多地执行 Core Data 工作来避免这一点。这里我们传入要搜索的实体名称和 NSPredicate。服务器将返回一个 NSArray，其中包含符合该 NSPredicate 的实体。这个方法中一个值得注意的有趣之处是，我们没有使用新的 for 循环来访问返回的 NSArray。由于这个 NSArray 实际上是服务器上 NSArray 的 NSDistantObject 代理，新的 for 循环无法正确处理它。因此，我们需要改用较旧的 NSEnumerator。

```objective-c
- (void)testObjectFetch
{
    NSString *test = [GUID substringToIndex:3];
    NSPredicate *predicate = nil;
    predicate = [NSPredicate predicateWithFormat:@"name contains[c] %@", test];

    NSArray *results = [server objectsOfName:@"Test" withPredicate:predicate];

    NSEnumerator *enumerator = [results objectEnumerator];
    NSManagedObject *object;
    while (object = [enumerator nextObject]) {
        [object setValue:GUID forKey:@"name"];
    }

    [self setFilteredObjects:results];
}
```

为了跨分布式对象展示并测试 KVO，我们遍历 NSArray 中的 NSManagedObject 对象，并将它们的 name 更新为 a

### 11.4 小结

每当我们开始处理网络上的多台计算机或应用程序间通信时，代码就会开始变得极其复杂。然而，至少通过这种设计，我们可以尽可能地将 Core Data/持久化与分布式对象/网络分离。这样做，我们避免了原本需要的大量锁和同步。

正如我们在本章开头所讨论的，这并不是一个非常可扩展的设计，但在正式独立数据库显得大材小用的情况下，这种设计实际上相当有效。没有用户配置，也不需要设置外部应用程序；我们只需在一台机器上启动一个应用程序，在另一台机器上启动另一个应用程序，然后让它们通信。最大的坑在于 NSManagedObjectContext。只要我们不去尝试跨分布式对象共享它，就可以相当透明地使用 Core Data。

我们在这里构建的设计也可以用于对等环境，而不是客户端-服务器设计。多个对等节点可以使用 Bonjour 发现彼此，并使用分布式对象同步各自的数据存储，这样每个设备都拥有完整且最新的数据集副本。在这种情况下，用户可以在自己的每台机器上安装我们的应用程序，每当它们彼此靠近（即位于同一局域网）时，它们就会自动更新彼此。这用户体验可真不错！

## 第 12 章

### 秘诀：动态参数

如果你有一个文档风格的应用程序，你将需要处理文档特定的参数或设置。例如，在文字处理器中，有些设置特定于某个文档，而有些设置则适用于整个应用程序。在存储应用程序级参数时，我们有一个很好的实现：NSUserDefaults。然而，对于文档级参数，API 并没有提供可复用的存储系统。在本章中，我们将在 Core Data 中构建这个可复用的存储系统。

系统级和用户级偏好设置在 OS X 上非常有用，而且易于访问。在应用程序任意位置调用一次 NSUserDefaults 的 standardUserDefaults，就能立即访问当前登录用户的默认设置。然而，有时我们不想在用户级别存储偏好设置，而是更愿意在文件级别存储它们。

当我们使用 Core Data 应用程序时，第一个想法就是为这些参数创建一个表，并从 Core Data API 中访问它们。然而，问题出现在访问这些参数时。它不再是对 NSUserDefaults 的 standardUserDefaults 的一次调用；现在它看起来更像这样：

```objective-c
- (void)clunkyParameterAccess
{
    NSManagedObjectContext *moc = [self managedObjectContext];
    NSFetchRequest *request = [[NSFetchRequest alloc] init];
    [request setEntity:[NSEntityDescription entityForName:@"parameter"
                                      inManagedObjectContext:moc]];

    [request setPredicate:[NSPredicate predicateWithFormat:@"name == %@",
                                              @"default1"]];

    NSError *error = nil;

    NSManagedObject *param = [[moc executeFetchRequest:request
                                                 error:&error] lastObject];
    if (error) {
        NSLog(@"%@:%s Error fetching param: %@", [self class], _cmd, error);
        return;
    }

    NSLog(@"%@:%s Parameter value %@", [self class], _cmd,
          [param valueForKey:@"value"]);
}
```

更糟的是当我们需要设置参数时：

下载 CDPreferences/MyDocument.m

```objc
- (void)clunkyParameterWrite
{
    NSManagedObjectContext *moc = [self managedObjectContext];
    NSFetchRequest *request = [[NSFetchRequest alloc] init];
    [request setEntity:[NSEntityDescription entityForName:@"parameter"
                                  inManagedObjectContext:moc]];

    [request setPredicate:[NSPredicate predicateWithFormat:@"name == %@",
                                              @"default1"]];

    NSError *error = nil;

    NSManagedObject *param = [[moc executeFetchRequest:request
                                                  error:&error] lastObject];
    if (error) {
        NSLog(@"%@:%s Error fetching param: %@", [self class], _cmd, error);
        return;
    }

    if (!param) {
        param = [NSEntityDescription insertNewObjectForEntityForName:@"Parameter"
                                            inManagedObjectContext:moc];
        [param setValue:@"default1" forKey:@"name"];
    }

    [param setValue:@"SomeValue" forKey:@"value"];
}
```

对此最明显的解决方案是将这段代码抽象到某个地方，以便我们只需一行代码就能访问它。如果……岂不是……

