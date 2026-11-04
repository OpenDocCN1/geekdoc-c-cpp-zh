
## 更改窗体标题

在 Windows 窗体应用程序中，窗体的默认标题设置为 Form1。不过，您可以在设计时以及运行时通过更改窗体的 Text 属性来更改窗体标题。

让我们创建一个 Windows 窗体应用程序 SampleApplication，在其中可以执行以下步骤更改 Form1 窗体的标题：

- 1. 单击“开始”→“所有程序”→“Microsoft Visual Studio 2010”→“Microsoft Visual Studio 2010”以打开 Visual Studio 2010 IDE。
- 2. 从 Visual Studio 2010 IDE 的菜单栏中选择“文件”→“新建”→“项目”。此时将打开“新建项目”对话框。
- 3. 在“新建项目”对话框的“已安装的模板”窗格中选择 Visual C#→Windows，并在中间窗格中选择“Windows 窗体应用程序”选项。
- 4. 在“名称”文本框中输入 SampleApplication，并在“位置”组合框中指定适当的位置。
- 5. 单击“确定”按钮。将使用指定的名称和位置创建 SampleApplication 应用程序。
- 6. 单击 Form1 窗体上的任意位置，然后按 F4 键打开其“属性”窗口。
- 7. 在“属性”窗口中，将 Form1 窗体的 Text 属性设置为 FirstForm（图C#5.1）。

更改 Form1 窗体的 Text 属性后，其标题将显示为图C#5.1所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_150_0.png)

图C#5.1

在图C#5.1中，Form1 窗体的标题已更改为 FirstForm。

### 注意

还可以在 Form1 的 Load 事件中输入以下代码片段来更改 Form1 的 Text 属性：
上述代码片段将 Form1 的标题更改为 FirstForm。

```csharp
this.Text = "FirstForm";
```

接下来，让我们学习如何显示和隐藏 Windows 窗体上的“最大化”、“最小化”和“关闭”按钮。

## 显示和隐藏“最大化”、“最小化”和“关闭”按钮

窗体包含某些按钮，例如“最小化”、“最大化”和“关闭”。这些按钮位于窗体的右上角，默认可见。如果需要，可以通过将 Form1 窗体的 ControlBox 属性设置为 False 来隐藏这些按钮。

在本书“更改窗体标题”一节中创建的 SampleApplication 应用程序中，执行以下步骤来隐藏“最大化”、“最小化”和“关闭”按钮：

- 1 在“属性”窗口中，将 FirstForm 窗体的 ControlBox 属性设置为 False，以隐藏 ControlBox，如图C#5.2所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_151_0.png)

图C#5.2

- 2 按 F5 键运行 SampleApplication 应用程序。输出如图C#5.3所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_151_1.png)

图C#5.3

在图C#5.3中，FirstForm 窗体中看不到“最小化”、“最大化”和“关闭”按钮。现在，让我们学习如何指定窗体的初始状态和位置。

## 指定窗体的初始状态和位置

窗体可以在显示器或投影仪屏幕上按以下模式显示：

- 最大化状态：占据屏幕的整个显示区域。
- 最小化状态：最小化显示在任务栏上。
- 正常状态：正常显示，其大小和位置与“属性”窗口中指定的大小和位置相同。这是窗体的默认状态。

可以通过设置窗体的 WindowState 属性来设置窗体的初始状态。窗体的初始状态是指窗体首次显示时所处的状态（最大化、最小化或正常）。在 SampleApplication 应用程序中执行以下步骤来最大化 Windows 窗体：

- 1 在“属性”窗口中，将 FirstForm 窗体的 WindowState 属性设置为 Maximized，如图C#5.4所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_152_0.png)

图C#5.4

在图C#5.4中，FirstForm 窗体的 WindowState 属性为 Maximized。

### 注意

> WindowState 属性的默认值为 Normal。

有时，您可能需要将窗体显示在特定位置。可以借助窗体的 StartPosition 属性使窗体出现在屏幕上的特定位置。Form1 窗体的 StartPosition 属性可采用表5.1中列出的不同值：

表5.1：StartPosition 属性的可能值

| 值 | 描述 |
|---|---|
| CenterParent | 使窗体在其父窗体的边界内居中 |
| CenterScreen | 按窗体 Size 属性指定的尺寸将窗体居中 |
| Manual | 使用窗体的 Location 和 Size 属性确定窗体的起始位置 |
| WindowsDefaultBounds | 将窗体定位到 Windows 界面的默认位置，并由 Windows 默认值确定边界 |
| WindowsDefaultLocation | 将窗体定位到 Windows 界面的默认位置，并使用窗体 Size 属性指定的尺寸 |

在 SampleApplication 应用程序中，在“属性”窗口中将 FirstForm 窗体的 StartPosition 属性设置为 CenterScreen，如图C#5.5所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_153_0.png)

图C#5.5

如图C#5.5所示，**SampleApplication** 应用程序的 **StartPosition** 属性已设置为 **CenterScreen**。

## 创建多窗体 Windows 窗体应用程序

在某些情况下，您可能希望向 Windows 窗体应用程序中添加多个窗体。多窗体 Windows 应用程序允许您向应用程序中添加一个或多个窗体，并在另一个窗体中使用某个窗体的数据。您可以向单个 Windows 窗体应用程序中添加多个窗体。

让我们执行以下步骤，向 **SampleApplication** 应用程序中添加另一个窗体：

- 1. 在“解决方案资源管理器”中右键单击 **SampleApplication** 应用程序，然后从上下文菜单中选择 **添加➔新建项**，如图C#5.6所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_153_1.png)

图C#5.6

此时将打开“添加新项”对话框（图C#5.7）。

- 2. 在“添加新项”对话框中选择 **Windows 窗体** 选项（图C#5.7）。
- 3. 在“名称”文本框中输入 **SecondForm.cs**（图C#5.7）。
- 4. 单击 **添加** 按钮，如图C#5.7所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_154_0.png)

**图C#5.7**

一个名为 **SecondForm** 的新窗体已添加到 **SampleApplication** 应用程序中，如图C#5.8所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_154_1.png)

**图C#5.8**

用同样的方法，您可以向应用程序中添加更多窗体。

## 在多窗体 Windows 窗体应用程序中设置启动窗体

每当打开多窗体 Windows 窗体应用程序时，**Form1** 窗体都会作为默认启动窗体出现；不过，您也可以将任何其他窗体设置为启动窗体。在 C# 中，可以在 **Program.cs** 文件中设置启动窗体。

在 **SampleApplication** 应用程序中执行以下步骤，将 **SecondForm** 设置为多窗体 Windows 窗体应用程序中的启动窗体：

- 1. 在“解决方案资源管理器”中 **双击** **Program.cs** 文件。代码编辑器将显示代码，如清单5.1所示：

**清单5.1：显示 Program.cs 文件的代码**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Windows.Forms;

namespace SampleApplication
{
    static class Program
    {
        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new Form1());
        }
    }
}
```

在清单5.1中，Main() 方法中的最后一行是用于启动窗体的指令。在本例中，启动窗体是 Form1。

将启动指令更改为 SecondForm 窗体，如以下代码片段所示：

```csharp
Application.Run(new SecondForm());
```

按 F5 键运行 SampleApplication 应用程序。输出如图C#5.9所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_155_0.png)

图C#5.9

在图C#5.9中，第二个窗体 SecondForm 首先出现。

## 使用 MessageBox.Show() 方法

在 C# 2010 中，.NET Framework 的 MessageBox.Show() 方法用于显示消息框。MessageBox.Show() 方法是一个重载方法，其语法如下：

```csharp
public static DialogResult Show(
    string text,
    string caption,
    MessageBoxButtons buttons,
    MessageBoxIcon icon,
    MessageBoxDefaultButton defaultButton,
    MessageBoxOptions options,
    string helpFilePath,
    HelpNavigator navigator,
    object param
)
```

MessageBox.Show() 方法的不同参数说明如下：

- **text:** 在消息框中显示文本。
- **caption:** 在消息框的标题栏中显示文本。
- **buttons:** 指定要在消息框中显示的按钮。它是 MessageBoxButton 枚举值之一。
- **icon:** 指定要在消息框中显示的图标。它是 MessageBoxIcon 枚举值之一。
- **defaultButton:** 指定消息框的默认按钮。它是 MessageBoxDefaultButton 枚举值之一。
- **options:** 指定用于消息框的显示和相关选项。它是 MessageBoxOptions 枚举值之一。
- **helpFilePath:** 表示当用户单击“帮助”按钮时要显示的帮助文件的路径和名称。
