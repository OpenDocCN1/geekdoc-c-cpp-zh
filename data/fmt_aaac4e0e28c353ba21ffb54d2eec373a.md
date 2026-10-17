
| 代码 | Visual C# 项目 | 一个空白的 Windows Forms | | |

| 数据 | 接口 | Visual C# 项目 | 新建项窗口 | |

| 通用 | Windows Form | | Windows Forms | |

| Web | 用户控件 | Visual C# 项目 | 表单名称 | |

| Windows Forms | 组件类 | Visual C# 项目 | 添加按钮 | |

| WPF | 用户控件 (WPF) | | | |

| AspNetCore | 关于框 | Visual C# 项目 | | | |

| 图形 | ADO.NET 数据... | | | |

| 在线 | 应用程序配置 | | | |

| 名称： | BelleAireForm.cs | | | |

**图 12-36** 新建项窗口

- 4. 点击“添加”按钮。项目中将添加一个新表单，其“名称”（Name）和“文本”（Text，标题栏）属性包含 `BelleAireForm`。保存项目（并定期继续保存）。

- 5. 将表单的“背景”（`BackColor`）属性更改为黄色以匹配 `BaileysForm` 的颜色。

- 6. 在表单上拖入一个标签。将标签的“名称”（Name）更改为 `belleAireDescriptionLabel`。将标签的“文本”（Text）属性更改为包含：BelleAire 套房有两个卧室、两个浴室和一个私人阳台。点击文本属性上的箭头分两行输入此长消息。在表单上再次拖入一个标签，命名为 `belleAirePriceLabel`，并将价格作为“文本”（Text）属性输入：**每晚 199 美元**。调整标签的布局。

# 使用其他控件（继续）

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_609_0.png)

**图 12-37** BelleAire 套房

- 7. 在设计器选项卡中，双击 BelleAire 复选框。将方法重命名为大写字母开头，你可以在方法中编写任何代码语句。例如，假设已将一个名为 `helloLabel` 的标签拖到表单上。如果选择蓝色（Blue）菜单选项会导致标签变为蓝色，你可以这样编写该方法：

```cpp
private void BlueToolStripMenuItem_Click(object sender, EventArgs e) {
    helloLabel.ForeColor = Color.Blue;
}
```

- 4. 点击添加按钮。项目中将添加一个新表单，其“名称”（Name）和“文本”（Text，标题栏）属性包含 `BelleAireForm`。保存项目（并定期继续保存）。

- 5. 将表单的“背景”（`BackColor`）属性更改为黄色以匹配 `BaileysForm` 的颜色。

- 6. 在表单上拖入一个标签。将标签的“名称”（Name）更改为 `belleAireDescriptionLabel`。将标签的“文本”（Text）属性更改为包含：BelleAire 套房有两个卧室、两个浴室和一个私人阳台。点击文本属性上的箭头分两行输入此长消息。在表单上再次拖入一个标签，命名为 `belleAirePriceLabel`，并将价格作为“文本”（Text）属性输入：**每晚 199 美元**。调整标签的布局。

```cpp
private void BelleAireCheckbox_CheckedChanged(object sender, EventArgs e) {
    if (belleAireCheckbox.Checked) {
        BelleAireForm belleAireForm = new BelleAireForm();
        belleAireForm.ShowDialog();
    }
}
```

- 8. 保存项目，然后通过选择菜单栏上的“调试”来运行它。当你选择 BelleAire 复选框时，会出现 BedBreakfast 表单。

- 9. 在 IDE 中调整你认为可以改进控件的大小、位置或字体，然后测试程序。

- 10. 为了让它显示未选中状态，在 if 块中添加以下语句：

```cpp
belleAireCheckbox.Checked = false;
```

- 11. 点击菜单栏上的“项目”，然后点击“新建项”。点击 Windows Form，然后输入其名称：`LincolnForm`。点击“添加”按钮，当新表单出现时，其“名称”和“文本”属性将已设置为 `LincolnForm`。将“文本”属性更改为 Lincoln Room。然后在表单上添加两个标签，并为它们提供适当的“名称”属性。将第一个标签的“文本”更改为：在这个带有私人浴室的迷人房间回到 1850 年。第二个应为：每晚 110 美元。将表单的“背景”（Back）属性更改为白色。参见图 12-38。

- 12. 从工具箱将一个文本框（`TextBox`）拖到表单上。选择它的“图像”（Image）属性，并点击省略号。对话框允许你选择资源。点击“本地资源”（Local resource），然后点击“导入”按钮浏览图像。下载的学生文件的 Chapter.12 中找到 `AbeLincoln` 文件并双击它。（或者，你也可以导入你喜欢的其他图像。）图像出现在“选择资源”对话框中后，点击确定。选中的图像出现在图片后，将“大小模式”（`SizeMode`）属性更改为“缩放”（Zoom）。调整表单的大小以及标签和图片框的大小和位置，使图片完全可见且在表单上看起来很美观。参见图 12-39。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_611_0.png)

**图 12-39** 带有图片框的 LincolnForm

# 第 12 章 使用控件

（续）

`AbeLincoln` 文件获取自 www.clipartkid.com。你可以访问该网站并下载其他图像在在你自己的应用程序中使用。你还应该在网络上搜索“free clip art”（免费剪画）等短语。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_612_0.png)

- 13. 在解决方案（`Solution Explorer`）中，双击 `Form1.cs`，或者点击设计界面顶部的 `Form1.cs[Design]`。在 BedAndBreakfast 窗单上，双击 Lincoln Room 复选框（Checkbox），并将默认名称重命名为大写字母开头。然后将以下语句添加到 `LincolnCheckBoxCheckedChanged()` 方法中：

```sharp
private void LincolnCheckBoxCheckedChanged(object sender, EventArgs e)
{
    if (LincolnCheckBox.Checked)
    {
        LincolnForm = new LincolnForm();
        LincolnForm.ShowDialog();
        LincolnCheckBox.Checked = false;
    }
}
```

- 14. 保存项目并执行。当 BedAndBreakfast 窗体出现时，点击任意一个复选框——会出现相应的信息窗体。关闭然后点击另一个复选框。再次出现相应的窗体。

- 15. 关闭所有窗体。

## 向窗体添加单选按钮（RadioButtons）

接下来，你向 BedAndBreakfast 窗体添加更多控件。当用户必须从互斥选项中进行选择时，通常使用单选按钮。

- 1. 在 BedAndBreakfast 项目的窗体设计视图中，在窗体底部添加一个按钮（Button）。将按钮的 Name 属性更改为 `mealButton`，并将按钮的 Text 更改为 Click for meal options。调整按钮的大小，使其文本完全可见。

- 2. 从菜单栏选择 Project（项目）、Add New Item（添加新项），并点击 Windows Form。将窗体命名为 `BreakfastOptionForm`，并点击 Add（添加）。在新创建的窗体上，进行以下更改：

    - 将窗体的 `BackColor`（背景颜色）设置为黄色。

    - 向窗体上拖入一个 Label（标签）。为它适当命名，并将其 Text 设置为 Select your breakfast option。

    - 向窗体上拖入三个 RadioButtons。将它们各自的 Text 属性设置为 **Continental, Full, and Deluxe**。将它们的 Name 分别设置为 `contRadioButton`、`fullRadioButton` 和 `deluxeRadioButton`。

    - 为 Label 和 RadioButtons 选择一种合适的字体。

    - 向窗体上拖入一个 Label，然后将其设置为 **Price:**，并将其 Name 设置为 **priceLabel**。将字体属性设置得比其他窗体组件大一点，并将其设置为 **Bold（加粗）**。

参见图 12-40 以了解所有这些控件的大致位置。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_613_0.png)

**图 12-40** 开发 BreakfastOptionForm

- 3. 双击 BreakfastOptionForm 的标题栏，以生成一个名为 `BreakfastOptionForm_Load()` 的方法。在此方法中，你可以编写在每次创建窗体时都会执行的语句。在 BreakfastOptionForm 类中添加以下语句，声明三个代表不同早餐选项价格的常量。在 `BreakfastOptionForm_Load()` 方法中，设置在窗体加载时默认将 `priceLabel` 的 Text 属性设置为最低价格。

```csharp
public partial class BreakfastOption : Form {
    private const double CONT_BREAKFAST_PRICE = 6.00;
    private const double FULL_BREAKFAST_PRICE = 9.95;
    private const double DELUXE_BREAKFAST_PRICE = 16.50;

    public BreakfastOptionForm()
    {
        InitializeComponent();
    }

    private void BreakfastOptionForm_Load(object sender,
        EventArgs e)
    {
        priceLabel.Text = "Price: " +
        CONT_BREAKFAST_PRICE.ToString("C");
    }
}
```

- 4. 返回 BreakfastOptionForm 的设计视图，双击 contraButton。当你看到生成的 CheckedChanged() 方法时，将其重命名为大写字母开头，并添加一条语句，当用户选择该选项时将 priceLabel 设置为连续式早餐价格：

```sharp
private void ContRadioButton_CheckedChanged(object sender, EventArgs e)
{
    priceLabel.Text = "Price: " +
    CONT_BREAKFAST_PRICE.ToString("C");
}
```

- 5. 返回 BreakfastOptionForm 的设计视图，双击 fullRadioButton，重命名生成的方法，并添加一条语句，当用户选择该选项时将 priceLabel 设置为全早餐价格：

```csharp
private void FullRadioButton_CheckedChanged(object sender, EventArgs e)
{
    priceLabel.Text = "Price: " +
    FULL_BREAKFAST_PRICE.ToString("C");
}
```

- 6. 返回 BreakfastOptionForm 的设计视图，双击 deluxeRadioButton，重命名生成的方法，并添加一条语句，当用户选择该选项时将 priceLabel 设置为豪华式早餐价格：

```csharp
private void DeluxeRadioButton_CheckedChanged(object sender, EventArgs e)
{
    priceLabel.Text = "Price: " +
    DELUXE_BREAKFAST_PRICE.ToString("C");
}
```

- 7. 在解决方案（`Solution Explorer`）中，双击 `Form1.cs`，或者点击设计界面顶部的 `Form1.cs[Design]`。在 BedAndBreakfast 窗体上，双击 Lincoln Room 复选框，并将默认名称重命名为大写字母开头。然后将以下语句添加到 `LincolnCheckBoxCheckedChanged()` 方法中：

```sharp
private void MealButton_Click(object sender, EventArgs e)
{
    BreakfastOptionForm breakfastForm = new BreakfastOptionForm();
    breakfastForm.ShowDialog();
}
```

- 8. 保存项目并执行。当 BedAndBreakfast 窗体出现时，点击任意一个复选框——会出现相应的信息窗体。关闭然后点击另一个复选框。再次出现相应的窗体。

- 9. 关闭所有窗体。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_615_0.png)

**图 12-41** 选中了 Continental 单选按钮的 BreakfastOptionForm

# 核心术语

图形控制元素，或者更简单地称为“控件”，是用户与 GUI 程序交互的组件。

小部件（Widgets）是 GUI 控件。

链接标签（Link label）是一种带有文本的控件，可以将用户链接到其他资源如网页或文件。

控件（Control）的默认事件是在 IDE 中设计控件时双击该控件时生成的事件，它是你使用该控件时最可能修改的方法，也是用户在运行应用程序中遇到该控件时最期望生成的事件。

复选框（Check box）是用户可以点击或取消选择某个选项的 GUI。

单选按钮（Radio button）是一组中的选项，其中一次只能选择一个——选择任何单选按钮都会自动取消其他按钮。

访问键（Access key）提供了使用键盘进行选择的快捷方式。

图片框（Picture box）是一个可以显示图形的 GUI 元素。

列表框（List box）是一个显示用户可以通过点击选择的项目列表 GUI 元素。

组合框（Combo box）是列表框和编辑控件的组合 GUI 元素，允许用户从列表中选择或输入新文本。

对齐线（Snap lines）出现在设计环境中，帮助你将新控件与已有的其他控件对齐。

分组框（Group box）是一个包含其他 GUI 元素的 GUI 元素；它类似于没有滚动条且可以包含标题的面板。

面板（Panel）是一个包含其他 GUI 元素的 GUI 元素；它类似于没有标题但可以包含滚动条的分组框。

菜单条（Menu strip）是出现在表单（Form）或窗口标题栏下的通用选项水平列表。

模态窗口（Modal window）是一个从主窗口接管控制权的次级窗口，用户在继续操作之前必须处理它。

## 复习题

+ 1. 标签、按钮和复选框都是

   a. GUI 对象

   c. 小部件

   b. 控件

   d. 以上所有

# 第 12 章 使用控件

+ 2. 所有的控件对象都继承自 ____________________。

a. Form c. ButtonBase

b. Component

d. 以上所有

+ 3. 下列哪项与单选按钮（RadioButton）最相似？

a. ListControl c. 图片框

b. CheckedListBox

d. 按钮

+ 4. 下列哪项项不是常用的控件属性？

a. BackColor c. 语言 (Language)

b. Location

d. Size

+ 5. 你经常用于为另一个控件对象提供描述性文本的控件是 ________________。

a. 标签 (Label) c. 复选框 (CheckBox)

b. 表单 (Form)

d. 消息框 (MessageBox)

+ 6. 下列哪项创建了 firstLabel？

a. firstLabel = new firstLabel();

b. Label = new firstLabel();

c. firstLabel = new Label();

d. firstLabel = Label();

+ 7. 决定用户在 Label 上阅读内容的属性是 ________________。

a. 设置 (Setting) c. 短语 (Phrase)

b. Label

d. Text

+ 8. 下列哪项正确地创建了字体（Font）？

a. FontMyFont = new Font("Arial", 14F, FontStyle.Bold);

b. FontMyFont = new Font("Courier", 13.6);

c. myFont = Font Font new Font("TimesRoman", FontStyle.Italic);

d. Font MyFont = Font(20, "Helvetica", Underlined);

+ 9. 控件的默认事件是 ________________。

a. 当用户操作控件时自动发生或不发生

b. 在 IDE 中设计控件时双击该控件时生成的

c. 不需要参数

d. 当用户用鼠标点击控件时发生
