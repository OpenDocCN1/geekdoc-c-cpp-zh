

## 练习

- 1. [WPF, SimpleEdit] 使用你在第6课练习10中构建的WPF程序，重复“试一试”部分的操作。提示：要删除当前选中内容，请使用语句 `contentRichTextBox.Selection.Text = "";`。

- 2. [SimpleEdit] 复制你在“试一试”中构建的程序，并添加简单代码来处理“文件”菜单的“新建”、“打开”、“保存”和“退出”命令。对于“新建”命令，只需清空RichTextBox。（提示：使用Clear方法。）

  对于“打开”和“保存”命令，只需加载和保存文件Test.rtf。（程序会在你第一次保存时创建该文件。如果你在文件存在之前尝试打开它，程序会崩溃，所以在使用“保存”之前不要使用“打开”。）第8课将解释如何使用文件打开和保存对话框，让用户选择应打开或保存的文件。

- 3. [WPF, SimpleEdit] 使用你在练习1中构建的程序重复练习2。提示：
  - 一种清除控件内容的方法是使用以下代码：

    ```
    contentRichTextBox.SelectAll();
    contentRichTextBox.Selection.Text = "";
    ```

  - 上述代码可以正常工作，但如果控件包含大量文本，速度会相当慢。以下代码更复杂，但效率更高：

    ```
    TextRange range = new TextRange(
        contentRichTextBox.Document.ContentStart,
        contentRichTextBox.Document.ContentEnd);
    range.Text = "";
    ```

  - 要加载已保存的文件，请使用以下代码（抱歉，WPF版本的RichTextBox有点复杂）：

    ```
    TextRange range = new TextRange(
        contentRichTextBox.Document.ContentStart,
        contentRichTextBox.Document.ContentEnd);
    using (System.IO.Stream stream =
        new System.IO.FileStream("Test.rtf", System.IO.FileMode.Open))
    {
        range.Load(stream, DataFormats.Rtf);
    }
    ```

  - 要将文本保存到文件中，请使用以下代码：

    ```
    TextRange range = new TextRange(
        contentRichTextBox.Document.ContentStart,
        contentRichTextBox.Document.ContentEnd);
    using (System.IO.Stream stream =
        new System.IO.FileStream("Test.rtf", System.IO.FileMode.Create))
    {
        range.Save(stream, DataFormats.Rtf);
    }
    ```

- 4. [SimpleEdit] 复制你在练习2中构建的SimpleEdit程序，并添加代码来处理“格式”菜单的命令（“字体”命令和颜色命令除外，这些将在第8课中介绍）。

### 提示：

- 要打开或关闭项目符号，请使用语句 `contentRichTextBox.SelectionBullet = formatBulletMenuItem.Checked;`。

- 让缩进命令（无、悬挂、左、右和两端）重置所有其他缩进设置。例如，“悬挂”命令应将 `SelectionIndent` 和 `SelectionRightIndent` 属性设置为0，如以下代码所示：

  ```
  contentRichTextBox.SelectionIndent = 0;
  contentRichTextBox.SelectionRightIndent = 0;
  contentRichTextBox.SelectionHangingIndent = 20;
  ```

- 5. [WPF, SimpleEdit] 复制你在练习3中构建的WPF SimpleEdit程序，并添加代码来处理“格式”菜单的对齐和项目符号命令。提示：
  - 要打开或关闭项目符号，请使用语句 `EditingCommands.ToggleBullets.Execute(null, contentRichTextBox);`。
  - 对于对齐命令，请使用类似的 `EditingCommands` 方法。

- 6. [SimpleEdit] 复制你在练习4中构建的SimpleEdit程序，并添加代码来处理工具栏的颜色命令。

- 7. SimpleEdit程序只允许无、悬挂、左、右和两端这几种缩进样式。它不允许其他组合，例如“悬挂”加“右”。构建一个使用工具栏按钮的程序，让用户单独选择每种缩进属性（悬挂、左和右）。提供第四个按钮来清除所有缩进属性。

- 8. 制作一个包含两个菜单和一个RichTextBox的程序。“文件”菜单应包含常规的“退出”命令。“字体”菜单应包含“小”、“中”和“大”三个项目，并分别使用小、中、大字体。当用户选择其中一项时，程序应将RichTextBox中选定的文本设置为使用该项目的字体。

- 9. [困难] 制作一个包含RichTextBox和一个带有“撤销”和“重做”按钮的工具栏的程序。最初禁用这些按钮。每当用户更改RichTextBox的文本（捕获TextChanged事件）或单击其中一个按钮时，使用RichTextBox控件的CanUndo和CanRedo属性来启用或禁用这些按钮。验证当你单击按钮或按Ctrl+Z或Ctrl+Y时，程序是否按预期工作。还要确保按Ctrl+V粘贴到RichTextBox时也能正常工作。

> **注意** 请在 www.wrox.com/go/csharp24hourtrainer2videos 在线选择第7课的视频。

> **注意** 你可能还记得，在第1课中，我说过：“通常你不需要担心某个功能是由Visual Studio、C#语言还是.NET Framework提供的。”这里也是如此，但值得注意的是，这些对话框实际上是由.NET Framework提供的，而不是C#。这不会改变你使用它们的方式，但意味着它们是被所有.NET语言（如Visual Basic、Visual C++或JScript）使用的相同对话框。
>
> 通过将这些标准对话框构建到.NET Framework中，微软让使用多种语言的程序员能够共享相同的通用功能。

这些对话框会自动为你提供一些相当复杂的功能，无需额外代码。例如，OpenFileDialog类允许用户浏览文件系统以选择要打开的文件。该对话框可以自动验证文件是否确实存在，因此用户无法输入不存在的文件名并单击“打开”。

类似地，如果所选文件确实存在，SaveFileDialog类会自动提示用户。例如，如果用户选择了已存在的文件Test.txt，对话框会显示消息“Test.txt已存在。是否要替换它？”如果用户不单击“是”，对话框就不会关闭。当对话框关闭时，用户必须选择了尚不存在的文件，或者同意覆盖原文件。

在本课中，你将学习如何显示这些标准对话框。你将学习如何初始化它们以向用户显示程序的当前设置，如何判断用户单击了哪个按钮，以及如何使用用户所做的选择。

> **注意** 本课在打印对话框方面实际上有点取巧。虽然它解释了如何显示这些对话框，但在你知道如何打印之前，你无法用它们做任何真正有用的事情，而打印是一个更复杂的主题。第30课将详细介绍如何打印。

## 对话框的一般用法

你基本上可以用相同的方式使用所有标准对话框。唯一的区别在于如何初始化对话框，使其显示颜色、字体、文件等内容，以及如何处理结果。

你可以按照以下四个步骤在Windows Forms应用程序中使用标准对话框：

- 1. 将对话框添加到窗体。
- 2. 初始化对话框以显示当前设置。
- 3. 显示对话框并检查返回结果。
- 4. 处理结果。

### 将对话框添加到窗体

你可以像添加任何其他组件（如Timer）一样，将对话框添加到窗体中。与其他组件一样，对话框会出现在窗体下方的“组件托盘”中。

工具箱有一个“对话框”选项卡，其中包含大多数标准对话框，因此很容易找到。与打印相关的对话框包含在“打印”选项卡中，所以也很容易找到（如果你知道去那里找的话）。图8-1显示了工具箱的“打印”和“对话框”选项卡。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_156_0.png)

**图8-1**

### 初始化对话框

大多数标准对话框在启动时都有一些初始选择。FontDialog启动时会选中一种字体，ColorDialog启动时会选中一种颜色，依此类推。通常你应该初始化对话框，使其向用户显示程序的当前设置。例如，FontDialog应显示程序当前的字体。

通常进行这些初始选择很容易。只需将对话框的关键属性（Font、Color、FileName）设置为你想要显示的值即可。

例如，以下代码将ColorDialog的Color属性设置为窗体当前的BackColor值。（回想一下，这指的是当前正在执行代码的窗体或其他对象。）

```
backgroundColorDialog.Color = this.BackColor;
```

这里唯一的诀窍在于知道要设置哪些属性。表8-1列出了不同类型对话框的关键属性。

