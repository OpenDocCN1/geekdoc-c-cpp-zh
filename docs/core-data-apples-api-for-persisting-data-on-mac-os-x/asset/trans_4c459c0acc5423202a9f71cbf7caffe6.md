
此设计的位置位于用户主目录下 Library 目录中的 Application Support 目录内。

一旦我们确认存在或添加了适当的目录，下一步就是获取对 NSManagedObjectModel 的引用，这将在第 68 页的 4.5 节“NSManagedObjectModel”中讨论。有了对 NSManagedObjectModel 的引用，我们就可以用该模型初始化 NSPersistentStoreCoordinator。

在初始化 NSPersistentStoreCoordinator 之后，我们需要将实际的 NSPersistentStore 添加到其中。可以向 NSPersistentStoreCoordinator 添加多个 NSPersistentStore，这在处理被拆分到多个文件中的数据时很有用。不过，在我们的示例中，我们只有一个文件。将 NSPersistentStore 添加到 NSPersistentStoreCoordinator 的一部分工作是指定存储的类型。不同类型的存储及其优点将在第 97 页的第 6 章“性能调优”中讨论。当我们把 NSPersistentStore 添加到 NSPersistentStoreCoordinator 时，可能会发生失败。因此，我们要检查错误，并在错误发生时进行处理。

通常，一旦我们初始化了 NSPersistentStoreCoordinator 并将其添加到 NSManagedObjectContext 中，我们就很少再碰它了。在大多数情况下，我们唯一想再次访问它的时机是处理手动迁移。

### 4.7 获取属性

除了 NSFetchRequest 对象之外，我们还能够定义对象之间的延迟关系。获取属性在某种程度上是关系与 NSFetchRequest 的混合体。严格来说，获取属性并不是一种关系，并且直到请求该属性时才会被实现。当访问该属性时，Core Data 会执行底层的 NSFetchRequest 并返回结果。与普通关系不同，获取属性返回的是 NSArray，而不是 NSSet。

在实践中，我发现获取属性不如创建存储的获取请求或在代码中构建获取请求那样有用和灵活。通常，当情况需要获取属性时，对相关实体进行子类化、在代码中执行 NSFetchRequest 并返回结果往往更容易。

### 4.8 小结

本章介绍了 Core Data 的许多组成部分。随着我们继续深入探索 Core Data，请将本章作为参考，了解 Core Data 的各个部分以及它们如何组合在一起。到本书结束时，这些元素中的每一个对你来说都应该像今天的 NSString 和 NSArray 一样熟悉。

## 版本管理与迁移

就像作战计划一样，没有任何代码库能在与用户接触后保持不变。一旦用户开始使用某个应用程序，他们就会想要改变它。即使代码只是为我们自己而写，我们作为用户也会想要改变一些东西。例如，我们可能需要添加一个属性、添加一个新对象，或者只是为了适应这些变化而重构结构。这些改动可能相当复杂，并且总是需要改变数据的存储方式。尽管即使没有存储数据，数据迁移也能正常工作，但有一些数据可供操作会对后续工作更有用。因此，如果你还没有添加任何食谱，我建议在我们继续之前先添加一些。

从 Mac OS X 10.5 Leopard 开始，Apple 已使 Core Data 用户的数据迁移几乎变得轻而易举。在为 Leopard 开发时，版本管理已包含在 Core Data API 中，作为开发者，我们只需付出相对较少的努力，就可以轻松地将数据存储从一个版本迁移到另一个版本。根据迁移的复杂程度，我们开发者所需付出的努力可能微不足道，也可能相当复杂。

以我们在第 14 页第 2 章*Core Data 入门*中开始的项目为例，我们将在后续版本中为其添加一些附加功能。在版本 2 中，我们将添加为食谱标记作者以及标记“最后使用”日期的功能。这样，我们就知道是谁创造了这道美味佳肴，以及我们最后一次制作它是什么时候。我们当然不希望连续两天不小心做同一道菜！最后，我们将从 `Recipe` 实体的 `Type` 属性中移除 Meat 和 Fish 条目。任何标记为 Meat 或 Fish 的食谱条目都将改为更新为 Entrée。

![](img/ffa5f756dbdb501d7886468ffb761ad4_73_0.png)

图 5.1：默认模型问题对话框

在版本 3 中，我们将通过提取配料并形成回到食谱的多对多关系，对存储库进行一些规范化。此外，我们将添加购物清单的概念，以便更容易确保我们在下次去商店时买齐所有配料。最后，我们将把 unitOfMeasure 属性从 RecipeIngredient 实体中提取到它自己的实体中，并允许这个新实体链接到新的配料实体。这将为我们提供一个用于各种计量单位的查找列表，并降低人为错误的风险。

### 5.1 迁移前的一些维护工作

在我们实际发布会迁移数据的新版应用程序之前，我们需要先为用户完成一次小幅“维护”更新。通常我们会把这段代码添加到应用程序的第一个版本中，但以防我们编写第一个版本时还没有考虑版本管理（或者以防我们是为 Tiger 编写第一个版本），我们需要回到旧版本，并添加非常少量的代码来帮助我们的用户。

有些用户会下载应用程序的新版本只是为了“试用一下”，看看它是否值得升级费用或是否值得费这个麻烦。通常这不成问题，直到我们升级了用户底层的数据。然后事情就出岔子了。我们不希望发生的就是图 5.1 中显示的错误消息。

这是一种糟糕的用户体验，也是我们想要避免的。幸运的是，避免它的方法非常简单，我们可以在进行任何迁移之前将其添加到应用程序的维护版本中。这样，当用户在“测试”第二个版本后打开我们应用程序的第一个版本时，他们会收到一条友好的错误消息，或者你可以更进一步，恢复/访问他们数据的旧版本。

下载 GrokkingRecipes_v2/AppDelegate.m

```
if (![persistentStoreCoordinator addPersistentStoreWithType:NSXMLStoreType
                                              configuration:nil
                                                        URL:url
                                                    options:dict
                                                      error:&error]) {
    NSDictionary *ui = [error userInfo];
    if (ui) {
        NSLog(@"%@:%s %@", [self class], _cmd, [error localizedDescription]);
        for (NSError *suberror in [ui valueForKey:NSDetailedErrorsKey]) {
            NSLog(@"\t%@", [suberror localizedDescription]);
        }
    } else {
        NSLog(@"%@:%s %@", [self class], _cmd, [error localizedDescription]);
    }
    NSAlert *alert = [[NSAlert alloc] init];
    [alert setAlertStyle:NSCriticalAlertStyle];
    [alert setMessageText:@"Unable to load the recipes database."];
    NSString *msgText = nil;
    msgText = [NSString stringWithFormat:@"The recipes database %@\n\n%@\n"
               @"is either corrupt or was created by a newer "
               @"version of Grokking Recipes. Please contact "
               @"support to assist with this error.\n\nError: ",
               [error localizedDescription]];
    [alert setInformativeText:msgText];
    [alert addButtonWithTitle:@"Quit"];
    [alert runModal];
    exit(1);
}
```

我们已将这段代码添加到食谱应用程序第一个版本的应用程序委托中的 -persistentStoreCoordinator 方法里。在我们应用程序的第一个版本中，如果在将 NSPersistentStore 添加到 NSPersistentStoreCoordinator 时发生错误，我们只会通过 [[NSApplication sharedApplication] presentError:error] 向用户呈现错误。通过这一更改，我们向用户提供了更多有用的信息，同时也把相当多有用的信息转储到日志中供我们查看。我们还会在所有未来版本的应用程序中保留这段代码，以帮助其“面向未来”。当然，这只是我们能做的最低限度，我建议添加其他选项。不过，最重要的一点已经到位。我们不会在没有 Core Data 栈的情况下让用户继续操作。我们最初的方式是
