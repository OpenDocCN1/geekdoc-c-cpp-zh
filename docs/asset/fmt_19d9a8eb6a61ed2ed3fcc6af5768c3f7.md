
观看视频 Using MenuStrip。

## 两个真理一个谎言

在 Form 上添加 MenuStrip

- 1. 当你点击菜单条中的项时，最常见的结果是启动一个操作。
- 2. 当使用 Visual Studio IDE 将 `MenuStrip` 控件拖到 Form 上时，`MenuStrip` 将水平添加在 Form 的顶部，就在标题栏下方。
- 3. `MenuStrip` 的默认事件是 `Click()`。

## 使用其他控件

如果你查看 Visual Studio IDE 或搜索 Visual Studio 文档，你会发现许多本章未涵盖的控件。如果你点击菜单栏上的“项目”（Project）并点击“添加新项”（Add New Item），你就可以向项目添加额外的 Form、文件、控件和其他元素。（在接下来的“你来做”部分中，你将创建一个项目，该项目会在从主 Form 做出选择后添加新的 Form。）新的控件和容器将在未来开发，你甚至可能设计自己的新控件。尽管如此，所有控件都包含属性和方法，你在 C# 的坚实基础将让你能够有效地使用新控件。

## 你来做

### 在 Form 上添加 CheckBox

在接下来的步骤中，你向 BedAndBreakfast Form 添加两个 CheckBox。这些控件允许用户选择可用房间并查看其信息。

- 1. 如果屏幕上尚未打开 BedAndBreakfast 项目，请在 Visual Studio 中打开它。
- 2. 在 Visual Studio IDE 中 BedAndBreakfast 项目的设计视图中，将一个 CheckBox 拖到 `Check our rates` Label1 下方的 Form 上。（大致位置参见图 12-35。）将 CheckBox 的 `Text` 属性更改为 `BelleAir Suite`。将属性的 `Name` 改为 `belleAireCheckbox`。在第一个 CheckBox 下方拖入第二个 CheckBox。将其 `Text` 属性更改为 `Lincoln Room`，`Name` 改为 `linCheckbox`。

## 第12章 使用控件

![](img/b0a31988f44670d0728c4f372d8dab77_613_0.png)

**图 12-35** 带有两个 CheckBox 的 BedAndBreakfast Form

- 3. 接下来，你将创建两个新的 Form：用户选择 BelleAire CheckBox 时出现一个，用户选择 Lincoln CheckBox 时出现另一个。点击菜单栏上的**项目**，然后点击**添加新项**。在“添加新项”窗口中，点击**Windows Form**。在窗口底部的 Name 框中，输入 **BelleAireForm**。参见图 12-36。

## 使用其他控件（继续）

## 添加新项 - BedAndBreakfast

| | 排序依据：默认 | | | 类型：Visual C# 项目 |
|---|---|---|---|---|
| Visual C# 项目 | | | | Visual C# 项目 |
| Code | | | | 空的 Windows Form |
| Data | | Interface | | Visual C# 项目 |
| General | | | | 添加新项窗口 |
| Web | | Windows Form | | Visual C# 项目 |
| Windows Forms | | User Control | | 选择 Windows Form |
| XAML | | Component Class | | Visual C# 项目 |
| SQL Server | | | | Visual C# 项目 |
| Graphics | | User Control (WPF) | | Visual C# 项目 |
| Online | | Abstract Box | | Visual C# 项目 |
| | | ADO.NET Entity Data... | Visual C# 项目 |
| | | Application Manifest File | Visual C# 项目 |
| | | 点击此处联网查找模板 | | |

图 12-36 添加新项窗口

- 1. 点击**添加** 按钮。项目将添加一个新 Form，其 `Name` 和 `Text`（标题栏）属性包含 `BelleAireForm`。保存项目（并定期继续这样做）。
- 2. 将 Form 的 `BackColor` 属性更改为黄色，以匹配 Baileys's Form 的颜色。
- 3. 在 Form 上拖入一个 Label。将 Label 的 `Name` 改为 `belleAireDescriptionLabel`。将 Label 的 `Text` 属性更改为包含以下内容：**BelleAire 套房有两个卧室、两间浴室和一个私人阳台。** 点击文本属性上的箭头，分两行输入该长文本标签消息。调整 Label 的大小和位置，使其类似于图 12-37。在 Form 上拖入第二个 Label，将其命名为 `belleAireDescriptionLabel`。

（注：原文后续部分存在大量重复的 OCR 错误文本，已根据要求进行去重处理，仅保留逻辑流的翻译）

**图 12-37** 带有两个 CheckBox 的 BedAndBreakfast Form

![](img/b0a3 specifically_615_0.png)

# 使用控件（继续）

![](img/b0a31988f44670d0728c4f372d8dab77_618_0.png)

图 12-40 带有图片的 LincolnForm

Lincoln 文件获取自 www.free-graphics.com。你可以访问该网站并下载图像用于你自己的应用程序中。你还应该在网上搜索“free clip art”等短语。

- 13. 在解决方案管理器中，双击 `Form1.cs` 或点击 `Form1.cs` 顶部的设计[Design] 选项卡。在 BedAndBreakfast 表单上，双击 Lincoln Room 复选框，并在 `LincolnCheckBox_Checked_Changed()` 方法中添加以下 if 语句：

```csharp
private void LincolnCheckBox_CheckedChanged(object sender, EventArgs e)
{
    if (LincolnCheckBox.Checked)
    {
        LincolnForm LincolnForm = new LincolnForm();
        LincolnForm.ShowDialog();
        LincolnCheckBox.Checked = false;
    }
}
```

（继续）

- 14. 保存项目并执行它。当 BedAndBreakfast 表单出现时，点击复选框——会出现相应的信息表单。关闭它然后点击另一个复选框。再次出现相应的表单。
- 15. 关闭所有表单。

# 在表单中添加单选按钮

接下来你向 BedAndBreakfast 表单添加更多控件。当用户必须从互斥选项中选择时，通常使用单选按钮（RadioButtons）。

- 1. 在 BedAndBreakfast 项目的主表单视图中，在表单底部添加一个按钮。将按钮的 `Name` 属性更改为 `mealButton`，并将 `Text` 更改为 `Click options`。调整按钮的大小使其完全可见。
- 2. 从菜单栏选择 Project，点击 Add Item，然后点击 Windows Form。将表单命名为 BreakfastOptionForm 并点击 Add。在新表单上，进行以下更改：
    - 将表单的 `BackColor` 设置为黄色。
    - 拖一个 Label 到表单上。对其进行命名，并将其 `Text` 设置为 `Select breakfast option`。
    - 拖三个单选按钮到表单上。将它们的 `Text` 属性分别设置为 `Continental`、`Full` 和 `Deluxe`。将它们的 `Name` 分别设置为 `contBreakfastButton`、`fullBreakfastButton` 和 `deluxeBreakfastButton`。
    - 为 Label 和单选按钮选择合适的字体。
    - 拖一个 Label 到表单上，然后将其 `Text` 设置为 `Price:`并将 `Name` 设置为 `priceLabel`。将 `Font` 属性设置得比其他控件大一点。

查看图 12-41 获取这些控件的布局。

![](img/b0a31988f44670d0728c4f372d8dab77_620_png.png)

- 3. **双击** BreakfastOptionForm 的标题栏生成一个名为 `BreakfastOptionForm_Load()` 的方法。在此方法中，你可以编写每次创建表单时执行的语句。在 `BreakfastOptionForm` 类中添加以下语句，声明三个表示不同早餐选项的常量。在 `BreakfastOptionForm_Load()` 方法中，当表单加载时，将 `priceLabel` 的 `Text` 属性设置为默认价格。

```csharp
public partial class BreakfastOptionForm : Form
{
    private const double CONT_BREAKFAST_PRICE = 6.00;
    private const double FULL_BREAKFAST_PRICE = 9.95;
    private const double DELUXE_BREAKFAST_PRICE = 16.50;
    public BreakfastOptionForm()
    {
        InitializeComponent();
    }
    private void BreakfastOptionForm_Load(object sender, EventArgs e)
    {
        priceLabel.Text = "Price: " + CONT_BREAKFAST_PRICE.ToString("C");
    }
}
```

# 第 12 章 使用控件（继续）

- 4. 返回 BreakfastOptionForm 的设计视图，双击 `contBreakfastButton` 单选按钮。当你看到生成的 `Changed()` 方法时，添加一条语句，当用户选择该选项时将 `priceLabel` 设置为早餐价格：

```csharp
private void contBreakfastButton_CheckedChanged(object sender, EventArgs e)
{
    priceLabel.Text = "Price: " + CONT_BREAKFAST_PRICE.ToString("C");
}
```

- 5. 返回 BreakfastOptionForm 的设计视图，双击 `fullBreakfastButton` 单选按钮。添加一条语句，当用户选择该选项时将 `priceLabel` 设置为全餐价格：

```csharp
private void fullBreakfastButton_CheckedChanged(object sender, EventArgs e)
{
    priceLabel.Text = "Price: " + FULL_BREAKFAST_PRICE.ToString("C");
}
```

- 6. 返回 BreakfastOptionForm 的设计视图，双击 `deluxeBreakfastButton` 单选按钮。添加一条语句，当用户选择该选项时将 `priceLabel` 设置为豪华早餐价格：

```csharp
private void deluxeBreakfastButton_CheckedChanged(object sender, EventArgs e)
{
    priceLabel.Text = "Price: " + DELUXE_BREAKFAST_PRICE.ToString("C");
}
```

# 核心术语

- **图形控制元素**，或简单地称为**控件**（Controls），是用户与 GUI 程序交互的组件。
- **小部件**（Widgets）是 GUI 控件。
- **链接标签**（Link label）是一种带有文本的控件，该文本将用户链接到其他资源，例如网页或文件。
- **控件**（Control）的**默认事件**是在你在 IDE 中设计它时双击该控件时生成的事件，也是你使用该控件时最可能修改的方法，也是用户在运行应用程序中遇到该控件时最期望触发的事件。
- **复选框**（Check box）是一种 GUI 小部件，用户可以点击它来选择或取消某个选项。
- **单选按钮**（Radio button）是一组选项中的，一次只能选择其中一个——选择任何单选按钮都会自动取消其他按钮的选择。
- **访问键**（Access key）提供了一个使用键盘进行选择的快捷方式。
- **图片框**（Picture box）是一个可以显示图形的 GUI 元素。
- **列表框**（List box）是一个显示项目项列表的 GUI 元素，用户可以通过点击来选择项目。
- **组合框**（Combo box）是列表框和编辑控件的结合 GUI 元素，允许用户从列表中选择或输入新文本。
- **对齐线**（Snap lines）出现在设计环境中，帮助你将新控件与其他已有的控件对齐。
- **组框**（Group box）是一个包含其他 GUI 元素的 GUI 元素；它类似于面板（Panel），但没有滚动条并且可以包含标题。
- **面板**（Panel）是一个包含其他 GUI 元素的 GUI 元素；它类似于组框，但没有标题并且可以包含滚动条。
- **菜单条**（Menu strip）是出现在表单（Form）或窗口（Window）标题栏下的通用选项水平列表。
- **模态窗口**（Modal window）是一个次级窗口，它接管主窗口的控制权，用户在继续之前必须处理它。

## 复习习题

+ 1. 标签（Labels）、按钮（Buttons）和复选框（CheckBoxs）都是
   - a. 小部件 (widgets)
   - b. GUI 对象 (objects)
   - c. 控件 (controls)

# 第 12 章 使用控件

2. 所有 Control 对象都继承自 ____________________。
   - a. 表单 (Form)
   - b. 组件 (Component)
   - c. 按钮基类 (ButtonBase)
   - d. 以上皆是

3. 以下哪项最像单选按钮（RadioButton）？
   - a. 列表控件 (ListControl)
   - b. 已检查列表框 (CheckedListBox)
   - c. 图片框 (PictureBox)
   - d. 按钮 (Button)

4. 下面哪个不是常用的 Control 属性？
   - a. 背景颜色 (BackColor)
   - b. 语言 (Language)
   - c. 位置 (Location)
   - d. 大小 (Size)

5. 你经常用于为另一个对象提供描述文本的 Control 是 ____________________。
   - a. 表单 (Form)
   - b. 标签 (Label)
   - c. 复选框 (CheckBox)
   - d. 消息框 (MessageBox)

6. 下面哪个项创建名为 firstLabel 的 Label？
   - a. `firstLabel = new firstLabel();`
   - b. `Label = new firstLabel();`
   - c. `Label firstLabel = new Label();`
   - d. `Label firstLabel = Label();`

7. 决定用户在 Label 上阅读内容的属性是 ____________________ 属性。
   - a. (Text)
   - b. 标签 (Label)
   - c. 短语 (Phrase)
   - d. 设置 (Setting)

8. 下面哪项正确地创建了一个字体（Font）？
   - a. `Font myFont = new Font("Arial", 14F, FontStyle.Bold);`
   - b. `Font myFont = new Font("Courier", 13.6);`
   - c. `myFont = Font new Font("TimesRoman", FontStyle.Italic);`
   - d. `Font myFont = Font(20, "Helvetica", Underlined);`

9. Control 的默认事件是 ____________________。
   - a. 无论用户是否操作控件都会自动发生
   - b. 在 IDE 中设计它时双击控件时生成的
   - c. 不需要任何参数
   - d. 当用户用鼠标点击控件时发生

10. 假设你创建了一个名为 myLabel 的 Label。下面哪项将 myLabel 的背景颜色设置为绿色？
    - a. `myLabel = BackColor.System.Drawing.Color.Green;`
    - b. `myLabel.BackColor = System.Drawing.Color.Green;`
    - c. `myLabel.Green = System.Drawing.Color;`
    - d. `myLabel.Background = new Color.Green;`

11. CheckBox 和 RadioButton 对象之间的一个区别是？
    - a. RadioButtons 继承自 ButtonBase；CheckBox 不是。
    - b. 一次只能选择一个 RadioButton。
