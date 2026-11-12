
我们将 `WeightHistory` 对象作为文件呈现器传递。这意味着我们的 `WeightHistory` 类不会收到有关在协调块执行期间所做的更改的任何通知。通常，这正是我们想要的——但这也意味着我们完成后可能需要手动更新 UI。

最后，我们在后台队列上调用 `resolveConflictsWithCurrentURL:coordinator:` 方法。在这里使用后台线程非常重要。显然，从性能角度来看，我们绝不想在主线程上执行任何文件输入/输出操作——这会严重影响用户界面的性能。相反，我们应该始终在后台读取和写入数据。然而，更实际地说，在主线程上创建协调块可能导致应用程序死锁。我们绝对不希望这种情况发生。

接下来，让我们看一下 `resolveConflictsWithCurrentURL:coordinator:` 方法。

```objc
- (void)resolveConflictsWithCurrentURL:(NSURL*)currentURL
                 coordinator:(NSFileCoordinator*)coordinator {
    NSError* error;
    [coordinator
        coordinateReadingItemAtURL:currentURL
        options:0
        writingItemAtURL:currentURL
        options:NSFileCoordinatorWritingForMerging
        error:&error
        byAccessor:^(NSURL *inputURL, NSURL *outputURL) {
            // Load our data.
            NSData* data =
                [NSData dataWithContentsOfURL:inputURL];
            NSMutableArray* currentHistory =
                [NSKeyedUnarchiver unarchiveObjectWithData:data];
            // Read in all the old versions.
            NSArray* unresolvedVersions =
[NSFileVersion
    unresolvedConflictVersionsOfItemAtURL:inputURL];

// Merge the histories.
for (NSFileVersion* version in unresolvedVersions) {
    [self mergeCurrentHistory:currentHistory
        withConflictingVersion:version
        coordinator:coordinator];
}

// Sort the current history.
NSSortDescriptor* sortByDate =
    [NSSortDescriptor sortDescriptorWithKey:@"date"
                                   ascending:NO];
[currentHistory sortUsingDescriptors:
    [NSArray arrayWithObject:sortByDate]];

// Save the changes.
[self saveMergedHistory:currentHistory
                  toURL:outputURL
             coordinator:coordinator
              oldVersions:unresolvedVersions];
}]; // Current File Read/Write block.
if (error != nil) {
    NSLog(@"*** Error: Unable to perform a coordinated "
          @"read/write on our current history! %@ ***",
          [error localizedDescription]);
}
}
```

在这里，我们首先创建一个协调块，用于对当前 URL 进行读取和写入。所有协调块方法的工作方式类似。我们传入一个 URL，设置一些选项来定义要执行的读取或写入操作类型，然后传入一个块。协调器会确保系统处于良好状态。这可能涉及要求其他进程中的文件呈现器执行它们自己的读取或写入操作。例如，`NSFileCoordinatorWritingForMerging` 选项会强制所有相关文件呈现器在协调写入操作开始之前保存它们的更改。这有助于确保我们在开始进行更改之前拥有文件的最新版本。

接下来，协调器尝试获取文件锁。系统通常允许多个并发读取操作，而写入操作需要对文件的独占访问。这意味着写入操作会阻塞，直到所有当前正在执行的读取或写入操作完成。然后，一旦写入块开始运行，在其完成之前，其他读取或写入操作都无法开始。

与许多基于块的 API 不同，系统同步执行所有协调块操作。这意味着它会在方法返回之前执行我们的块参数。这使得将一系列读取和写入操作串联起来变得更加容易。还要注意，在创建协调块时我们提供了一个 URL。然后系统会向我们的块传递一个 URL 参数。在访问文件时，我们应该始终使用块的 URL 参数。毕竟，文件可能因另一个文件呈现器的写入操作而移动。因此，到我们的块运行时，我们提供的原始 URL 可能已不再有效。

> **注意：** 我们只需要与我们设备上的其他进程协调读取和写入操作。我们不需要在设备之间进行协调。通常，对于 iOS 设备，我们只需要与本地 iCloud 同步服务进行协调。因此，在我的 iPhone 上创建协调块可能会强制手机的 iCloud 服务将其更改写入磁盘（可能强制其下载文件的更新副本），但这不会影响我的 iPad 上运行的任何进程。

![](img/fe9fea534a8e7868f811f7cd33da015f_324_0.png)

即使在协调块中，`coordinateReadingItemAtURL:options:writingItemAtURL:options:error:byAccessor:` 也有些特别。它请求一个需要与写入操作协调的读取操作。在我们的场景中，我们希望读取当前文档、更新它，然后再次写入。尽管名称如此，它实际上只是一个智能的读取块。我们不能在其中直接执行写入操作。相反，我们必须创建一个嵌套的写入块并在那里执行写入操作。

在我们的代码中，我们从当前版本加载历史数组。然后我们获取所有冲突版本的列表。我们遍历这些版本，对每个冲突版本调用 `mergeCurrentHistory:withConflictingVersion:coordinator:`。稍后我们将看到，这将确保当前版本包含所有冲突版本中的所有条目。

遗憾的是，合并过程可能会使我们的历史数组变得无序。因此，我们按日期对其进行排序。我们创建一个排序描述符，它使用键值编码来访问我们的体重条目的 `date` 属性，并按降序对它们进行排序。

最后，我们调用 `saveMergedHistory:toURL:coordinator:oldVersions:` 来保存我们新的、合并后的历史记录，然后清理所有旧的冲突版本。请注意，在内部，此方法会创建嵌套的协调写入块。

现在让我们看一下 `mergeCurrentHistory:withConflictingVersion:coordinator:`。

```objc
- (void)mergeCurrentHistory:(NSMutableArray*)currentHistory
    withConflictingVersion:(NSFileVersion*)version
              coordinator:(NSFileCoordinator*)coordinator {
    NSError* readError;
    [coordinator
     coordinateReadingItemAtURL:version.URL
     options:0
     error:&readError
     byAccessor:^(NSURL *oldVersionURL) {
        NSData* oldData =
        [NSData dataWithContentsOfURL:oldVersionURL];
        NSArray* oldHistory =
        [NSKeyedUnarchiver unarchiveObjectWithData:oldData];
        [currentHistory unionWith: oldHistory];
    }];
    if (readError) {
        NSLog(@"*** Error: Unable to perform a coordinated read "
              @"on a previous version! %@ ***",
              [readError localizedDescription]);
    }
}
```

虽然这看起来有些复杂，但实际上我们只是在创建另一个协调读取块。在该块内部，我们从指定的冲突版本读取数据。然后我们调用 `NSMutableArray` 的 `unionWith:` 方法合并两个历史数组。

只有一个问题：`NSMutableArray` 没有 `unionWith:` 方法。没问题，我们只需要添加一个。

在项目导航器中，右键单击 `Model` 组并选择 New File。在模板面板中，选择 iOS > Cocoa Touch > Objective-C Category。将其命名为 `Union`，并确保它是 `NSMutableArray` 上的一个分类。

接下来，打开 `NSMutableArray+Union.h`，定义我们的 `unionWith:` 方法。

```objc
#import <Foundation/Foundation.h>
@interface NSMutableArray (Union)
- (void)unionWith:(NSArray*)array;
@end
```

切换到实现文件，并添加如下所示的方法：

```objc
- (void)unionWith:(NSArray*)array {
    NSMutableArray* toAdd =
    [[NSMutableArray alloc] initWithCapacity:[array count]];
    for (id entry in array) {
        if (![self containsObject:entry]) {
            [toAdd addObject:entry];
        }
    }
}
```
