

## Locals 窗口

![](img/844f608d10a44654833ea5efc8a2e7a7_376_0.png)

### 如何使用 Locals 窗口

- Locals 窗口显示当前作用域内变量的信息。
- 要显示 Locals 窗口，请单击 Locals 选项卡或使用 Debug → Windows → Locals 命令。
- 如果你正在调试一个表单并单击 `this` 关键字左侧的 ▷ 符号，则会显示该表单的属性和变量。然后，如果你愿意，可以将鼠标悬停在属性上并单击属性名称右侧出现的图钉图标，将该属性固定在此组顶部。
- 要更改属性或变量的值，请在 Value 列中双击该值，然后输入新值并按 Enter 键。
- 在 Visual Studio 2019 及更高版本中，你可以在 Locals 窗口中搜索值和对象，并可以指定要搜索的深度层数。

### 如何使用 Autos 窗口

- Autos 窗口的工作方式与 Locals 窗口类似，但它只显示当前语句和前一条语句所使用的变量信息。
- 要显示 Autos 窗口，可以使用 Debug → Windows → Autos 命令。

**Figure 11-6** 如何使用 Locals 和 Autos 窗口来监视变量

## 如何使用 Watch 窗口来监视表达式

默认情况下，当应用程序进入断点模式时，Watch 窗口位于 Visual Studio 左下角的窗口组中，如图 11-7 所示。你可以使用这些窗口查看输入到这些窗口中的监视表达式的值。这些表达式会在应用程序执行时自动更新。

如果应用程序进入断点模式时 Watch 1 窗口不可用，你可以通过下拉 Debug 菜单，选择 Windows 子菜单，选择 Watch 子菜单，然后选择 Watch 1 项目来显示它。你也可以通过从此子菜单中选择相应项目来显示其他三个监视窗口中的任何一个。这些窗口提供与 Watch 1 窗口相同的功能。如果你想将监视表达式分组，可以使用它们。

要添加监视表达式，请在空行的 Name 列中单击并输入表达式。监视表达式可以是调试器识别的任何表达式。自 Visual Studio 2015 起，包括 lambda 表达式。你将在第 13 章中了解更多关于 lambda 表达式的内容。如果表达式存在于应用程序中，你也可以在代码编辑器中选择它并将其拖到 Watch 窗口中。此图中的 Watch 窗口显示了调试器识别的两个表达式：futureValue 变量和 Future Value 文本框的 Text 属性。

如果你将添加到 Watch 窗口的表达式是对象的名称，Watch 窗口将在名称左侧显示一个 ▷ 符号。然后，你可以单击此符号以显示对象属性。如果表达式是数组的名称，也会添加一个 ▷ 符号。然后，你可以单击此符号以显示数组中的元素。

你可以通过在 Value 列中双击值并输入新值来更改监视表达式的值。要删除监视表达式，可以使用在右键单击表达式时显示的快捷菜单上的 Delete Watch 命令。要删除所有监视表达式，可以使用快捷菜单上的 Select All 命令，然后使用 Delete Watch 命令。

### 一个 Watch 窗口

![](img/844f608d10a44654833ea5efc8a2e7a7_378_0.png)

### 描述

- Watch 窗口让你在应用程序处于断点模式时查看 *watch expressions* 的值。要显示 Watch 窗口，请单击其 Watch 选项卡。或选择 Debug > Windows > Watch 并选择 Watch 1、Watch 2、Watch 3 或 Watch 4。
- 要向 Watch 窗口添加表达式，请在 Name 列的空行上单击，然后输入表达式。你也可以在代码编辑器中突出显示一个表达式并将其拖入 Watch 窗口。
- 如果表达式超出作用域，它将在 Watch 窗口中变暗，并显示一条消息，说明该表达式在当前上下文中无效。
- 如果你在 Watch 窗口中输入对象或数组的名称，其名称旁边会出现一个树控件。然后，你可以使用此控件展开或折叠此条目。
- 要更改监视表达式的值，请在 Value 列中双击其值，输入新值，然后按 Enter 键。
- 要删除监视表达式，请右键单击该表达式并从快捷菜单中选择 Delete Watch 命令。要删除所有监视表达式，请右键单击 Watch 窗口，选择 Select All 命令，然后选择 Delete Watch 命令。
- 在 Visual Studio 2019 及更高版本中，你可以在 Watch 窗口中搜索值和对象，并可以指定要搜索的深度层数。

**Figure 11-7** 如何使用 Watch 窗口来监视表达式

## 如何使用 Immediate 窗口执行命令

另一个可用于调试的窗口是图 11-8 所示的 Immediate 窗口。默认情况下，此窗口显示在 Visual Studio 右下角的窗口组中。

你可以使用 Immediate 窗口显示变量或属性的值或执行代码。例如，你可以输入赋值语句来更改变量或属性的值。同样，你可以使用此窗口执行方法或显示方法返回的值。这对于使用不同参数测试方法的结果非常有用。在此过程中，你可以执行 .NET 类中的可用方法以及你在项目中编写的任何方法。

你在 Immediate 窗口中输入的命令在与正在运行的应用程序相同的范围内执行。这意味着你无法显示超出作用域的变量的值，也无法执行当前未执行的类中的私有方法。如果你尝试这样做，Visual Studio 会显示一个空白行或错误消息。

你还应该知道，你输入到 Immediate 窗口中的命令会一直保留在那里，直到你退出 Visual Studio 或使用窗口快捷菜单中的 Clear All 命令显式删除它们。这样，你就可以使用标准的 Windows 技术在一次应用程序执行到另一次执行之间编辑和重用相同的命令，而无需重新输入它们。与 Watch 窗口中的表达式不同，命令结果不会随着应用程序的执行而更新。

要执行已在 Immediate 窗口中输入的命令，请按向上或向下箭头键定位该命令。这会将命令显示在窗口底部。然后，如果你愿意，可以编辑该命令。或者，你可以按 Enter 执行该命令。

### Immediate 窗口

```
private decimal CalculateFutureValue(decimal monthlyInvestment, int months)
{
    decimal futureValue = 0m;
    for (int i = 0; i < months; i++)
    {
        futureValue = (futureValue + monthlyInvestment) * (1 + monthlyInterestRate);
    }
    return futureValue;
}
```

![](img/844f608d10a44654833ea5efc8a2e7a7_380_0.png)

```
? txtInterestRate.Text = "8"
? txtInterestRate.Text = "8"
```

### 描述

- 你可以使用 Immediate 窗口在执行期间显示和分配应用程序的值。要显示此窗口，请单击 Immediate Window 选项卡或使用 Debug→Windows→Immediate 命令。
- 要显示一个值，请输入一个问号后跟你想要显示其值的表达式。然后，按 Enter 键。
- 要为变量或属性分配不同的值，请输入赋值语句。然后，按 Enter 键。
- 要执行方法，请输入其名称和所需的任何参数。然后，按 Enter 键。如果你想显示方法的结果，请在方法调用前加上问号。
- 要重新发出命令，请使用向上或向下箭头键显示你想要的命令。然后，你可以编辑该命令或按 Enter 键执行它。
- 要从 Immediate 窗口中删除所有命令和输出，请使用窗口快捷菜单中的 Clear All 命令。
- 在 Visual Studio 2015 及更高版本中，你可以在 Immediate 窗口中输入 lambda 表达式。有关 lambda 表达式的更多信息，请参阅第 13 章。

