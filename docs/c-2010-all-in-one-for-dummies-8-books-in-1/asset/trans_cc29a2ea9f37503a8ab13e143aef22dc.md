

# 496 在设计器中设计

对于 Visual Studio 维护的每种主要项目类型都有一个相应的设计器。设计器处理“所见即所得”的体验部分，通常还处理幕后的标记代码。

问题在于，由于我们所处的软件开发世界的需要，所有设计师的工作方式略有不同。例如，HTML 和 XAML 之间存在显著差异，Web 设计师和 WPF 设计师的外和操作并不相同。

Visual Studio 提供了几个视觉设计器来帮助开发应用程序，包括：

- 类设计器 (Class Designer)
- 数据视图 (Data View)
- Windows Forms 
- Windows Presentation Foundation (WPF)

## Windows Presentation Foundation (WPF)

Windows Presentation Foundation 在第五书中会有较深入的介绍，但目前你应该知道，它是微软 Windows 开发体验的未来。第五本书详尽讨论了 WPF，因此你可以阅读更多关于它的信息。

用户界面设计的核心是一种称为 XAML 的语言，（令人惊讶的是）它是一种基于 XML 的领域特定标记语言，用于创建用户界面。在图 2-1 所示的设计器中，设计位于顶部框架，而底层代码位于底部框架。

你可以在设计器中点击设计内容并根据需要移动它们，或者使用设计器选择项目并在“属性”面板中编辑属性（我将在接下来的章节“工作区面板化”中介绍它）。此外，如果你在代码区域更改了某些内容，你将在设计中看到变化。这是一个非常好的系统。

WPF 设计器中有几个细小但重要的特征应该注意。你可以在图 2-1 中看到所有这些。

在左上角附近有一个缩放栏。你可以点击它的底部并选择“适应大小”（Zoom To Fit），或者移动滑块。这对于处理比屏幕更大的应用程序，或者为了微调视觉效果来说是无价的。

在设计框架和 XAML 框架之间分割线的左侧有一个小的双箭头图标。点击此图标会将底部框架中的任何内容切换到顶部框架，反之亦然。

# # 在设计器中设计 497

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_522_0.png)

**图 2-1：WPF 设计器。**

在同一条分割线的右侧有三个按钮，它们决定了分割的类型——垂直分割、水平分割（默认值）或不分割。

设计器本身还包含了一些点按式的调整工具。这里是其中一个：点击设计器窗口中表格的红色区域。将鼠标停在“146”尺寸标记出现的正上方。

看到出现的那个带有星号（*）、井号（#）和单词 *Auto* 单词的小方框了吗？那是你在 WPF 设计器中可以找到的许多辅助工具之一。井号（`#`）将列宽设置为一个数字（默认情况下即如此）。星号（`*`）将其设置为表格的百分比——对于调整大小非常有用。*Auto* 单词根据内容对列进行自动大小调整。

这些小功能只对设计器下方框架中的 XAML 进行更改。如果你在浮动表格设计器中点击 *Auto* 单词，你将更改这行代码：

```
<ColumnDefinition Width="146" />
```

将其变为 XAML 框架中的以下这行代码：

```
<ColumnDefinition Width="Auto" />
```

# 498 在设计器中设计

有些人喜欢代码。有些人喜欢设计器。有些人（喜欢）两者的奇妙结合。你决定如何使用这些工具。

## Windows Forms

Windows Forms 设计器与 WPF 设计器之间的主要区别是 Windows Forms 中缺少代码面板。虽然有（某种）代码支撑 Windows Forms 的运行，但你无法编辑它。就那样吧。

本书没有涵盖 Windows Forms 主题。尽管它仍然是一个活跃的开发平台，但我必须做出艰难的决定转而涵盖 WPF。它执行与 Windows Forms 相同的编程职责，但它是更新的技术。Windows Forms 设计器如图 2-2 所示。

事实上上，关于 Windows Forms 设计器本身没什么可说的。单个控件有一些很棒的设计器功能，但设计器本身并没有什么。

不过必须说明的是，我在这书中并没有对 Windows Forms 做什么。首先，这不是一本 Windows 编程书籍；它是一本 C# 书。其次，Windows Forms 正在逐渐淡出。WPF 是 Windows 编程的未来。Windows Forms 只是为了后兼容。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_523_0.png)

图 2-2：Windows Forms 设计器。

# 在设计器中设计 499

## Web Forms

Web 编程更像 WPF 编程而非 Windows Forms 编程，但它在 Web 服务器上运行并在浏览器中查看。（第六本书全是 Web Forms。）因为设计器具有后端代码元素，你可以看到分屏视图，如图 2-3 所示。

在 HTML 设计器中导航非常容易。我想特别指出 HTML 设计器的两个特征。这些特征可以在设计器底部菜单栏中找到：

- 视图切换按钮，显示 Source（源代码）、Design（设计）和 Split（拆分）：Source 只显示 HTML 代码。Design 只显示设计器。Split 令人惊讶的是同时包含两个面板，就像 WPF 设计器一样。

- 有趣的是，这两个框架并不保持同步。如果你更改了 HTML，设计框架会显示一条消息：“设计与源视图不同步。点击此处同步视图。”希望他们在发布到量产之前能修复这个问题。

- 用于查看视图切换按钮的小型文档树：它在分级树中显示，显示你的光标相对于文档其余部分的位置。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_524_0.png)
![](img/36596fb11aa4233d5cab0d6ddd1d82e8_524_1.png)

第四本书 第2章
使用界面

图 2-3 使用 Web 项目返回代码。

## 类设计器

你可以从任何项目创建类设计器，但我在下一个示例中使用了类库项目，如图 2-4 所示：

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_525_0.png)

图 2-4：数字格式的类。

类设计器为你提供了类的可视化界面。你可以轻松看到继承关系，而且成员是可见且可编辑的。这是我在图 2-4 中使用的类库：

```
namespace MyGarden
{
    public class Flower
    {
        public string Color;
    }
    public class Vegetable
    {
        public bool Yummy;
    }
    public class Daisy : Flower
    {
        public double Height;
    }
    public class Sunflower : Flower
    {
        public bool Harvested;
    }
    public class Tomato : Vegetable
    {
    }
    public double StakeHeight;
}
public class Carrot : Vegetable
{
    public double Depth;
}
}
```

要创建这样的类库，请遵循以下步骤：

1. 创建一个新的类库项目。
2. 将默认代码替换为你自己的代码。
3. 按 Shift + B 生成类库。
4. 右键点击项目并选择类图 (Class Diagram)。
   如果你需要，可以使用它。
   Visual Studio 会创建一个名为 ClassDiagram.cd 的新文件。这就是你的类图文件。
5. 保存项目。

你也可以向新类添加内容。点击 Flower 类的方法，在 name 下输入 Water，在 type 下输入 Public（作为修饰符）以添加 Water 方法。如果你切换回库视图，你会发现该类下增加了一个方法。

> 为了辅助项目文档，你可以在设计器窗的任何位置右键点击并选择“将此图导出为图像”，将其保存为 PNG 文件。我发现这在创建项目文档时非常有用。它比 Visio 有用得多，因为它与代码集成，包含在 Visual Studio 中，而且是免费！

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_526_0.png)

# 数据视图

数据视图通常与服务器管理器一起使用，它是 SQL 管理工具的一种数据表示的一部分。你可以在 Visual Studio 内部查看并编辑 SQL Server（以及其他）数据库管理系统的数据表。示例见 2-5。

这里有惊人的功能，空间无法涵盖所有内容。再次，这不是一本数据库书籍，所以我建议阅读有关 SQL 资源管理器数据连接功能的 MSD 条目以获取更多详细信息。

