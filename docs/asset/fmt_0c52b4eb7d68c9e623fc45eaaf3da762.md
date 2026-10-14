
`Window.Current.Activate();`

}
/// <summary>
/// Invoked when Navigation to a certain page fails
/// </summary>
/// <param name="sender">The Frame which failed navigation</param>
/// <param name="e">Details about the navigation failure</param>
void `OnNavigationFailed`(object `sender`, `NavigationFailedEventArgs` `e`)
{
    throw new Exception("Failed to load Page " + `e.SourcePageType.FullName`);
}
/// <summary>
/// Invoked when application execution is being suspended. Application state is saved
/// without knowing whether the application will be terminated or resumed with the
/// contents
/// of memory still intact.
/// </summary>
/// <param name="sender">The source of the suspend request.</param>
/// <param name="e">Details about the suspend request.</param>
private void `OnSuspending`(object `sender`, `SuspendingEventArgs` `e`)
{
    var `deferral` = `e.SuspendingOperation.GetDeferral`();
    //TODO: Save application state and stop any background activity
    `deferral.Complete`();
}
}

这段代码大部分由注释（以“//”开头的行）和其他你暂时无需理解的语句组成，但关键元素位于加粗高亮的 `OnLaunched` 方法中。该方法在应用程序启动时运行，其中的代码会使应用程序创建一个新的 `Frame` 对象，在该框架中显示 `MainPage` 表单，然后激活它。此时无需完全理解这段代码的工作原理或这些语句的语法，但了解应用程序启动时就是通过这种方式显示表单是有帮助的。

### 向图形应用程序添加代码

现在你对图形应用程序的结构有了一些了解，是时候编写一些代码让你的应用程序真正做点事情了。

### 编写 OK 按钮的代码

1. 在 Design View 窗口中，打开 `MainPage.xaml` 文件（在 Solution Explorer 中双击 `MainPage.xaml`）。
2. 仍在 Design View 窗口中，单击表单上的 OK 按钮以选中它。
3. 在 Properties 窗口中，单击所选元素的 Event Handlers 按钮。

此按钮显示一个类似闪电的图标，如下所示：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_65_0.png)

Event handlers for selected element

Properties 窗口会显示 Button 控件的事件名称列表。事件表示通常需要响应的重要操作，你可以编写自己的代码来执行此响应。

4. 在 Click 事件旁边的框中，输入 `okClick`，然后按 Enter。

`MainPage.xaml.cs` 文件会在 Code and Text Editor 窗口中出现，并且在 `MainPage` 类中添加了一个名为 `okClick` 的新方法。该方法如下所示：

```
private void okClick(object sender, RoutedEventArgs e)
{
}
```

暂时不要太担心此代码的语法——你将在第 3 章学习有关方法的所有内容。

5. 将以下加粗显示的 `using` 指令添加到文件顶部列表中（省略号 [...] 表示为简洁而省略的语句）：

```
using System;
...
using Windows.UI.Xaml.Navigation;
using Windows.UI.Popups;
```

6. 将以下加粗显示的代码添加到 `okClick` 方法中：

```
private void okClick(object sender, RoutedEventArgs e)
{
    MessageDialog msg = new MessageDialog("Hello " + userName.Text);
    msg.ShowAsync();
}
```

此代码将在用户单击 OK 按钮时运行。同样，不要太担心语法，只要确保按所示完全复制代码即可；你将在接下来的几章中了解这些语句的含义。需要理解的关键点是，第一条语句使用消息“Hello <YourName>”创建了一个 `MessageDialog` 对象，其中 `<YourName>` 是你在表单上的 `TextBox` 中输入的名称。第二条语句显示 `MessageDialog`，使其出现在屏幕上。`MessageDialog` 类在 `Windows.UI.Popups` 命名空间中定义，这就是你在步骤 5 中添加它的原因。

### Note

你可能会注意到 Visual Studio 2015 在你输入的最后一行代码下方添加了一条波浪绿线。如果你将鼠标悬停在此行代码上，Visual Studio 会显示一条警告，内容为“Because this call is not awaited, execution of the current method continues before the call is completed. Consider applying the ‘await’ operator to the result of the call.” 本质上，此警告意味着你没有充分利用 .NET Framework 提供的异步功能。你可以安全地忽略此警告。

7. 单击 Code and Text Editor 窗口上方的 `MainPage.xaml` 选项卡，以再次在 Design View 窗口中显示表单。
8. 在显示表单 XAML 描述的下部窗格中，检查 Button 元素，但要小心不要更改任何内容。注意它现在包含一个名为 Click 的属性，该属性引用 `okClick` 方法。

```
<Button x:Name="ok" ... Click="okClick" />
```

9. 在 Debug 菜单上，单击 Start Debugging。
10. 当表单出现时，在文本框中，输入你的姓名覆盖现有文本，然后单击 OK。

会出现一个消息对话框，显示以下问候语：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_67_0.png)

11. 在消息框中单击 Close。
12. 返回 Visual Studio 2015，然后在 Debug 菜单上单击 Stop Debugging。

### Summary

在本章中，你学习了如何使用 Visual Studio 2015 创建、构建和运行应用程序。你创建了一个在控制台窗口中显示输出的控制台应用程序，并创建了一个具有简单 GUI 的通用 Windows 平台应用程序。

- 如果你想继续下一章，请保持 Visual Studio 2015 运行并转到第 2 章。
- 如果你现在想退出 Visual Studio 2015，请在 File 菜单上单击 Exit。如果出现 Save 对话框，请单击 Yes 保存项目。

### Quick Reference

| To | Do this |
|---|---|
| Create a new console application using Visual Studio 2015 | On the File menu, point to New, and then click Project to open the New Project dialog box. In the left pane, expand Installed, expand Templates, and then click Visual C#. In the middle pane, click Console Application. In the Location box, specify a directory for the project files. Type a name for the project, and then click OK. |
| Create a new blank Universal Windows Platform app using Visual Studio 2015 | On the File menu, point to New, and then click Project to open the New Project dialog box. In the left pane, expand Installed, expand Templates, expand Visual C#, expand Windows, and then click Universal. In the middle pane, click Blank App (Windows Universal). In the Location box, specify a directory for the project files. Type a name for the project, and then click OK. |
| Build the application | On the Build menu, click Build Solution. |
| Run the application in Debug mode | On the Debug menu, click Start Debugging. |
| Run the application without debugging | On the Debug menu, click Start Without Debugging. |

## 第 2 章 使用变量、运算符和表达式

完成本章后，你将能够：

- 理解语句、标识符和关键字。
- 使用变量存储信息。
- 使用原始数据类型。
- 使用算术运算符，如加号 (`+`) 和减号 (`−`)。
- 增加和减少变量。

第 1 章“欢迎使用 C#”介绍了如何使用 Microsoft Visual Studio 2015 编程环境构建和运行控制台程序和图形应用程序。本章向你介绍 Microsoft Visual C# 语法和语义的元素，包括语句、关键字和标识符。你将学习 C# 语言内置的原始类型以及每种类型所保存的值的特征。你还将看到如何声明和使用局部变量（仅存在于方法或其他代码小段中的变量），了解 C# 提供的算术运算符，学习如何使用运算符操作值，并学习如何控制包含两个或多个运算符的表达式。

### 理解语句

语句是执行操作的命令，例如计算值并存储结果或向用户显示消息。你将语句组合起来创建方法。你将在第 3 章“编写方法和应用作用域”中更详细地了解方法，但现在，将方法视为命名好的语句序列。`Main` 在上一章中介绍过，是一个方法的例子。

C# 中的语句遵循一套定义良好的规则来描述其格式和构造。这些规则统称为语法。（相比之下，语句做什么的规范统称为语义。）最简单也是最重要的 C# 语法规则之一规定你必须用分号终止所有语句。例如，第 1 章演示了如果没有终止分号，以下语句将无法编译：

```
Console.WriteLine("Hello, World!");
```

### Tip

C# 是一种“自由格式”语言，这意味着空格字符或换行等空白在作为分隔符时才有意义。换句话说，你可以随意以任何风格布局你的语句。然而，你应采用简单一致的布局风格，以使你的程序更易于阅读和理解。

在任何语言中编程良好的诀窍是学习该语言的语法和语义，然后以自然且符合惯用法的方式使用该语言。这种方法使你的程序更易于维护。随着你阅读本书的进展，你将看到最重要的 C# 语句的示例。

### 使用标识符

标识符是你用来标识程序中元素的名称，例如命名空间、类、方法 和变量。（你将很快学习关于变量的内容。）在 C# 中，选择标识符时必须遵守以下语法规则：

- 你只能使用字母（大写和小写）、数字和下划线字符。
- 标识符必须以字母或下划线开头。

例如，`result`、`_score`、`footballTeam` 和 `plan9` 都是有效的标识符，而 `result%`、`footballTeam$` 和 `9plan` 则不是。

### Important

C# 是区分大小写的语言：`footballTeam` 和 `FootballTeam` 是两个不同的标识符。

### 识别关键字

C# 语言为其自身保留了 77 个标识符，你不能将这些标识符重复用于自己的目的。这些标识符称为关键字，每个都有特定的含义。关键字的例子有 `class`、`namespace` 和 `using`。你将在阅读本书的过程中学习大多数 C# 关键字的含义。以下是关键字的列表：

| abstract | do | in | protected | true |
| as | double | int | public | try |
| base | else | interface | readonly | typeof |
| bool | enum | internal | ref | uint |
| break | event | is | return | ulong |
| byte | explicit | lock | sbyte | unchecked |
| case | extern | long | sealed | unsafe |
| catch | false | namespace | short | ushort |
| char | finally | new | sizeof | using |
| checked | fixed | null | stackalloc | virtual |
| class | float | object | static | void |
| const | for | operator | string | volatile |
| continue | foreach | out | struct | while |
| decimal | goto | override | switch |  |
| default | if | params | this |  |
| delegate | implicit | private | throw |  |

![](img/16f6e3fe08f01ddadb2741a92c392b0e_71_0.png)

### Tip

在 Visual Studio 2015 代码和文本编辑器窗口中，输入关键字时它们会显示为蓝色。

C# 还使用以下标识符。这些标识符未被 C# 保留，这意味着你可以使用这些名称作为自己的方法、变量和类的标识符，但应尽可能避免这样做。

| add | get | remove |
| alias | global | select |
| ascending | group | set |
| async | into | value |
| await | join | var |
| descending | let | where |
| dynamic |orderby | yield |
| from | partial |  |

### 使用变量

变量是保存值的存储位置。你可以把变量想象成计算机内存中的一个盒子，存放临时信息。你必须为程序中的每个变量提供一个无歧义的名称，在其使用的上下文中唯一标识它。你使用变量的名称来引用它所保存的值。例如，如果你想存储商店中商品的成本值，你可能会创建一个简单地称为 `cost` 的变量，并将商品的成本存储在此变量中。稍后，如果你引用 `cost` 变量，检索到的值将是你之前存储在那里的商品成本。

### 命名变量

你应为变量采用命名约定，以帮助你避免对已定义的变量产生混淆。如果你的项目团队中有多名开发人员在应用程序的不同部分工作，这一点尤其重要；一致的命名约定有助于避免混淆并可减少错误发生的范围。以下列表包含一些通用建议：

- 不要以下划线开头标识符。虽然这在 C# 中是合法的，但它会限制你的代码与使用其他语言（如 Microsoft Visual Basic）构建的应用程序的互操作性。
- 不要创建仅按大小写不同的标识符。例如，不要同时创建名为 `myVariable` 的一个变量和名为 `MyVariable` 的另一个变量，因为很容易将两者混淆。此外，定义仅按大小写不同的标识符可能会限制在不区分大小写的语言（如 Visual Basic）中开发的应用程序中重用类的能力。
- 以小写字母开头名称。
- 在多词标识符中，以大写字母开头第二个及后续每个单词。（这称为 camelCase 记法。）
- 不要使用匈牙利命名法。（如果你是 Microsoft Visual C++ 开发人员，你可能熟悉匈牙利命名法。如果你不知道匈牙利命名法是什么，不用担心！）
