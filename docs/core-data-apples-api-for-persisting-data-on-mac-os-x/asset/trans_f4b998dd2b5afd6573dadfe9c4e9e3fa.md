
下载 RecipeCT/Classes/MainViewController.m

```objective-c
- (UITableViewCell *)tableView:(UITableView *)tableView
    cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    static NSString *cellIdentifier = @"cellIdentifier";
    UITableViewCell *cell = nil;
    cell = [tableView dequeueReusableCellWithIdentifier:cellIdentifier];
    if (!cell) {
        cell = [[[UITableViewCell alloc] initWithStyle:UITableViewCellStyleSubtitle
                                       reuseIdentifier:cellIdentifier] autorelease];
        [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];
    }
    [self updateCell:cell fromRecipe:[[self resultsController]
                                      objectAtIndexPath:indexPath]];

    return cell;
}
```

因为我们的表格只有一种行样式，所以这个类比那些具有多种行类型的表格中的类更简单。我们首先尝试出队一个 UITableViewCell，以便复用它。如果没有可出队的单元格，我们就构造一个新的。由于每个单元格都会显示一个披露指示器，因此我们在新单元格的初始化过程中配置它。

一旦获得单元格，就需要填充它。由于我们会在控制器中的多个位置填充和/或更新单元格，因此填充单元格的逻辑已被抽象到其自己的方法中。因此，我们的 -tableView:cellForRowAtIndexPath: 需要获取该行实体的引用，并将其传递给 -updateCell:fromRecipe: 方法。

由于 NSFetchedResultsController 类能够感知 UITableView，我们不需要编写任何复杂代码来获取指定对象。只需调用一次 -objectAtIndexPath: 并传入所引用的 NSIndexPath 对象，就能得到相关菜谱。

### 实现 -updateCell:fromRecipe: 方法

每当创建或更新单元格时，都需要配置其内容。幸运的是，我们使用了 3.0 中包含的一种新表格视图单元格样式，因此不需要进行任何复杂的视图构建和布局。然而，由于单元格的更新可能发生在 MainViewController 中的多个位置，我们已将实现移至其自己的方法中。

```objective-c
- (void)updateCell:(UITableViewCell *)cell fromRecipe:(RecipeEntity*)recipe
{
    [[cell textLabel] setText:[recipe name]];
    NSString *text = nil;
    text = [NSString stringWithFormat:@"Serves: %@", [recipe serves]];
    [[cell detailTextLabel] setText:text];
}
```

由于我们使用的是标准单元格布局之一，填充单元格只需设置 textLabel 属性和 detailTextLabel 属性即可。

### 实现 -controllerWillChangeContent: 方法

在回顾了更有趣的 UITableViewDataSource 方法之后，剩下的就是实现 NSFetchedResultsControllerDelegate 方法。我们需要实现四个方法。第一个是 -controllerWillChangeContent: 方法。该方法在每个通知周期（可能包含多次变更）中调用一次，它让我们有机会为即将执行的变更设置视图。由于我们只显示了一个 UITableView，因此为这些变更所做的设置非常简单。

```objective-c
- (void)controllerWillChangeContent:(NSFetchedResultsController*)controller
{
    [[self tableView] beginUpdates];
}
```

### 实现 -controller:didChangeObject:atIndexPath:forChangeType:newIndexPath: 方法

这个方法正是 NSFetchedResultsController 的核心所在。每当实体被插入、删除、更改或移动时，都会调用此方法。此方法的确切触发时机是在通过 NSManagedObjectContext 的 -save: 方法保存变更之后。一旦保存完成，每个变更都会经过此方法。

```objective-c
- (void)controller:(NSFetchedResultsController*)controller
    didChangeObject:(id)anObject
        atIndexPath:(NSIndexPath*)indexPath
      forChangeType:(NSFetchedResultsChangeType)type
       newIndexPath:(NSIndexPath*)newIndexPath
{
    NSArray *paths = [NSArray arrayWithObject:newIndexPath];
    NSIndexSet *section = [NSIndexSet indexSetWithIndex:[newIndexPath section]];

    switch (type) {
        case NSFetchedResultsChangeInsert:
            [[self tableView] insertRowsAtIndexPaths:paths
                                  withRowAnimation:UITableViewRowAnimationFade];
            break;
        case NSFetchedResultsChangeDelete:
            [[self tableView] deleteRowsAtIndexPaths:paths
                                  withRowAnimation:UITableViewRowAnimationFade];
            break;
        case NSFetchedResultsChangeMove:
            [[self tableView] deleteRowsAtIndexPaths:paths
                                  withRowAnimation:UITableViewRowAnimationFade];
            [[self tableView] insertRowsAtIndexPaths:paths
                                  withRowAnimation:UITableViewRowAnimationFade];
            break;
        case NSFetchedResultsChangeUpdate:
            [self updateCell:[[self tableView] cellForRowAtIndexPath:indexPath]
                 fromRecipe:[[self resultsController] objectAtIndexPath:indexPath]];
            break;
    }
}
```

对于每个变更，我们首先确定发生了哪种类型的变更。如果发生了插入或删除，我们会将该信息传递给 UITableView，以便 UITableView 能够处理该变更。在插入的情况下，表格视图随后会分别查询 -tableView:numberOfRowsInSection: 和 -tableView:cellForRowAtIndexPath: 方法。在每种情况下，如果行在屏幕上可见，UITableView 都会为该行的变更添加动画。

在行被移动的情况下（如果排序属性发生足够大的变化而需要重新排序，就会出现这种情况），UITableView 会处理行位置变化的动画（同样，前提是这些行当前在屏幕上可见）。

在最后一种可能的情况下，即实体的属性发生变更，我们会调用 -updateCell:fromRecipe: 方法，并将相关的 Recipe 实体和 UITableViewCell 传递给它。

### 实现 -controller:didChangeSection:atIndex:forChangeType: 方法

除了实体变更之外，NSFetchedResultsController 中的变更还可能导致分区数量发生变化。例如，如果每个分区代表字母表中的一个字母，而我们添加了一个新菜谱，它是该字母下的第一个菜谱，这可能会导致一个

![](img/ffa5f756dbdb501d7886468ffb761ad4_203_0.png)

*图 10.6：Cocoa Touch 菜谱应用程序表格视图*

受 Core Data 影响的分区变更。其余方法在随附的示例代码中实现。

## 构建详情视图控制器

好消息是，几乎所有与 Core Data 的交互都已完成。坏消息是，详情视图包含应用程序中最复杂的用户界面代码。尽管在此示例中我们不会实现整个用户界面，但仍有相当多的代码用于处理字段编辑。

详情视图的基本设计如下一页的图 10.7 所示。该视图的主要部分是一个表格视图以及一个自定义头部视图。头部视图中包含一个 UIImageView、一个 UILabel 和一个 UITextField。菜谱名称包含在 UITextField 中，该控件默认处于禁用状态。当点击编辑按钮时，

下载 RecipeCT/Classes/RecipeDetailViewController.m

```objective-c
- (void)setEditing:(BOOL)editing animated:(BOOL)animated
{
    [super setEditing:editing animated:animated];
    [self.navigationItem setHidesBackButton:editing animated:YES];

    [[self titleLabel] setEnabled:editing];

    if (editing) return;
    NSManagedObjectContext *context = recipe.managedObjectContext;
    NSError *error = nil;
    if (![context save:&error]) return;

    NSLog(@"save error %@, %@", error, [error userInfo]);
    exit(-1); // Fail
}
```

由于我们使用 NSFetchedResultsController，它会自动监视 NSManagedObjectContext 的变更并将其广播给其委托。因此，只需保存 NSManagedObjectContext，就会自动处理其他视图控制器中的任何变更通知。

## 概述

在本节中，我们探讨了将 Core Data 添加到 Cocoa Touch 应用程序所带来的影响。与桌面端类似，Core Data 有助于消除大量处理对象层级以及将数据持久化到磁盘的代码。通过将 Core Data 添加到 Cocoa Touch 项目，我们可以进一步减少开发应用程序所需的代码量，并进一步缩短上市时间。

## 10.5 进一步探索

由于本章我们完全聚焦于 Core Data，因此没有涵盖此应用程序的所有方面。我们也没有完成该应用程序并使其达到面向消费者的就绪状态。

有趣的是，随着 Cocoa Touch v3.0 的发布，Apple 还发布了一个使用 Core Data 的 iPhone 示例菜谱应用程序。该应用程序可供所有拥有 iPhone 开发者账户的人使用，我强烈建议查看该项目中提供的解决方案。

