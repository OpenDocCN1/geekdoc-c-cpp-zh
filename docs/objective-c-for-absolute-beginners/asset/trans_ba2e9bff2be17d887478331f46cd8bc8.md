

前面的代码将调用我们自定义的 setter（设置），而不是标准的 setter。如果我们写了自己的 getter（get），情况也是一样。现在，让我们继续开发商店（Bookstore）应用程序。

## 完成 MyBookstore 程序

在理解了实例变量和属性后，我们现在将开始创建真正的书店程序。想法非常简单：创建一个名为 `Bookstore` 的类，并在其中存放一些 `Book` 对象。

## 创建视图

让我们从准备好视图开始。如果你需要复习如何在 Xcode 中构建界面，请参考第 6 章。

- 1. 在导航窗口中点击 `DetailViewController.xib` 文件。这将显示 Xcode 的界面编辑器（interface builder），如图 8–8 所示。

![](img/322e107ddf8f5cd963a6efafdcd86f38_190_0.png)

图 8–8. 准备 MyBookstore 详情视图。

- 2. 直接删除现有的仅作为详情视图占位符的控件。我们将添加一些新字段来显示所选书籍的详情。由于我们删除了它，也需要删除引用它的代码。

- a. 在 `DetailViewController.h` 文件中，删除以下行：
  `@property (strong, nonatomic) UILabel *detailDescriptionLabel;`

- b. 在 `DetailViewController.m` 文件中，删除 cell 顶部附近的行：
  `@synthesize detailDescriptionLabel = _detailDescriptionLabel;`

- c. 在 `DetailViewController.m` 文件的 `configureView` 方法中，
  `self.detailDescriptionLabel.text = [self.detailitem description];`

- 3. 接下来，点击视图的实用工具（Utilities）图标，如图 8-9 所示。这将弹出可以放置在视图上的控件视图。

![](img/322e107ddf8f5cd963a6efafdcd86f38_191_0.png)

图 8-9. 选择工具窗口并添加一些 Label。

- 4. 从对象库（Object Library）将一些 `Label` 对象拖放到详情视图上，如图 8–9 所示。确保底部的 `Label` 控件设置为视图的宽度。这样它们就可以容纳较长的文本。两个显示为“Label”的 `Label` 对象将用于连接到 `Book` 对象的两个值：标题（Title）和作者（Author(s)）。## 添加实例变量

接下来，我们将为 `DetailViewController` 类添加一些实例变量。这些实例变量将对应详情视图的标签。

- 1. 首先，打开 `DetailViewController.h` 文件并删除 `detailDescriptionLabel` 属性——我们已经从接口中删除了它，不再需要它了。

- 2. 接下来，我们将添加两个代表详情视图上标签的字段，并将书籍数据存储在其中，如代码列表 8–14 所示。

**列表 8-14。** 修改 `DetailViewController.h` 文件以包含新的 Label。

```objc
#import <UIKit/UIKit.h>

@interface DetailViewController : UIView

@property (strong, atomic) id detailItem;

@property (strong, atomic) IBOutlet UILabel *titleLabel;
@property (strong, atomic) IBOutlet UILabel *authorLabel;

@end
```

- 3. 如果你还记得第 7 章的内容，属性中包含的 `IBOutlet` 标识符让这些实例变量（`titleLabel` 和 `authorLabel`）成为视图中的控件。接下来，右键点击“Title”下方的标签，并将一个“新引用输出”（New Referencing Outlet）拖到名为“File’s Owner”（文件所有者）的最顶部对象，如图 8–10 所示。

![](img/322e107ddf8f5cd963a6efafdcd86f38_193_0.png)

图 8–10. 为 Label 对象定义一个新的引用输出。

- 4. 拖动到 File's Owner 时，会弹出一个二级菜单，询问新输出应该连接到哪个变量。我们将把此 Label 连接到 `titleLabel` 输出，如图 8–11 和图 8–12 所示。

![](img/322e107ddf8f5cd963a6efafdcd86f38_193_1.png)

图 8-11. 选择 `titleLabel` 输出。

![](img/322e107ddf8f5cd963a6efafdcd86f38_193_2.png)

图 8-12. 连接完成。

- 5. 对“Author:”标签下方的 `Label` 对象重复此步骤，但将 Label 连接到 `authorLabel` 输出。## 添加描述

现在，我们需要向视图添加描述。描述与之前的略有不同，在于它可以跨多行显示。为了这一点，我们将使用 `Text View` 对象。

- 1. 开始在视图上添加一个“Description:”标签，如图 8–13 所示。

![](img/322e107ddf8f5cd963a6efafdcd86f38_194_0.png)

- 2. 接下来，在详情视图中添加 `Text View` 对象，如图 8–14 所示。文本视图的优势是易于显示多行文本。虽然 `Label` 也可以显示多行，但没有 `Text View` 对象那么整洁。

> 注意：默认情况下，Text View 控件填充了各种随机文本。这种文本被称为 Lorem Ipsum（填充文本）。如果你需要填充页面文本，可以在网上找到许多 Lorem Ipsum 生成器。至于我们的 Text View，文本可以保持原样，因为我们会在运行时将其移除。此外，如果清空了它，将很难发现 Text View 在屏幕上的具体位置——它是白底白字的！

![](img/322e107ddf8f5cd963a6efafdcd86f38_195_0.png)

图 8-14. 为详情添加 Text View。

- 3. 为了让程序利用 Text View，我们需要为它创建一个输出，就像我们为标题和描述创建的那样只需在 `DetailViewController.h` 文件中添加一个新属性，如列表 8–15 中的第 9 行所示。

列表 8-15。为 Text View 添加输出以持有描述。

```objc
1 #import <UIKit/UIKit.h>
2
3 @interface DetailViewController : UI
4
5 @property (strong, atomic) id detailItem;
6
7 @property (strong, atomic) IBOutlet UILabel *titleLabel;
8 @property (strong, atomic) IBOutlet UILabel *authorLabel;
9 @property (strong, atomic) IBOutlet UITextView *descriptionTextView;
10
11 @end
```

- 4. 注意类型是 `UITextView` 而不是 `UILabel`——这非常重要。此外，不要忘记在 `DetailViewController.m` 的 `@synthesize` 中添加 `descriptionTextView`。

```objc
@synthesize titleLabel, authorLabel, descriptionTextView;
```

