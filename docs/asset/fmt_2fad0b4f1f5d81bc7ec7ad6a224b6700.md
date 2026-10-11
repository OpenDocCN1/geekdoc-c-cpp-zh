
## 10. 假设你创建了一个名为 `myLabel` 的 `Label`。下列哪项将 `myLabel` 的背景颜色设置为绿色？

+ a. `myLabel = BackColor.System.Drawing.Color.Green;`

b. `myLabel.BackColor = System.Drawing.Color.Green;`

c. `myLabel.Green = System.DrawingColor;`

d. `myLabel.Background = new Color.Green;`

## 11. 复选框（`CheckBox`）和单选按钮（`RadioButton`）对象之间的区别之一是？

+ a. 单选按钮继承自 `ButtonBase`；复选框不继承。

b. 一次只能选择一个单选按钮。

c. 一个表单上只能出现一个复选框。

d. 单选按钮不能放置在分组框中；复选框可以。

## 12. 单选按钮的 `Checked` 属性可以持有值

+ a. `true` 和 `false`                c. `0` 和 `1`

b. `Checked` 和 `Unchecked`        d. `Yes`, `No` 和 `Undetermined`

## 13. 你可以显示位图或 JPEG 图像的控件是(n)

+ a. `DisplayModule`             c. `BitmapControl`

b. 图片框 (`PictureBox`)                   d. `ImageHolder`

## 14. `ListBox`, `ComboBox` 和 `CheckedListBox` 对象继承自哪个家族？

+ a. `ListControl`                 c. `ButtonBase`

b. `List`                                 d. `ListBase`

## 15. 下列哪些属性与 `ListBox` 相关但不与 `Button` 相关？

+ a. `BackColor`                  c. `Location`

b. `SelectedItem`                d. `IsSelected`

## 16. 通过 `ListBox`，你可以允许用户选择 ____________________。

+ a. 仅选择一个选项             c. 以上两者任其一

b. 多项选择         d. 以上均不是

## 17. 你可以使用 ________________  方法向 `ListBox` 添加项。

+ a. `AddList()`                    c. `List()`

b. `Append()`                     d. `Add()`

# 第 12 章 使用控件

## 18. 单选按钮（`RadioButton`）的 `Checked` 属性包含

a. 被选中项的位置

b. 被选中项的值

c. 一个指示项是否被选中的布尔值

d. 被选中项的数量

## 19. 当你创建一个 `ListBox` 时，它的 `SelectionMode` 是

a. `Simple`

b. `Multi`

c. `Drop`

d. `false`

## 20. 出现在表单（`Form`）或窗口标题栏下的通用选项水平列表是

a. 菜单条 (`menu strip`)

b. 标题栏 (`title bar`)

## 编程练习

+ 1. 创建名为 `DaySelector` 的项目。其 `Form` 包含两个 `ListBox`——一个包含至少四个名称，另一个包含至少四个尺寸。让每个列表的第一个项为默认值。

+ 2. 创建名为 `BreezyApartments` 的项目，包含一个用于租赁服务的 `Form`。允许用户选择卧室数量、浴室数量。在用户做出选择后，显示月租金，该租金是根据一间一室、二室或三室公寓每月每月 `$450`、`$550` 或 `$700` 的基础价格计算的。如果浴室大于一个，则在基础价格增加 `$75`。

+ 3. 创建名为 `VacationPlanner` 的项目，用于提供全包服务的的热带度假村。该项目包含一个 `Form`，允许用户在每个类别——出发城市、房型和餐食计划中至少选择一个选项。为每个选择分配不同的价格，并在用户点击按钮时显示总额。

+ 4. 创建名为 `CarDealer` 的项目，包含一个用于汽车经销商的 `Form`。包含至少三个车型的选项。用户做出选择后，跳转到一个包含所选机型信息的新 `Form`。

+ 5. 创建名为 `AnnualBudget` 的项目，包含一个带有 `LinkLabel` 的 `Form`。一个链接打开电子表格，其他链接访问你的网站。在 `Form` 上包含 `Label` 以解释每个链接。你可以创建一个包含几个年度预算数字的电子表格，也可以使用第 12 章中的 `AnnualBudget.xls` 文件。

+ 6. 创建名为 `TinasCustomTees` 的项目，包含一个生产 T 恤的公司 `Form`。允许用户从至少四种尺寸中选择（价格不同），并从至少三种颜色中选择。当用户选择尺寸时调整最终显示价格，并在选择不同尺寸时更改框架的背景颜色。此外，允许用户从日历（`MonthCalendar`）中选择订单日期并显示三天后的日期。

+ 7. 创建名为 `MenuStripDemo2` 的项目，基于第 12 章下载的学生文件中的 `MenuStrip` 项目。为当前已编程的菜单选项（字体菜单中的两个选项和颜色菜单中的三个选项）添加适当的功能。

## 第 12 章 使用控件

（...菜单）。为程序添加至少三个其他菜单选项，可以是垂直、水平排列或两者兼之。

- 12. 创建一个名为 `LetsADeal` 的项目。在这个游戏中，三个价值不同的奖品被随机分配，并隐藏在“门”后面，你可以通过按钮（`Buttons`）来实现这些。例如，奖品可能是一辆新车、一台大屏幕电视和一只活羊。玩家选择一个按钮，然后会显示另外两个奖品中的一个：即最想要的奖品。随后用户可以选择将原始选择更改为剩余的未显示选项。例如，考虑以下两种游戏场景：

    * 最值钱奖品被随机分配到第一个按钮。如果用户选择了第一个按钮，显示另外两个奖品中的一个，并询问用户是否想更改选择。

    * 最值钱奖品被分配到第一个按钮，但用户选择了第二个按钮。显示第三个奖品，使最值钱奖品的位置保持隐藏，并询问用户是否想更改选择。

在用户选择保留原始选择或进行更改后，显示他们赢得奖品。

## 调试练习

- 1. 在可下载的学生文件中，`Chapter.12` 文件夹中的每个项目都存在语法和逻辑错误。在开始修正错误之前，请立即保存这四个项目并重命名。在纠正错误后，使用带有 `Fixed` 前缀的相同名称保存每个项目。例如，`DebugTwelve1` 将变为 `FixedDebugTwelve1`。

    a. `DebugTwelve1`

    b. `DebugTwelve2`

    c. `DebugTwelve3`

    d. `DebugTwelve4`

## 案例分析

- 1. 在本书中，你为“格林维尔偶像秀”（`Greenville Idol`）比赛创建了程序。现在创建一个名为 `GreenvilleAdvertisement` 的交互式广告，用于招募参赛者。包含至少在本章中学习过的三个控件，并使用至少两种不同的字体（`Fonts`）和两种不同的颜色（`Colors`）。

- 2. 在本书中，你为“马歇尔壁画”（`Marshall's Murals`）创建了程序。现在创建一个名为 `MarshallsAdvertisement` 的交互式广告，用于宣传壁画。包含至少在本章中学习过的三个控件，并使用至少两种不同的字体（`Fonts`）和两种不同的颜色（`Colors`）。

# 第 13 章 事件处理

完成本章后，你将能够：

- 描述事件处理
- 描述委托（`delegates`）
- 声明并使用自定义及内置事件处理程序
- 处理控件组件事件
- 处理鼠标和键盘事件
- 管理多个控件
- 继续你对控件和事件的探索

在本书中，你已经学习了如何创建交互式 GUI 程序，用户可以操作各种控件。你已经处理了多个响应用户发起的事件（如鼠标点击）的控件，并为控件的默认事件提供了操作。在本章中，你将扩展对事件处理过程的理解。你将学习更多关于触发事件的对象以及捕获并响应该事件的对象。你还将学习委托（`delegates`）——即在从发送者向接收者传输消息时充当中介的对象。你将创建委托并管理交互式事件。你将学习如何为一个项目中的单个控件管理多个事件。

## 事件处理

在 C# 中，事件是对程序中发生的情况的反应；当对象发生某些有趣的事情时，事件就会发生。当你创建一个类时，你精确决定了什么被认为是“有趣的”。例如，当你创建一个表单（`Form`）时，你可能决定某些操作是有趣的。

事件是对程序中发生的情况的反应；当对象发生某些有趣的事情时，事件就会发生。当你创建一个类时，你精确决定了什么被认为是“有趣的”。例如，当你创建一个表单（`Form`）时，你可能决定某些操作是有趣的。

（注：由于原文后续部分存在大量重复的乱码描述，此处已根据核心技术逻辑完成翻译。）

在图 13-4 中，你可以看到 `e` 对象是一个 `MouseEventArgs` 对象。这是很合理的，因为用户使用鼠标点击了 `Button`。（如果用户使用的是触摸屏，用户也可以通过触摸 `Button` 来生成事件。）

当你在 IDE 中打开 `Designer.cs` 文件时，可以检查为创建图 13-4 中的 `Form` 而生成的应用程序所有代码。展开 Windows Form Designer 生成的代码，可以让你看到注释以及设置控件属性的语句。例如，图 13-5 中为 `changeButton` 生成的代码。你可以识别出如按钮的 `Location`、`Name` 和 `Size` 等特征已经被设置过了。

```c
// changeButton
this.changeButton.Location = new System.Drawing.Point(243, 92);
this.changeButton.Name = "changeButton";
this.changeButton.Size = new System.Drawing.Size(135, 23);
this.changeButton.TabIndex = 1;
this.changeButton.Text = "Change the label";
this.changeButton.UseVisualBackColor = true;
this.changeButton.Click += new System.EventHandler(this.changeButton_Click);
```

**图 13-5** 由 Visual Studio 生成的涉及 `changeButton` 的代码

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_627_0.png)

IDE 中设计模式下生成的代码不是为了通过输入来修改的。你应该通过 IDE 中的属性窗口修改控件属性，而不是在 `Designer.cs` 中直接输入。

图 13-5 中的所有代码都是由 Visual Studio 生成的。你已经类似于图 13-5 中的大部分语句，包括设置 `changeButton` 的 `Size`、`TabIndex` 和属性的语句。（记得每个语句的开头指向持有 `changeButton` 的 `Form`。）`changeButton` 代码中最不寻的语句在图 13-5 中被阴影标记。该语句涉及点击事件，即用户在程序执行期间点击按钮时的操作。阴影语句是必要的，因为 `changeButton` 不会自动“知道”将由哪个方法来处理它的事件——C# 和所有 .NET 允许你为 GUI 对象中生成的事件选择事件处理方法的名称。换句话说，`changeButton` 的事件处理不需要被命名为 `changeButton_Click()`。例如，你可以编写程序，使得当用户点击按钮时，事件处理命名为 `CalculatePayroll()`、`ChangeLabel()` 或任何其他标识符。然而，通常你并不想进行此类更改；为在 `changeButton` 点击时执行的方法命名为 `changeButton_Click()` 是最接近事实的方法。

将事件与其产生的操作连接起来被称为“事件接线”（event wiring）。`changeButton_Click()` 的事件接线是在图 13-5 中的阴影语句中完成的。该语句表明对于此程序，名为 `changeButton_Click()` 的方法是 `checkBox` 点击事件的接收器；当用户点击按钮并触发事件时，该方法就会执行。程序员说该语句创建了一个委托，或者更具体地说，了一个复合委托。委托的类型是 `EventHandler`，它接收指向 `ChangeButton_Click()` 方法的引用。你将在本章的接两个部分学习委托，还将学习为什么在语句中使用 `+=` 运算符。

> 两个真理和一个谎言
>
> 事件处理
>
> 1. 诸如按键或点击按钮的操作会触发事件。
> 2. 响应事件执行任务的方法是事件处理程序。
> 3. 生成事件的控件是事件接收器。
>
> 被察觉为错误的陈述是 #3。

## 理解委托

**委托**（`delegate`）是一个包含指向方法引用的对象；面向对象编程的程序员会说委托封装了一个方法。在政府中，委托是你授权代表你做选择的代表员。例如，各州会派代表参加总统提名提名大会。当代表到达时，他们可以根据当前情况自由做出最后时刻的选择。同样，C# 提供了一种方法，让程序采取在运行时未确定的替代方案。当你编写一个方法时，你并不总是知道运行时会发生哪些操作，因此你赋予了委托运行正确方法方法的权限。

> 在第 1 章中，你学习了封装是面向对象编程的基本特征。回想封装是将对象的属性和方法打包成一个统一的单元，并可以作为独立实体使用的技术。

在你实例化一个 C# 委托之后，你可以将其传递给一个方法，然后该方法会调用委托内部引用的方法。换句话说，委托提供了一种将方法引用作为参数传递给另一个方法的方法。虽然你不能直接将方法传递给方法，但你可以传递一个指向该方法的对象。例如，如果 `del` 是一个包含指向 `M1()` 方法引用的委托，你可以将 `del` 传递给名为 `MyMethod()` 的新方法。或者，你可以创建一个包含指向 `M2()` 方法引用的委托，并将此版本传递给 `MyMethod()`。当你编写 `MyMethod()` 时，你不需要知道它是调用 `M1()` 还是 `M2()`；你只需要知道它调用的是内部引用的任何方法即可。

```c
using static System.Console;
delegate void GreetHandler(string s);
class Greeting {
    public static void Hello(string s)
    {
        WriteLine("Hello, {0}", s);
    }
    public static void Goodbye(string s)
    {
        WriteLine("Goodbye, {0}", s);
    }
    static void Main()
    {
        GreetingHandler firstDel, secondDel;
        firstDel = new GreetHandler(Hello);
        secondDel = new GreetHandler(Goodbye);
        GreetMethod(firstDel, "Cathy");
        GreetMethod(secondDel, "Bob");
    }
    public static void GreetMethod(GreetingHandler gd,
        string name)
    {
        WriteLine("The greeting is:");
        gd(name);
    }
}
```

图 13-6 问候程序

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_630_0.png)

图 13-7 问候程序的输出

委托的用处在于方法引用可以传递给另一个方法，因此接收方法可以是自定义的。通过 C# 的许多其他特性（以及所有其他编程语言），你可以使用其他技术来实现相同的结果。例如，你可以乐意地使用其他技术产生如 `Hello, Cathy` 的简单输出。然而，你在这里学习关于委托的少量知识，因为你将在在本章稍后的部分看到，它们被用于 C# GUI 环境中响应事件的代码中。

## 创建组合委托

你可以使用 `=` 运算符将一个委托赋值给另一个。你还可以使用 `+` 和 `-=` 运算符将委托组合成组合委托，该委托会调用构建它的各个委托。例如，假设你有名为 `del11`、`del12` 和 `del13` 的委托，并将方法 `M1()` 的引用赋值给 `del11`，将方法 `M2()` 的引用赋值给 `del12`。当执行语句 `del13 = del11 + del12` 时，它变成了一个顺序执行 `M1()` 和 `M2()` 的委托。只有具有相同参数列表的委托才能组合，且委托必须具有 `void` 返回类型。此外，你可以使用 `-` 和 `-=` 运算符从组合委托中移除委托。组合委托是委托的集合，`+=` 和 `-=` 运算符用于从集合中添加和删除项。

图 13-8 显示了一个包含组合委托的程序。该程序与图 13-6 中的 Greet 程序相比有两个变化：类名（`Greeting2`）以及创建组合委托的阴影语句。委托 `firstDel` 现在执行两个方法：`Hello()` 和 `Goodbye()`，而 `secondDel` 仍然执行 `Goodbye()`。

图 13-9 显示了它的输出：Cathy 使用了两个方法，而 Bob 仅使用了一个。
