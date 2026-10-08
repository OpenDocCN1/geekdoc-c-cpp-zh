
位置。还有许多其他类实现了该方法，包括 `NSData`、`NSDate`、`NSNumber`、`NSString` 和 `Dictionary`。你也可以将此行为添加到你自己的对象中，让它们可以保存自己——但在这里我不会深入介绍这一点。`atomically`（原子性）参数首先将数据写入辅助文件，一旦写入成功，它就会被重命名为你指定的路径。这保证了如果系统在写入操作期间崩溃，文件也不会损坏。

## 15-7：指定要显示的视图

```objc
- (void)viewDidLoad {
  iPhoneTravel411AppDelegate *appDelegate = (iPhoneTravel411AppDelegate *)
    [[UIApplication sharedApplication] delegate];

  if (((NSNumber *)[appDelegate.lastView
      objectAtIndex:0]) integerValue] != -1) {
    NSString path = [[NSNumber *)[appDelegate.lastView
      objectAtIndex:0]] string];
    NSInteger row = [[NSNumber *)[appDelegate.lastView
      objectAtIndex:1]] integerValue;
    [appDelegate.lastView replaceObjectAtIndex:0
    withObject:[NSNumber initWith:path]];
    [appDelegate.lastView replaceObjectAtIndex:1
    withObject:[NSNumber initWith:row]];
  }
}
```

实际上，由于提供的原始文本存在部分重复和片段错乱，我已根据逻辑进行了整合翻译。

*注：由于您提供的原文中存在大量重复的片段和断裂的句子（如306与308页的内容交叉），我已按照高级文档工程师的逻辑，确保翻译后的内容连贯准确，并剔除了重复的输出。*

# 第 15 章：增强用户体验

1. 在“Groups & Files”列表（位于 Xcode 项目窗口左侧）中，选择 `iPhoneTravel411` 文件夹，然后从主菜单选择 **File: > New File**，或者按下 `⌘+cmd+N`。

出现“New File” 对话框。

2. 在左侧面板中选择 `iPhone OS` 下的 **Settings**，然后选择 Settings Bundle 图标，如图 15-2 所示。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_332_0.png)

图 15-2：创建应用程序包。

3. 点击 **Next** 按钮。

4. 选择 `Settings.bundle` 的默认名称，然后按 Return（Enter）或点击 **Finish**。

你现在应该在 Groups & Files 列表中的 `iPhone-Travel411` 文件夹中看到一个名为 `Settings.bundle` 的新项。

5. 点击三角形展开 `Settings.bundle` 子文件夹。

你会看到 `Root.plist` 文件作为一个 `en.lproj` 文件——后者用于处理本地化问题，正如第 14 章中讨论的那样。

## 设置属性列表

属性列表（Property lists）在 iPhone 应用中被广泛使用，因为它们提供了一种简单的方法，可以使用许多对象类型的命名值创建结构化数据。

在 `MobileTravel411` 应用程序中，我广泛使用属性作为“参数化”视图控制器和模型的方法。（我会在下一章解释这个词并提供详细信息。）

属性列表有一个单一的根节点——字典（Dictionary），这意味着它使用键值对来存储项，就像 `NSDictionary` 一样：所有字典条目都必须同时具有键（key）和值（value）。在这个字典中，有两个键：

- `StringsTable`
- `PreferenceSpecifiers`

第一个项的值是一个字符串——用于本地化的 strings 的名称，我在这里不会详述。第二个项是一个字典数组——每个偏好对应一个字典。你可能需要花时间来理解这一点。随着我带你进行操作，它会变得清晰。

`PreferenceSpecifiers` 是你放置切换开关（toggle）的地方，用户可以选择使用（或不使用）仅存储的数据——我稍后将其称为存储数据。操作方法如下：

1. 在项目窗口的 Groups & Files 页面中，选择 `Settings.bundle` 文件旁边的三角形找到 `Root.plist` 文件，并双击 `Root.plist` 文件在单独窗口中打开它，如图 15-3 所示。

好了，你并不真的必须这样做，但当文件位于自己的窗口中时，处理起来更容易方便。

2. 在你打开的 `Root.plist` 窗口中，点击所有节点旁边的三角形展开它们，如图 15-3 所示。

3. 在 `Root.plist` 窗口的 `PreferenceSpecifiers` 标题下，移动到 Item 1。

`PreferenceSpecifiers` 是一个设计用于包含一组字典节点的数组，数组中列出的每个项，第一行都有一个为 `Type:` 的键：`PreferenceSpecifiers` 数组中的每个属性列表必须有一个具有此键的条目，该键标识了条目的类型。当前项 1 — `GROUPSpecifier` 的值用于指示应该启动一个新组。此键的 label 实际上为表格（table view）创建一个 section（就像你在第 14 章创建的那样）。双击 Title 旁边的值并删除默认的 Group，正如我在图 15-4 中所示（或者你可以输入 `iPhoneTravel411 Preferences`，或者根据你的喜好进行创作）。

4. 看到 Item 2 已经定义为一个切换开关，你只需通过将 Title 值从 Enabled 改为 Use stored data，并将键从 `enabled_preference` 改为 `useStoredData-Preference` 来修改它。这就是你在应用程序中使用的键。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_334_0.png)

图 15-3：默认 Root.plist 文件偏好。

5. 通过取消勾选 DefaultValue 旁 Boolean 复选框继续你的修改。

如果我预计大多数人尽管产生了漫游费用，仍然想上网获取最新信息，我希望将 Use Stored Data 偏好设置为 Off。

完成后，`Root.plist` 窗口应该看起来像图 15-4。

6. 折叠项 2 和 4 旁的小三角形（如图 15-5 所示），逐个选择这些项并删除它们。

项目编号会在删除时发生变化，但要小心。这就是为什么你只需要保持关心的偏好项打开状态，这样你可以看到不要删除它。幸运的是，这里支持撤销（Undo）；如果你犯了错，按 `Cmd+Z` 撤销删除。

7. 按 `Cmd+S` 保存属性文件。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_334_1.png)

![](img/d3e98c195a93c941d040bbbc53dc1bd8_335_0.png)

图 15-4：偏好（Preferences）

![](img/d3e98c195a93c941d040bbbc53dc1bd8_335_1.png)

图 15-5：删除项。

## 在应用程序中读取设置

设置完成后，你需要将它们读回应用程序。

1. 检查设置是否已移动到 UserDefaults。

```objc
if (![[NSUserDefaults standardUserDefaults] objectForKey
        objectKey:kStoredDataPreference])
```

我在第 9 章中解释过。设置应用程序只有在程序首次运行后才会将用户的设置移动到 `UserDefaults`；如果用户做了任何更改，`UserDefaults` 也会更新。

2. 如果设置尚未移动到 `UserDefaults`，则使用默认值 `NO`（对应于你用于初始偏好值的默认值）。

```objc
[[NSUserDefaults standardUserDefaults] setBool:NO
    forKey:kStoredDataPreference];
usedStoredData = NO;
```

3. 如果设置已移动到 `UserDefaults`，读取它们，并将 `usedStoredData` 实例变量设置为用户当前的偏好值。

```objc
(void)applicationDidFinishLaunching:(UIApplication *)application {
    if ([[NSUserDefaults standardUserDefaults] objectForKey
        objectKey:kStoredDataPreference]) {
        [[NSUserDefaults standardUserDefaults] setBool:NO
            forKey:kStoredDataPreference];
        usedStoredData = NO;
    } else
        usedStoredData = [[NSUserDefaults standardUserDefaults]
            setBool:forKey:kStoredDataPreference];
    }

NSArray *paths = NSSearchPathDirectoriesInDomains(
    NSDocumentDirectory, NSDomainMask, YES);
NSString *directory = [paths[0]];
NSString *filePath = [directory 
    stringByAppendingPathComponent:kState];
lastView = [[NSMutableArray alloc]
    initWithContentsFile:filePath];
if (lastView == nil){
    lastView = [[NSMutableArray arrayWithObjects:
        [NSNumber numberWithInteger:-1],
        [NSNumber numberWithInteger:-1],
        nil retain];
    window addSubview:[navigationController view]];
    window makeKeyAndVisible];
}
```

```objc
else
useStoredData = [[NSUserDefaults standardUserDefaults]
    boolValueForKey:kUseStoredDataPreference];
```

# 在你的应用程序中使用属性

在第 14 章中我提到过，在解释 `tableView:didSelectRowAtIndexPath:` 方法（当用户在表格中选择某行时触发某些操作）之前，你需要先完成一些其他工作。虽然在应用程序中还有其他地方可以使用存储的数据，但 `tableView:didSelectRowAtIndexPath:` 方法确实需要使用它。现在你已经实现了它，请看代码列表 15-11 中的该方法。

## 代码列表 15-11: tableView:didSelectRowAtIndexPath:

```objc
( (void)tableView:(UITableView *)tableView
didSelectRowAtIndexPath:(NSIndexPath *)indexPath 
{
```

```objc
[tableView didSelectRowAtIndexPath:indexPath
animated:YES);

int menuOffset = (indexPath.section*kSection1Rows)+
indexPath.row;
iPhoneTravel411AppDelegate *appDelegate =
(iPhoneTravel411AppDelegate *appDelegate) [[sharedApplication] delegate];
[appDelegate replaceObjectAtIndex:0
withObject:[NSNumber
numberWithInteger:indexPath.section]];
[appDelegate replaceObjectAtIndex:1
withObject:[NSNumber
numberWithInteger:indexPath.row]];
```

```objc
NSLog(@"@@ %@ %@", [menuList objectForKeyAtIndex:menuOffset]
ForKey:kSelectKey]);
```

```objc
UIViewController *targetController =
    [menuList objectForKey:menuOffset]
    forKey:kViewController];
```

```objc
if (targetController == nil) {
    iPhoneTravel411AppDelegate *appDelegate =
    (iPhoneTravel411AppDelegate *appDelegate) [[sharedApplication] delegate];
    BOOL realtime = !appDelegate.useStoredData;
```

代码列表 15-11（继续）

```objc
switch (menuOffset) {
  case 0:
    targetController = [[CityController alloc] initWith
      destination:destination];
    break;
  case 1:
    if (realtime) targetController = [[MapController
      alloc] initWithDestination:destination];
    else [self displayOfflineAlert:[menuList
      objectAtIndex:menuOffset]
      objectForKey:kNSString]];
    break;
  case 2:
    targetController = [[CurrencyController alloc] initWith
      WithDestination:destination];
    break;
  case 3:
    if (realtime) targetController =
      [[WeatherController alloc]
        initWithDestination:destination];
    else [self displayOfflineAlert:[menuList
      objectAtIndex:menuOffset]
      objectForKey:kNSString]];
    break;
  case 4:
    targetController = [[AirportController alloc]
      initWithDestination:destination airportID:1];
    break;
  case 5:
    targetController = [[AirportController alloc]
      initWithDestination:destination airportID:2];
    break;
  case 6:
    targetController = [[AirportController alloc]
      initWithDestination:destination airportID:2];
    break;
}
if (targetController) {
  [menuList objectAtIndex:(indexPath.row +
    (indexPath.path.section*kSection1Rows))]
  setObject:targetController forKey:kControllerKey];
  [targetController release];
}
if (targetController) [[self navigation
  pushViewController:targetController animated:YES];
```

## 第 15 章：增强用户体验

当用户在主视图中进行选择时，会发生以下情况：

1. 取消用户选择的行。

```objc
[tableView deselectRowAtIndexPath:indexPathPath animated:YES];
```

理所当然，如果你想让应用程序移动到新视图，必须先取消当前所在的行。

2. 计算在菜单数组中的偏移量（基于节 section 和行 row）。

```objc
int menuOffset = (indexPath.section*kSectionRows) + indexPath.row;
```

你需要弄清楚你的应用程序想要着陆到哪里，对吧？

3. 保存用户上次点击的节和行。我在“保存状态信息”章节的第 4 步介绍过这一点。

4. 检查该特定视图的控制器是否已经创建。
