
- `options` – 指定 `MessageBoxOptions` 枚举值，以确定消息框的显示和关联选项

- `helpfilePath` – 指定当用户单击帮助按钮时要显示的帮助文件的路径和名称

- `navigator` – 指定 `HelpNavigator` 值

- `param` – 当用户单击帮助按钮时，显示帮助主题的数字 ID

以下是 `MessageBoxButtons` 枚举的值：

- `AbortRetryIgnore` – 显示 Abort、Retry 和 Ignore 按钮

- `OK` – 显示 OK 按钮

- `OKCancel` – 显示 OK 和 Cancel 按钮

- `RetryCancel` – 显示 Retry 和 Cancel 按钮

- `YesNo` – 显示 Yes 和 No 按钮

- `YesNoCancel` – 显示 Yes、No 和 Cancel 按钮

以下是 `MessageBoxIcon` 枚举的值：

- `Asterisk` – 显示一个图标，显示圆圈中的小写字母 i

- `Error` – 显示一个图标，显示红色背景的圆圈中的白色 X

- `Exclamation` – 显示一个图标，显示黄色背景的三角形中的感叹号

- `Hand` — 显示一个图标，显示红色背景的圆圈中的白色 X

- `Information` — 显示一个图标，显示圆圈中的小写字母 i

- `None` — 不显示任何图标

- `Question` — 显示一个图标，显示圆圈中的问号

- `Stop` — 显示一个图标，显示红色背景的圆圈中的白色 X

- `Warning` — 显示一个图标，显示黄色背景的三角形中的感叹号

以下是 `MessageBoxDefaultButton` 枚举的值：

- `Button1` — 将消息框中的第一个按钮设为默认按钮

- `Button2` — 将消息框中的第二个按钮设为默认按钮

- `Button3` — 将消息框中的第三个按钮设为默认按钮

以下是 `MessageBoxOptions` 枚举的值：

- `DefaultDesktopOnly` — 在 Windows 的默认桌面上显示消息框

- `RightAlign` — 将消息框文本显示为右对齐。

- `RtlReading` — 指定消息框文本以从右到左的阅读顺序显示

- `ServiceNotification` — 当服务发出调用以通知用户事件时，在活动桌面上显示消息框

`Show` 方法的结果是 `DialogResult` 枚举的一个值。这些值是：`Abort`、`Cancel`、`Ignore`、`No`、`None`、`OK`、`Retry` 和 `Yes`。

让我们创建一个应用程序 `MessageBoxMethod`，以学习如何使用 `MessageBox.Show` 方法显示消息框。

执行以下步骤创建 `MessageBoxMethod` 应用程序：

1. 创建一个名为 `MessageBoxMethod` 的 Windows 窗体应用程序。
2. 将 `Form1` 的 `Text` 属性修改为 `Message Displaying Form`。
3. 向 `Form1` 添加一个 `Label`（`label1`）、`TextBox`（`textBox1`）和一个 `Button`（`button1`）。
4. 将 `label1` 的 `Text` 属性设置为 `Message Text:`（图 8.22）。
5. 将 `button1` 控件的 `Text` 属性设置为 `Click Me`。图 8.22 显示了 `MessageBoxMethod` 应用程序的设计视图：

![](img/e073a4882197be4ab61103cbe0bcb394_314_0.png)

图 8.22：显示 `MessageBoxMethod` 应用程序的设计视图

6. 在 `button1` 的 `Click` 事件中添加以下代码片段，使用 `MessageBox.Show` 方法显示消息框：

```
private void button1_Click(object sender, EventArgs e)
{
    string msg=textBox1.Text;
    int Result = 0;
    Result = ((int)MessageBox.Show("This is a message box!\nYour text is : "+msg,
    "Message Box",
    MessageBoxButtons.OKCancel, MessageBoxIcon.Information,
    MessageBoxDefaultButton.Button1, MessageBoxOptions.DefaultDesktopOnly));
    if (Result == (int)DialogResult.OK)
    {
        textBox1.Text = "You clicked OK";
    }
}
```

7. 按键盘上的 `F5` 键调试并执行应用程序。
8. 在 `Message Text:` 文本框中输入文本，如图 8.23 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_315_0.png)

图 8.23：显示带按钮控件的窗体

9. 单击 `Click Me` 按钮，会出现一个消息框，如图 8.24 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_315_1.png)

图 8.24：显示消息框

现在，当您在消息框中单击 `OK` 按钮时，`You clicked OK` 文本会出现在 `Form1` 的 `Message Text:` 文本框中，如图 8.25 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_315_2.png)

图 8.25：显示文本框控件中的文本

你可以在 CD 上的 `MessageBoxMethod` 应用程序中找到使用 `MessageBox.Show` 方法显示消息框的代码。

让我们现在学习如何创建对话框。

## 使用 Windows Forms 创建对话框

在 GUI 环境中，对话框是一种窗口类型，可在计算机与其用户之间实现通信。它可用于向用户传达信息，或提示用户做出响应，或同时实现这两个目的。最简单的形式是出现一个显示消息的对话框，可能需要确认已阅读该消息。警报还可能要求通过单击 `OK` 或 `Cancel` 按钮来决定是否应继续执行操作。

在本节中，你将学习执行以下任务：

- 创建对话框
- 从对话框读取数据
- 在对话框中创建 Accept 和 Cancel 按钮

让我们详细讨论这些内容。

### 创建对话框

在本节中，我们创建一个名为 `DialogBoxControl` 的应用程序，以展示如何创建对话框。你可以在 CD 上找到 `DialogBoxControl` 应用程序的源代码。

执行以下步骤创建 `DialogBoxControl` 应用程序：

- 1. 创建一个名为 `DialogBoxControl` 的 Windows Forms 应用程序。
- 2. 在 `Form1` 中添加一个 `Label`（`label1`）、`TextBox`（`textBox1`）和两个 `Buttons`（`button1` 和 `button2`）控件。
- 3. 修改表 8.6 中给出的控件属性：

表 8.6：控件的修改属性

| Control | Property Name | Property Value |
|---|---|---|
| `Form1` | `Text` | `My Dialog Box` |
| `Form1` | `FormBorderStyle` | `FixedDialog` |
| `Form1` | `ControlBox` | `False` |
| `Form1` | `ShowInTaskbar` | `False` |
| `label1` | `Text` | `Enter Your Text` |
| `textBox1` | `Modifiers` | `Internal` |
| `button1` | `Text` | `OK` |
| `button1` | `DialogResult` | `OK` |
| `button2` | `Text` | `Cancel` |
| `button2` | `DialogResult` | `Cancel` |

`DialogResult` 属性的可能设置在表 8.7 中显示：

表 8.7：`DialogResult` 枚举

| Member name | Description |
|---|---|
| `None` | Does not return anything |
| `OK` | Shows the return value OK |
| `Cancel` | Shows the return value Cancel |

### 表 8.7：`DialogResult` 枚举

| Member name | Description |
|---|---|
| `Abort` | Shows the return value Abort |
| `Retry` | Shows the return value Retry |
| `Ignore` | Shows the return value Ignore |
| `Yes` | Shows the return value Yes |
| `No` | Shows the return value No |

图 8.26 显示了修改属性后 `Form1` 及其控件：

![](img/e073a4882197be4ab61103cbe0bcb394_317_0.png)

图 8.26：显示 `Form1` 及其控件

现在，如果你运行应用程序，创建的对话框看起来像一个简单的 Windows 窗体，如图 8.27 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_317_1.png)

图 8.27：以窗体形式显示对话框

### 从对话框检索数据

在本节中，我们继续使用 `DialogBoxControl` 应用程序来展示如何从对话框检索数据。让我们执行以下步骤从对话框检索数据并在窗体上显示：

- 1. 向 `DialogBoxControl` 应用程序添加一个窗体 `Form2.cs`。
- 2. 向 `Form2` 添加 `Label`（`label1`）和 `Button`（`button1`）控件。
- 3. 修改表 8.8 中给出的控件属性：

### 表 8.8：控件的修改属性

| Control | Property Name | Property Value |
|---|---|---|
| `Form2` | `Text` | `Dialog Box Form` |
| `textBox1` | `Modifiers` | `Internal` |
| `button1` | `Text` | `Click Me` |

图 8.28 显示了 `Form2` 及其控件和修改后的属性：

![](img/e073a4882197be4ab61103cbe0bcb394_318_0.png)

图 8.28：显示 `Form2` 上的控件

- 4. 在 `Form2` 的 `button1` 的 `Click` 事件中添加以下代码片段：

```
public void button1_Click(object sender, EventArgs e)
{
    Form1 frm = new Form1();
    if (frm.ShowDialog() == DialogResult.OK)
    {
        textBox1.Text = frm.textBox1.Text;
    }
}
```

在前面的代码片段中，`Form1` 的 `textBox1` 控件的文本将显示在 `Form2` 的 `textBox1` 控件中。

现在，让我们创建 `OK` 和 `Cancel` 按钮，以便用户可以根据要执行的应用程序的要求接受或取消操作。

### 创建 Accept 和 Cancel 按钮

你可以通过使用 `Form1` 的 `AcceptButton` 和 `CancelButton` 属性轻松地在 `DialogBoxControl` 应用程序中创建 `OK` 和 `Cancel` 按钮。让我们继续使用 `DialogBoxControl` 应用程序并执行以下步骤在其中创建 Accept 和 Cancel 按钮：

- 1. 在 `Form1` 的 `Form1_Load` 事件中添加以下代码片段

```
private void Form1_Load(object sender, EventArgs e)
{
    AcceptButton = button1;
    CancelButton = button2;
}
```

- 2. 用以下代码片段替换 `Program.cs` 文件中 `Main` 方法的代码：

```
static void Main()
{
Application.EnableVisualStyles();
Application.SetCompatibleTextRenderingDefault(false);
Application.Run(new Form2());
}
```

3. 按 `F5` 键运行应用程序。输出如下图所示 8.29：

![](img/e073a4882197be4ab61103cbe0bcb394_319_0.png)

图 8.29：显示 `DialogBoxControl` 应用程序的输出

如果单击 `Click Me` 按钮，对话框 `My Dialog Box` 将打开，如图 8.30 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_319_1.png)

图 8.30：显示对话框

现在，在 `Enter Your Text` 文本框中输入文本并单击 `OK` 按钮（图 8.30）。对话框消失，你的文本出现在 `Form2` 的文本框中，如图 8.31 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_319_2.png)

图 8.31：从创建的对话框检索文本

TIP

始终建议在对话框中添加 `Cancel` 按钮，这样如果用户错误地打开了对话框，用户就可以在没有任何不良后果的情况下关闭它。

让我们现在学习下一节中如何创建 owned forms。

## 创建 Owned Windows Forms

Owned form 与拥有它的窗体绑定。当你最小化所有者窗体时，被拥有的窗体也会被最小化。你可以通过使用 `AddOwnedForm` 方法将 owned form 添加到 owner form 的应用程序中，并通过使用 `RemoveOwnedForm` 方法将其删除。让我们创建一个名为 `WinOwnedForm` 的应用程序，以学习如何创建 owned Windows Form。

执行以下步骤创建 owned form：

- 1. 创建一个 Windows Forms 应用程序 `WinOwnedForm`。
- 2. 向 `Form1` 添加一个按钮控件 `button1`
- 3. 修改 `Form1` 的 `Text` 属性为 `Owner Form`，`button1` 为 `Display Owned Form`，如图 8.32 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_320_0.png)

- 4. 向 `WinOwnedForm` 应用程序添加另一个 Windows Form，称为 `Form2`。
- 5. 向 `Form2` 添加一个 `Label` 控件 `label1`。
- 6. 修改 `Form2` 的 `Text` 属性为 `Owned Form`，`label1` 的 `Modifiers` 属性为 `Internal`，如图 8.33 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_320_1.png)

7. 在 `Form1` 的 `button1` 的 `Click` 事件中添加以下代码片段：

```
private void button1_Click(object sender, EventArgs e)
{
    Form2 OwnedForm1 = new Form2();
    this.AddOwnedForm(OwnedForm1);
    OwnedForm1.label1.Text = "This is an Owned form";
    OwnedForm1.Show();
}
```

8. 按 `F5` 键运行应用程序。输出如下图所示 8.34：

![](img/e073a4882197be4ab61103cbe0bcb394_321_0.png)

图 8.34：显示 `WinOwnedForm` 应用程序的输出

现在，当你单击 `Display Owned Form` 按钮时，会显示另一个窗体，其中包含一个标签，文本为 `This is an Owned form`，如图 8.35 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_321_1.png)

图 8.35：显示 Owned Form

你可以在 CD 上找到 `WinOwnedForm` 应用程序的源代码。

## 创建始终置顶的 Windows Forms

你可以通过将窗体的 `TopMost` 属性设置为 `true` 来设置窗体在应用程序中的其他窗体之上显示。

让我们创建一个应用程序 `AlwaysOnTopForms` 来查看 `TopMost` 属性的使用。

执行以下步骤使用窗体的 `TopMost` 属性：

- 1. 创建一个名为 `AlwaysOnTopForms` 的 Windows Forms 应用程序。
- 2. 在 `AlwaysOnTopForms` 应用程序中添加一个 Windows Form `Form2.cs`。
3. 将 `Form2` 的 `TopMost` 属性设置为 `False`，将 `Form1` 的 `TopMost` 属性设置为 `True`。图 8.36 显示了修改后的 `TopMost` 属性：

![](img/e073a4882197be4ab61103cbe0bcb394_322_0.png)

图 8.36：修改 `Form1` 的 `TopMost` 属性

4. 向 `Form1` 添加一个 `Button` 控件 `button1`，并将其 `Text` 属性设置为“点击我加载 `Form2`”。
