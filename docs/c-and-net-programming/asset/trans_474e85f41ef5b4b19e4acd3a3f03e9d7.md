

![](img/3005a4307e6d8f3bb7e76eea28a92357_596_0.png)

- 从可用模板中选择 **Windows 窗体应用程序**。
- 将**名称**保留为默认的 **WindowsFormsApplication1**，或**根据应用程序任务输入**，然后单击“确定”。创建此新的 Windows 应用程序项目后。

![](img/3005a4307e6d8f3bb7e76eea28a92357_596_1.png)

- 主窗口中的空白窗体以默认名称 Form1 出现，同时左侧会显示**工具箱**。可以从工具箱将控件添加到该空白 **Form1** 中。（如果看不到工具箱，单击其选项卡即可看到，工具箱将出现）。

![](img/3005a4307e6d8f3bb7e76eea28a92357_597_0.png)

- 如下所示，**解决方案资源管理器**位于屏幕右侧。（如果看不到，请单击 Visual Studio Express 顶部**视图**菜单中的“解决方案资源管理器”项。）

![](img/3005a4307e6d8f3bb7e76eea28a92357_597_1.png)

![](img/3005a4307e6d8f3bb7e76eea28a92357_597_2.png)

- 这两个项目（控制台应用程序和 WindowsFormsApplication）都有“属性”“引用”部分以及一个 Program.cs 文件。
- 双击 Program.cs 文件将其打开，可看到以下代码。

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApplication1
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

- 应用程序代码包含 using 行、一个命名空间、一个名为 Program 的类以及一个 Main 方法。
- Main 方法是程序的入口点。Main 的花括号之间的代码将在程序首次启动时执行。上述 WindowsFormsApplication1 代码中的最后一行是在应用程序启动时运行 Form1 的那一行。Main 方法启动程序，而解决方案资源管理器中的 Program.cs 包含 Main 方法的代码。

![](img/3005a4307e6d8f3bb7e76eea28a92357_598_0.png)

图 20.2.7 应用程序文件

![](img/3005a4307e6d8f3bb7e76eea28a92357_599_0.png)

图 20.2.8 窗体属性

## 6. 向应用程序添加代码和控件

- 菜单中有“查看代码”和“查看设计器”选项。

![](img/3005a4307e6d8f3bb7e76eea28a92357_600_0.png)

图 20.2.9 窗体代码视图

![](img/3005a4307e6d8f3bb7e76eea28a92357_600_1.png)

图 20.2.10 窗体设计视图

- 代码包含 **partial class Form1**。它是分部类，因为部分代码对开发者隐藏。

![](img/3005a4307e6d8f3bb7e76eea28a92357_601_0.png)

图 20.2.11 窗体文件

```
namespace WindowsApplication1
{
    partial class Form1
    {
        /// <summary>...
        private System.ComponentModel.IContainer components = null;

        /// <summary>...
        protected override void Dispose(bool disposing)
        {
            if (disposing && (components != null))
            {
                components.Dispose();
            }
            base.Dispose(disposing);
        }

        Windows Form Designer generated code
    }
}
```

```
#region Windows Form Designer generated code

/// <summary>
/// Required method for Designer support - do not modify
/// the contents of this method with the code editor.
/// </summary>
private void InitializeComponent()
{
    this.components = new System.ComponentModel.Container();
    this.AutoScaleMode = System.Windows.Forms.AutoScaleMode.Font;
    this.Text = "Form1";
}

#endregion
```

- **InitializeComponent** 是创建新的 Windows 应用程序项目时**自动生成**的代码（一个方法）。添加新控件时，附加代码会添加到这里。
- 单击顶部 **Form1.cs** 选项卡返回以再次查看窗体。如果该选项卡不存在，请右键单击右侧解决方案资源管理器中的 Form1.cs。从菜单中选择**查看设计器**。

![](img/3005a4307e6d8f3bb7e76eea28a92357_602_0.png)

图 20.2.12 窗体设计视图

正是在设计器视图中，按钮和文本框等控件被添加到窗体。

## 7. 运行程序

- 单击“启动调试”时，Visual C# 会先生成程序，然后如果可以的话运行它。如果无法运行该程序，则显示错误消息。
- 要运行程序，可以按 F5，或单击**调试 > 启动调试**。

![](img/3005a4307e6d8f3bb7e76eea28a92357_603_0.png)

## 20.3 理解设计和代码视图

- 1. Visual Studio IDE 中有两个视图：**设计视图**和**代码视图**。打开 Visual Studio IDE 时，默认情况下会显示如下所示的设计视图。
- 2. **设计视图**允许拖动控件并将其放到窗体上。
- 3. **属性窗口**用于设置对象、窗体或解决方案资源管理器中显示的其他文件的属性。
- 4. **解决方案资源管理器**允许重命名项目、窗体，甚至项目中包含的其他文件。
- 5. **设计视图**提供了一种可视化的方式来处理控件、对象、项目文件等。
- 6. **代码视图**用于实现窗体上可视控件背后的功能。
- 7. 要在设计视图和代码视图之间**切换**，请单击“视图”->“代码”，或在设计视图中右键单击 Windows 窗体并选择“查看代码”。两种方法都会打开代码视图。

![](img/3005a4307e6d8f3bb7e76eea28a92357_604_0.png)

图 20.3.1 代码视图

- 8. 代码视图显示所有代码功能。
- 9. 在上图中，Form1.cs 选项卡是显示代码视图的选项卡，而 Form1.cs (Design) 选项卡实际上是 Windows 窗体 Form1 的设计模式；这些选项卡允许在设计视图的所有 GUI 元素与代码视图中用于提供功能的相关代码之间切换。应注意，只有在设计视图中，工具箱才完全加载了控件，而在代码视图中则没有。
- 10. 可以使用解决方案资源管理器在设计视图和代码视图之间切换：选择所需的 Windows 窗体（如果打开了多个 Windows 窗体），右键单击，然后选择“查看代码”或“查看设计器”。这将打开所选 Windows 窗体的代码视图或设计视图。

### 在属性窗口中对属性排序

各种对象和控件具有许多属性，可能需要浏览这些属性；对属性排序后浏览会更方便。属性排序可以按类别或按字母顺序进行。

![](img/3005a4307e6d8f3bb7e76eea28a92357_606_0.png)

图 20.3.3 属性的字母顺序视图

### 设置解决方案、项目和 Windows 窗体的属性

- 1. 选择“WindowsFormsApplication1”解决方案，转到属性窗口，并将其 Name 属性值设置为“WindowsFormApp”。
- 2. 要在 Visual Studio 中查看解决方案文件（.sln），请单击“工具”->“选项”，转到“项目和解决方案”选项卡，选择“常规”，勾选“始终显示解决方案”选项，然后单击“确定”。
- 3. 在解决方案资源管理器中选择“WindowsFormsApplication1”项目，转到属性窗口，修改 Project File 属性值（该值定义项目的文件名），使其显示为“WinApp.csproj”。在此处可以更改项目名称。
- 4. 在解决方案资源管理器窗口中单击“Form1”，以在属性窗口中设置属性列表。

![](img/3005a4307e6d8f3bb7e76eea28a92357_607_0.png)

图 20.3.4 设置解决方案、项目和 Windows 窗体属性的 IDE

## 20.4 C# 中的用户界面元素和控件类层次结构

![](img/3005a4307e6d8f3bb7e76eea28a92357_607_1.png)

图 20.4.1 C# 控件类层次结构

