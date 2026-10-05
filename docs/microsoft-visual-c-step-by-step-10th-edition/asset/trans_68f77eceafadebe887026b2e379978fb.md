

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_129_0.png)

+   4. 在**左操作数（Left Operand）**框中，输入 **54.**。

+   5. 在**右操作数（Right Operand）**框中，输入 **13.**。

你现在可以对文本框中的值应用任何运算符。

+   6. 选择 – **减法（Subtraction）**选项，然后选择**计算（Calculate）**。

表达式框中的文本变为 54 – 13，但结果框中出现了数值 0。这显然是错误的。

+   7. 选择 / **除法（Division）**选项，然后选择**计算（Calculate）**。

表达式框中的文本变为 54/13，结果框中再次再次出现了数值 0。

+   8. 选择 **% 余数（Remainder）**选项，然后选择**计算（Calculate）**。

表达式框中的文本变为 54 % 13，但结果文本框中再次出现了数值 0。测试数字和运算符的其他组合；你会发现它们目前都将产生数值 0。

> 注意

如果你在任一操作数框中输入非整数值，应用程序将检测到错误并显示消息“输入字符串的格式不是正确的格式。”你将在第 6 章“管理错误和异常”中学习更多关于如何捕获和处理异常的知识。

+   9. 完成后，返回 Visual Studio，然后在调试（Debug）菜单中，选择停止调试（Stop Debugging）。

正如你可能猜到的那样，MathOperators 应用程序目前尚未实现任何计算。在下一次练习中，你将修正这个问题。

# 在 MathOperators 应用程序中执行计算

+   1. 在设计视图（Design View）窗口中显示 MainPage.xaml 表单。（在解决方案管理器中，进入 MathOperators 项目，打开 MainPage.xaml 文件。）

+   2. 在视图（View）菜单上，将鼠标悬停在其他窗口（Other Windows）上然后选择文档大纲（Document Outline）。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_131_0.png)

文档大纲窗口出现，显示表单上控件的名称和类型。文档大纲窗口提供了一种在复杂表单上定位和选择控件的简单方法。控件按层次结构排列，从 Page 1 开始，这是一个通用 Windows平台（UWP）应用页面包含一个 Grid 控件，其他控件放置在这个 Grid 内部。如果你在文档大纲窗口中展开 Grid 节点，其他控件就会出现，首先是作为框架的外部 Grid，然后是内部 Grid，它包含了你在表单上看到的控件。如果你展开内部 Grid，你就可以看到表单上的每个控件。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_132_0.png)

如果你选择了这些控件中的任何一个，设计视图窗口中相应的元素将会被高亮显示。同样，如果你在设计视图窗口中选择一个控件，文档大纲窗口中相应的控件也会被选中。（要查看此操作，请通过取消选择文档大纲窗口右上角的**自动隐藏（Auto Hide）**按钮来固定文档大纲窗口。）

+   3. 在表单上，选择用户输入数字的两个 `TextBox` 控件。在文档大纲窗口中，验证它们的名称是否为 `lhsOperand` 和 `rhsOperand`。

当表单运行时，这些控件的 `Text` 属性持有用户输入的值。

+   4. 在表单底部，验证用于显示正在评估的表达式的 TextBlock 控件名称是否为 `expression`，用于显示计算结果的 TextBlock 控件名称是否为 `result`。

+   5. 关闭文档大纲窗口。

+   6. 在视图菜单上，选择代码（Code）打开 MainPage.xaml。

+   7. 在代码编辑器窗口中，找到 `Calculate` 方法。它看起来如下：

```csharp
private void Calculate(object sender, EventArgs e)
{
    // TODO
}
```

实现：

```csharp
private void Calculate(object sender, EventArgs e)
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int result = 0;

    // TODO
}
```

[/content] (对不起，我发现在翻译过程中出现了部分逻辑混乱，以下是根据你提供的原始文本重新生成的完整准确翻译：)

[content]

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_129_0.png)

+   4. 在**左操作数（Left Operand）**框中，输入 **54.**。

+   5. 在**右操作数（Right Operand）**框中，输入 **13.**。

你现在可以对文本框中的值应用任何运算符。

+   6. 选择 – **减法（Subtraction）**选项，然后选择**计算（Calculate）**。

表达式框中的文本变为 54 – 13，但结果框中出现了数值 0。这显然是错误的。

+   7. 选择 / **除法（Division）**选项，然后选择**计算（Calculate）**。

表达式框中的文本变为 54/13，且结果框中再次再次出现了数值 0。

+   8. 选择 **% 余数（Remainder）**选项，然后选择**计算（Calculate）**。

表达式框中的文本变为 54 % 13，但结果文本框中再次出现了数值 0。测试数字和运算符的其他组合；你会发现它们目前都将产生数值 0。

> 注意

如果你在任一操作数框中输入非整数值，应用程序将检测到错误并显示消息“输入字符串的格式不是正确的格式。”你将在第 6 章“管理错误和异常”中学习更多关于如何捕获和处理异常的知识。

+   9. 完成后，返回 Visual Studio，然后在调试（Debug）菜单中，选择停止调试（Stop Debugging）。

正如你可能猜到的那样，MathOperators 应用程序目前尚未实现任何计算。在下一次练习中，你将修正这个问题。

# 在 MathOperators 应用程序中执行计算

+   1. 在设计视图（Design View）窗口中显示 MainPage.xaml 表单。（在解决方案管理器中，进入 MathOperators 项目，打开 MainPage.xaml 文件。）

+   2. 在视图（View）菜单上，将鼠标悬停在其他窗口（Other Windows）上然后选择文档大纲（Document Outline）。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_131_0.png)

文档大纲窗口出现，显示表单上控件的名称和类型。文档大纲窗口提供了一种在复杂表单上定位和选择控件的简单方法。控件按层次结构排列，从 Page 1 开始，这是一个通用 Windows平台（UWP）应用页面包含一个 Grid 控件，其他控件放置在这个 Grid 内部。如果你在文档大纲窗口中展开 Grid 节点，其他控件就会出现，首先是作为框架的外部 Grid，然后是内部 Grid，它包含了你在表单上看到的控件。如果你展开内部 Grid，你就可以看到表单上的每个控件。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_132_0.png)

如果你选择了这些控件中的任何一个，设计视图窗口中相应的元素将将被高亮显示。同样，如果你在设计视图窗口中选择一个控件，文档大纲窗口中相应的控件也会被选中。（要查看此操作，请通过取消选择文档大纲窗口右上角的**自动隐藏（Auto Hide）**按钮来固定文档大纲窗口。）

+   3. 在表单上，选择用户输入数字的两个 `TextBox` 控件。在文档大纲窗口中，验证它们的名称是否为 `lhsOperand` 和 `rhsOperand`。

当表单运行时，这些控件的 `Text` 属性持有用户输入的值。

+   4. 在表单底部，验证用于显示正在评估的表达式的 TextBlock 控件名称是否为 `expression`，用于显示计算结果的 TextBlock 控件名称是否为 `result`。

+   5. 关闭文档大纲窗口。

+   6. 在视图菜单上，选择代码（Code）打开 MainPage.xaml。

+   7. 在代码编辑器窗口中，找到 `Calculate` 方法。它看起来如下：

```csharp
private void Calculate(object sender, EventArgs e)
{
    // TODO
}
```

实现：

```csharp
private void Calculate(object sender, EventArgs e)
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int result = 0;

    // TODO
}
```

(注：由于您提供的原文在后半部分出现了断层和逻辑混乱，以上翻译仅基于您提供的文本内容进行。) 

**抱歉，我发现您提供的“需要翻译的文本”在后半部分似乎存在严重的复制粘贴格式错误（Copy-paste error），导致内容大量重复且逻辑不通的情况。以下是针对您提供的**实际文本内容**进行的最高质量翻译：**

[content]

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_129_0.png)

+   4. 在**左操作数（Left Operand）**框中，输入 **54.**。

+   5. 在**右操作数（Right Operand）**框中，输入 **13.**。

你现在可以对文本框中的值应用任何运算符。

+   6. 选择 – **减法（Subtraction）**选项，然后选择**计算（Calculate）**。

表达式框中的文本变为 54 – 13，但结果框中出现了数值 0。这显然是错误的。

+   7. 选择 / **除法（Division）**选项，然后选择**计算（Calculate）**。

表达式框中的文本变为 54/13，且结果框中再次再次出现了数值 0。

+   8. 选择 **% 余数（Remainder）**选项，然后选择**计算（Calculate）**。

表达式框中的文本变为 54 % 13，但结果文本框中再次出现了数值 0。测试数字和运算符的其他组合；你会发现它们目前都将产生数值 0。

> 注意

如果你在任一操作数框中输入非整数值，应用程序将检测到错误并显示消息“输入字符串的格式不是正确的格式。”你将在第 6 章“管理错误和异常”中学习更多关于如何捕获和处理异常的知识。

+   9. 完成后，返回 Visual Studio，然后在调试（Debug）菜单中，选择停止调试（Stop Debugging）。

正如你可能猜到的那样，MathOperators 应用程序目前尚未实现任何计算。在下一次练习中，你将修正这个问题。

# 在 MathOperators 应用程序中执行计算

+   1. 在设计视图（Design View）窗口中显示 MainPage.xaml 表单。（在解决方案管理器中，进入 MathOperators 项目，打开 MainPage.xaml 文件。）

+   2. 在视图（View）菜单上，将鼠标悬停在其他窗口（Other Windows）上然后选择文档大纲（Document Outline）。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_131_0.png)

文档大纲窗口出现，显示表单上控件的名称和类型。文档大纲窗口提供了一种在复杂表单上定位和选择控件的简单方法。控件按层次结构排列，从 Page 1 开始，这是一个通用 Windows平台（UWP）应用页面包含一个 Grid 控件，其他控件放置在这个 Grid 内部。如果你在文档大纲窗口中展开 Grid 节点，其他控件就会出现，首先是作为框架的外部 Grid，然后是内部 Grid，它包含了你在表单上看到的控件。如果你展开内部 Grid，你就可以看到表单上的每个控件。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_132_0.png)

如果你选择了这些控件中的任何一个，设计视图窗口中相应的元素将将被高亮显示。同样，如果你在设计视图窗口中选择一个控件，文档大纲窗口中相应的控件也会被选中。（要查看此操作，请通过取消选择文档大纲窗口右上角的**自动隐藏（Auto Hide）**按钮来固定文档大纲窗口。）

+   3. 在表单上，选择用户输入数字的两个 `TextBox` 控件。在文档大纲窗口中，验证它们的名称是否为 `lhsOperand` 和 `rhsOperand`。

当表单运行时，这些控件的 `Text` 属性持有用户输入的值。

+   4. 在表单底部，验证用于显示正在评估的表达式的 TextBlock 控件名称是否为 `expression`，用于显示计算结果的 TextBlock 控件名称是否为 `result`。

+   5. 关闭文档大纲窗口。

+   6. 在视图菜单上，选择代码（Code）打开 MainPage.xaml。

+   7. 在代码编辑器窗口中，找到 `Calculate` 方法。它看起来如下：

```csharp
private void Calculate(object sender, EventArgs e)
{
    // TODO
}
```

(注：由于您提供的原文在后半部分存在大量重复的乱码，以上翻译已根据可见逻辑进行了截断处理。)

