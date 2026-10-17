
![](img/d3e98c195a93c941d040bbbc53dc1bd8_297_1.png)

![](img/d3e98c195a93c941d040bbbc53dc1bd8_297_2.png)

# 第 14 章：设置表格

为了看到表格视图的效果，你自然需要一个项目来展示它们。留着此考虑，启动 Xcode 并正式启动 iPhoneTravel411 项目。（如果你需要复习如何在 Xcode 中设置，请再看一遍第 4 章。）如图 14-3 所示，你需要选择“基于导航的应用程序”（Navigation-Based Application）模板。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_298_0.png)

图 14-3：基于导航的应用程序模板。

然后我将项目保存为 iPhoneTravel411，并放在桌面上的一个文件夹中，如图 14-4 所示。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_298_1.png)

图 14-4：命名并保存项目。

## 第四部分：工业级应用

你的新项目出现在 Xcode 窗口左侧的“分组与文件”（Groups & Files）列表中。接下来，看看当你点击项目文件夹中的“分组与文件”列表直到选中 `RootViewController` 时（如图 14-5 所示）发生了什么。Xcode 项目的主面板显示 `RootViewController` 是一个 `UITViewController`。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_299_0.png)

图 14-5：RootViewController。

数据源和代理（但不一定）实现在同一个对象中——该对象是 `UITViewController` 的子类。我计划在我的 iPhoneTravel41 应用中使用 `RootViewController`。

实现这五个（数一数，是五个）方法，并在 Interface Builder 中转转几圈，再加上你在 `ReturnMeApp` 中用过的同样的初始化方法和标准的内存管理方法，就可以创建一个能够响应表格中选择操作的表格视图。

`UITableView` 对象必须有一个数据源和一个代理。数据源提供表格视图的内容，而代理负责管理表格视图的外观和行为。数据遵循 `UITableViewDataSource` 协议——这并不意外。在上述方法中，`tableView:didSelectRowAtIndexPath:` 包含在 `UITableViewDelegate` 协议中。之前列出的其他方法都包含在 `UITableViewDataSource` 协议中。

数据源和代理（但不一定）实现在同一个对象中——该对象是 `UITViewController` 的子类。我计划在我的 iPhoneTravel41 应用中使用 `RootViewController`。

实现这五个（数一数，是五个）方法，并在 Interface Builder 中转转几圈，再加上你在 `ReturnMeApp` 中用过的同样的初始化方法和标准的内存管理方法，就可以创建一个能够响应表格中选择操作的表格视图。

还不错。

## 创建并格式化分组表格视图

表格视图有两种基本样式。默认样式被称为“普通”（plain），看起来不加修饰——就像原汁原味。它是一个列表：一个接一个地出现。不过，你可以对它进行索引，尽管联系人（Contacts）应用中的表格也是如此，因此它可以成为一个非常强大的工具。

另一种样式是分组表格视图（grouped table view）；不出所料，它允许你将条目分类到不同的类别。在图 14-2 中，你可以看到左侧是一个分组表格；右侧是一个普通表格。

分组表格没有索引。

当你配置分组表格视图时，还可以拥有页头（header）、页脚（footer）和分区标题（普通视图也可以有分区页头和页脚）。我稍后会展示如何设置分区标题。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_297_0.png)

![](img/d3e98c195a93c941d040bbbc53dc1bd8_297_1.png)

![](img/d3e98c195a93c941d040bbbc53dc1bd8_297_2.png)

## 让 UITViewController 工作

数据源和代理（但不一定）实现在同一个对象中——该对象是 `UITViewController` 的子类。我计划在我的 iPhoneTravel41 应用中使用 `RootViewController`。

实现这五个（数一数，是五个）方法，并在 Interface Builder 中转转几圈，再加上你在 `ReturnMeApp` 中用过的同样的初始化方法和标准的内存管理方法，就可以创建一个能够响应表格中选择操作的表格视图。

还不错。

## 添加分区

在分组表格中，每个组被称为分区（section）。在索引表格中，每个索引组也被称为分区。例如，在 iPod 应用中，所有以“A”开头的专辑是一个分区，以“B”开头的另一个，依此类推。虽然名称相同，但这与没有索引的分区不是回事。

你首先需要的两个方法如下：

```
numberOfSectionsInTableView:(UITableView *)tableView
tableView:(UITableView *)tableView
numberOfRowsInSection:(NSInteger)
```

每个方法分别返回一个整数，告诉表格视图某些信息——分区数量和给定分区的行数。

在列表 14-1 中，你可以看到在两个分区中各三行的代码。这些方法已经由“基于导航的应用程序”模板在 `RootViewController.file` 中为你实现。你需要删除现有的代码并将其替换为列表 14-1 所示的内容。

### 列表 14-1：修改 `numberOfSectionsInTableView:` 和 `tableView:numberOfRowsInSection:`

```objc
-(NSInteger)numberOfSectionsInTableView:
(UITableView *)tableView
return 2;

-(NSInteger)tableView:(UITableView *)tableView
numberOfRowsInSection:(NSInteger) section {
NSInteger rows;
switch (section) {
case 0:
rows = 4;
break;
case 1:
rows = 3;
break;
default:
break;
}
return rows;
}
```

记住，第一个分区从零开始，第一行也是如此。

尽管这已经是最简单的方法了，但并不是最好的方法。请继续阅读。

为了向你展示如何实现一个健壮的应用程序，我将使用常量表示节的数量以及每个节的行数。我会将这些常量放在一个名为 `Constants.h` 的文件中，该文件最终包含其他常量。我这样做纯粹出于防御性考虑（我知道这是为什么，因为后事事皆明），将它们声明为常量可以轻松更改行数和节数，而且有助于避免那些难以察觉的错误。

> 提示
>
> 我稍后会向你展示一些可以让生活变得容易、非常容易的技巧。这意味着要关注一些不那么显眼的通知和螺栓功能——你可以称之为“内存管理”——这些功能在实现过程中可能会很烦人，但如果以后再进行重构就会非常困难。我想引导你避开许多开发者走过的布满怪石的小径（也包括我），他们后来对此深感遗憾。

要实现 `Constants.h` 文件，你需要执行以下操作：

- 1. 从 Xcode 主菜单中选择 `File::New File`。

我建议在 `Groups & Files` 列表中选中 `Classes` 文件夹，这样文件就会被放置在其中。

- 2. 在弹出的 New File 对框中，从左侧列表（Mac OS X 标题下）选择 `Other`，然后在主面板中选择 `Empty File`，如图 14-7 所示。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_302_0.png)

图 14-7：创建一个空文件。

3. 在出现新对话框中，将文件命名为 `Constants.h`（如图 14-8 所示），然后点击 `Finish`。

空文件已保存在 `Classes` 文件夹中，如图 14-9 所示。

既然常量的新家已经准备好并等待着，你们只需要添加目前需要的常量即可（列表 14-2 显示了你需要添加到 `Constants.h` 文件中的常量）。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_303_0.png)

![](img/d3e98c195a93c941d040bbbc53dc1bd8_303_1.png)

### 列表 14-2：向 Constants.h 文件添加内容

| #define | 值 |
|---|---|
| #define kSections | 2 |
| #define kSection1Rows | 4 |
| #define kSection2Rows | 3 |

拥有一个 `Constants.h` 文件很好，但你必须让 `RootViewController.m` 知道你打算使用它。要在 `RootViewController.m` 中包含 `Constants.h`，请在 Xcode 中打开 `ViewController.m` 并添加以下语句：

```
#import "Constants.h"
```

你可以在用于创建表格视图的所有各种方法中使用这些常量，如列表 14-3 所示。

### 列表 14-3：更好的节和行处理

```
(NSInteger)numberOfSectionsInTableView:(UITableView *) tableView {

return kSections;
}

(NSInteger)tableView:(UITableView *)tableView
numberOfRowsInSection:(NSInteger)section {

NSInteger rows;
switch (section) {
case 0:
rows = kSection1Rows;
break;
case 1:
rows = kSection2Rows;
break;
default:
break;
}
return rows;
}
```

当你构建并运行这个（临时的）应用程序时，你将看到图 14-10 所示的内容——两个节，第一个有四行，第二个有三行。

虽然使用常量和 `switch` 语句使你的程序更具扩展性，但如果你想添加或更改布局，确实需要你修改 `switch` 语句。更好的解决方案是在 `awakeFromNib` 中创建一个所示的数组。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_304_0.png)

```
sectionsArray = [[NSMutableArray alloc]
initWithCapacity:2];
[sectionsArray addObject:[[NSNumber alloc]
initWithInt:4]];
[sectionsArray addObject:[[NSNumber alloc]
initWithInt:3]];
```

然后，你就可以使用数组计数 `[sectionsArray count]` 来返回节的数量，并通过数组索引 `[sectionsArray objectAtIndexIndex:section]` 来获取每一节的行数。

## 为节添加标题

节已经设置好了，你现在需要为它们命名标题，以便用户知道这些节的用途。坦率地说，对你来说，`UITableViewDataSource` 协议有一个方便的方法——名不虚其实的 `tableView:titleForInSection:` 方法——它允许你为每个节添加标题。列表 14-4 显示了如何实现该方法。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_305_0.png)

图 14-10：现在有了节。

### 列表 14-4：tableView 添加节标题

```
(NSString*)tableView:(UIView*)tableView
titleForSection:(NSInteger)section {
    NSString *title = nil;
    switch (section) {
    case 0:
        title = @"Welcome to London";
        break;
    case 1:
        title = @"Getting there";
        break;
    default:
        break;
    }
    return title;
}
```

（再次）是一个简单的 `switch` 语句。对于 case 0，即第一个节，你希望标题是 "Welcome to London"，而对于 case 1，即第二个节，你希望标题是 "Getting there"。

好了，这个也很容易——所以你不会惊讶地发现它并不是处理整个标题业务的最佳方法。另一条不建议走的路径——实际上是一个非常重要的不要走的路径。严肃的应用程序开发者坚持满足日益增长的全球观众的需求，这意味着——矛盾的是——他们必须对应用程序进行本地化。换句话说，应用程序的创建必须能够向不同的本地受众展示不同的视图。下一节将解释如何这样做。

## 本地化

本地化应用程序并不困难，只是繁琐。为了本地化你的应用程序，需要在程序包中每个你想支持的语言创建一个文件夹。每个文件夹都有字符串文件。当本地化应用程序需要加载资源（例如图像或 nib）时，应用程序会检查用户的语言和区域，并查找与语言相对应的文件夹。

如你所见，该宏有两个输入。第一个是语言中的字符串，第二个是给翻译者的通用注释。在运行时，`NSLocalizedString` 会在设置的语言中查找名为 `localizable.strings` 的字符串文件：例如西班牙语（用户可以通过进入设置，选择通用 > 国际来设置）。如果 `NSLocalizedString` 找到了该字符串文件，它会在文件中搜索与第一个参数匹配的行。在这种情况下，它将返回“Cómo llamó”，并将其作为节标题显示。如果该宏没有找到文件或指定的字符串，它将返回它的第一个参数——该字符串将以基础语言显示。

要创建可本地化的字符串文件，你需要运行一个名为 `genstrings` 的命令行程序，它会搜索你代码中的标记并将它们全部放置在一个 `localizable.strings` 文件中（该文件由它创建），供（人类翻译者）使用。`genstrings` 超出了本书的讨论范围，但它有完善的文档。当你准备好后，我就留给你自己操作了。

好吧，在编写代码时做这类事情确实非常烦人（是的，我知道，真的很烦人）。但等到应用程序快要做完时再回去寻找并替换所有想要本地化的字符串，那比这要烦人得多。听我的没错！

### 列表 14-5：添加可本地化的节标题

```objc
(NSString *)tableView:(UIView*)tableView
             titleForHeaderInSection:(NSInteger)section {
NSString *title = nil;
switch (section) {
case 0:
    title = NSLocalizedString(@"Welcome to London",
                             @"City name");
    break;
case 1:
    title = NSLocalizedString(@"Getting there",
                             @"Airport choices");
    break;
default:
    break;
}
return title;
}
```
