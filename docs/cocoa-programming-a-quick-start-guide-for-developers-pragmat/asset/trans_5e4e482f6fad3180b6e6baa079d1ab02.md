
字典来消除我们代码另一部分中的一个 if。这次我们将使用另一种技术。

### 16.7 将表格列标识符用作键

在 if 语句中，我们可以不使用列标题，而使用表格列的另一个属性，称为*标识符*。标题是显示在列顶部表头单元格中的文本。该文本用于与应用用户沟通。标识符对最终用户不可见。数据源使用它来标识列。我们可以将标识符用作字典中的键，或用作属性或方法的名称。

因此，在 Interface Builder 中选择表格的第一列，并使用 Attributes inspector 将 Identifier 设置为 icon。同样，将第二列的 Identifier 设置为 localizedName。我并非随意选择这些名称；它们是我希望每一列中显示的 NSRunningApplication 类中的属性名称。

![](img/9355405953264484a02198b0e3d25b7e_264_0.png)

现在我们可以调用与标识符同名的方法。它只是该名称属性的 getter。

```objective-c
- (id)tableView:(NSTableView *)aTableView
       objectValueForTableColumn:(NSTableColumn *)aTableColumn
                              row:(NSInteger)rowIndex {
    return [[self.runningApps objectAtIndex:rowIndex]
        performSelector:NSSelectorFromString([aTableColumn identifier])];
}
```

下面大致说明用图标和名称填充表格时必须发生的过程。首先，表格视图询问其数据源这个表格有多少行。数据源回复 [runningApps count]。然后，对于表格中的每个单元格，表格视图询问其数据源：“这里放什么？”数据源现在用数组中索引与行号匹配的应用程序信息来回答。^4 并且在每个单元格中，数据源用与单元格所在列的标识符匹配的属性值来响应。相当巧妙。

看看这如何简化了代码——无需做出选择。更好的是，即使我们引入新列，也不必更改这段代码。

### 16.8 后续内容预览

事实证明，属性的一个优点是它们遵循某种命名约定，使我们能够将对象当作字典来处理。换句话说，我们可以像向字典传入键一样，传入我们想要其值的属性名称。你将在第 19 章*键值编码*（第 298 页）中学到更多相关内容。

这是一个应用该技术的绝佳场景，我简直等不及到那一章了。你不需要理解 KVC 就能欣赏这个应用。我们不再将标识符转换为 SEL 再执行该选择器，而是使用 `valueForKey:` 方法，并将标识符作为键传入。

下载 Tables/HelloApplication34/ActivityController.m

```objective-c
- (id)tableView:(NSTableView *)aTableView
    objectValueForTableColumn:(NSTableColumn *)aTableColumn
        row:(NSInteger)rowIndex {
    return [[self.runningApps objectAtIndex:rowIndex]
        valueForKey:[aTableColumn identifier]];
}
```

这又是使用 Cocoa 编程时让我会心一笑的一点。

### 16.9 练习：添加和移除行

我们的迷你 Dock 现在会显示应用程序启动时正在运行的应用程序的图标和名称快照。接下来，让我们通过添加正在启动的应用程序并移除正在终止的应用程序来更新列表。

4. 幸运的是，它们的计数都从 0 开始。

我们本可以在每次应用程序启动或终止时，从 NSWorkspace 的 runningApplications 数组重新生成列表。不过，我在这里的目标是向你展示如何向表格视图的底层数据源添加和移除内容，然后更新视图。

你已经有在应用程序启动或终止时响应的委托方法。实现其中一个方法，通过向 runningApps 末尾添加条目并更新表格视图，将正在启动的应用程序添加到表格视图底部。同样，实现另一个方法，通过从 runningApps 中移除相应条目并更新表格视图，从表格视图中移除正在终止的应用程序。

### 16.10 解决方案：添加和移除行

我们将需要从 ActivityController 中访问表格视图。向头文件添加一个 outlet：

下载 Tables/HelloApplication35/ActivityController.h

```objective-c
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface ActivityController : NSViewController <ActivityMonitorDelegate,
NSTableViewDelegate, NSTableViewDataSource> {
    NSMutableArray *runningApps;
    NSTableView *table;
}
@property(retain) NSMutableArray *runningApps;
@property IBOutlet NSTableView *table;
@end
```

在 Interface Builder 中，将此 outlet 连接到你的表格视图。

回到 Xcode，你应该已经将这两个方法添加到 ActivityController 的实现文件中。然后向 runningApps 数组添加和移除相应条目，并告诉表格视图重新加载。^5

下载 Tables/HelloApplication35/ActivityController.m

```objective-c
- (void) applicationDidLaunch: (NSRunningApplication *) app {
    [self.runningApps addObject:app];
    [self.table reloadData];
}

-(void) applicationDidTerminate: (NSRunningApplication *) app {
    [self.runningApps removeObject:app];
    [self.table reloadData];
}
```

5. 另外，你应该记住，每次我们在头文件中添加属性时，都需要在相应的实现文件中合成它。

### 16.11 手动移除行

到目前为止，我们已经在数据源中发起更改，并反映在表格中。在本节中，我们还将利用这样一个事实：我们已将 ActivityController 也设置为表格视图的委托。

让我们向应用程序添加一个 Remove 按钮。这将允许用户从列表中移除应用程序。仅当用户在表格视图中选择应用程序时，该按钮才会变为可见。然后，如果用户点击该按钮，所选应用程序将从列表中消失，我们还会再次隐藏该按钮。

首先向 ActivityController 头文件添加一个 outlet 和一个 action。outlet 将连接到新按钮，action 将是按钮被点击时调用的方法。

```objective-c
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface ActivityController : NSViewController <ActivityMonitorDelegate, NSTableViewDelegate, NSTableViewDataSource> {
    NSMutableArray *runningApps;
    NSTableView *table;
    NSButton *deleteButton;
}
@property(retain) NSMutableArray *runningApps;
@property IBOutlet NSTableView *table;
@property IBOutlet NSButton *deleteButton;
-(IBAction)removeRow:(id)sender;
@end
```

在 Interface Builder 中，在表格视图下方添加一个小方形按钮。我们不会给它设置标题，而是在上面显示一个减号。为此，打开 Attributes Inspector，将按钮的图像设置为 NSRemoveTemplate。同时选中 Hidden 复选框。

![](img/9355405953264484a02198b0e3d25b7e_268_0.png)

将 ActivityController 的 deleteButton outlet 连接到该按钮，并同样连接 removeRow: action。保存。

现在你需要在 ActivityController 中实现两个方法。第一个是用户选择行时调用的委托方法。我们要做的只是在选中行时让按钮可见。

下载 Tables/HelloApplication35/ActivityController.m

```objective-c
- (void)tableViewSelectionDidChange:(NSNotification *)notification {
    [self.deleteButton setHidden:NO];
}
```

当用户点击 Delete 按钮时，我们从 runningApps 数组中移除所选行并重新加载表格视图。我们还会确保表格视图中不再选中任何行，并隐藏该按钮。

下载 Tables/HelloApplication35/ActivityController.m

```objective-c
- (IBAction)removeRow:(id)sender {
    [self.runningApps removeObjectAtIndex:[self.table selectedRow]];
    [self.table deselectAll:nil];
    [self.table reloadData];
    [self.deleteButton setHidden:YES];
}
```

再一次，我喜欢这段代码读起来几乎就像我们要完成之事的描述。

点击 Build & Run，你将能够选择行并将它们从列表中移除。遗憾的是，如果你退出 HelloApplication 并再次启动它，已移除的项目又会回来。在下一章中，我们将为此示例添加持久化和偏好设置。
