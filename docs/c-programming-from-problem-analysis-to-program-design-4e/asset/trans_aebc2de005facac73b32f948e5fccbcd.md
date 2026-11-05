
**注意** 在 **视图** 菜单中选择 **代码** 会显示与 Form1.cs 文件关联的源代码。在设计模式下双击窗体，会转到 **代码编辑器**，但会产生不希望的副作用：代码中会添加 `Form1_Load()` 事件处理程序方法标头和空方法体。你将在第 10 章进一步了解事件。每个控件都有一个默认事件。双击大多数控件会将其默认事件处理程序方法添加到代码中。窗体的默认事件是 Load 事件。

图中展示了三个文件。创建简单的 Windows 应用程序时，IDE 会将源代码分成三个文件。最初这些文件命名为 Form1.cs、Form1.Designer.cs 和 Program.cs。前两个文件 Form1.cs 和 Form1.Designer.cs 都包含 Form1 类的 `partial class` 定义。建议永远不要编辑 Form1.Designer.cs 文件。通常只需编辑 Form1.cs 文件。

Program.cs 文件包含 `Main()` 方法，执行总是从那里开始。`Main()` 方法中的三行代码之一是对 `Application.Run()` 的调用，它使窗体可见并准备好接收用户输入。示例 9-2 中显示的代码完全由 Visual Studio 生成。对示例 9-2 所做的唯一更改是针对注释进行的。Visual Studio 插入的 XML 注释被删除，并添加了新的内联注释。

**注意** 你将在第 11 章进一步了解 `partial` 类。分部类允许将一个 `class` 的定义拆分到两个或多个文件中。

## 示例 9.2

```csharp
//FirstWindows.Form1.cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace FirstWindows
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
    } // End of FirstWindows.Form1.cs file
}
```

```csharp
//FirstWindows.Form1.Designer.cs
namespace FirstWindows
{
    partial class Form1
    {
        // Required designer variable.
        private System.ComponentModel.IContainer components = null;
        // Clean up any resources being used.
        protected override void Dispose(bool disposing)
        {
            if (disposing && (components != null))
            {
                components.Dispose();
            }
            base.Dispose(disposing);
        }
#region Windows Form Designer generated code
        // Required method for Designer support - do not modify
        // the contents of this method with the Code Editor.
        private void InitializeComponent()
        {
            this.SuspendLayout();
            // Form1
            this.AutoScaleDimensions = new System.Drawing.SizeF(10F, 19F);
            this.AutoScaleMode = System.Windows.Forms.AutoScaleMode.Font;
            this.AutoScroll = true;
            this.BackColor = System.Drawing.Color.FromArgb(((int)(((byte)(255)))), ((int)(((byte)(224)))), ((int)(((byte)(192)))));
            this.ClientSize = new System.Drawing.Size(392, 373);
            this.Font = new System.Drawing.Font("Arial", 12F, System.Drawing.FontStyle.Bold, System.Drawing.GraphicsUnit.Point, ((System.Byte)(0)));
            this.ForeColor = System.Drawing.Color.Blue;
            this.Location = new System.Drawing.Point(30, 30);
            this.Margin = new System.Windows.Forms.Padding(4);
            this.MaximizeBox = false;
            this.Name = "Form1";
            this.StartPosition = System.Windows.Forms.FormStartPosition.CenterScreen;
            this.Text = "First Windows Application";
            this.ResumeLayout(false);
        }
#endregion
    }
} // End of FirstWindows.Form1.Designer.cs file
```

```csharp
//FirstWindows.Program.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace FirstWindows
{
    static class Program
    {
        // The main entry point for the application.
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new Form1());
        }
    }
}
// End of FirstWindows.Program.cs file
```

通过从 Visual Studio 的 **调试** 菜单中选择 **开始调试** 或 **开始执行（不调试）**，你可以像运行控制台应用程序一样运行 Windows 应用程序。也可以使用快捷键 **F5** 和 **Ctrl+F5**，或单击 **标准** 工具栏上的 **启动** 图标来运行应用程序。运行示例 9-2 中的程序时，屏幕中央会显示一个桃色窗口，标题为“First Windows Application”。标题栏上的“最大化”按钮灰显。StartPosition 属性覆盖了所设置的 Location 属性值。查看 StartPosition 的下拉菜单选项时，注意 Manual 是可选择的值之一。选择 Manual 会启用 Location 属性来更改窗体的显示位置。

**注意** 你可以提前查看图 9-8，了解添加标题栏文字、Windows 最大化按钮灰显以及颜色设置为桃色后窗体的外观。图 9-8 只包含一个额外叠加在窗体上的 MessageBox 对话框。它是在后续示例中添加的。

## 检查 Visual Studio 生成的代码

检查图 9-7 所示的 **解决方案资源管理器** 窗口，可以看到属于该应用程序的三个以 .cs 扩展名结尾的源代码文件。控制台应用程序只创建一个源代码文件。

查看图 9-7 时，请注意三个文件之一实际上显示在 Form1.cs 结构下。这就是 Form1.Designer.cs 文件。正是在这个文件中，你会找到与为应用程序设置的属性相关联的 Windows 窗体设计器生成的代码。

![](img/36e48639a06772bcb0fa1ea2525b33a3_550_0.png)

![](img/36e48639a06772bcb0fa1ea2525b33a3_551_0.png)

**图 9-7** 解决方案资源管理器窗口

在示例 9-2 中，你看到了两行以井号（#）开头的代码。这些行位于 `Form1.Designer.cs` 文件中。第一行是 `#region Windows Forms Designer generated code`。在该行下方约 20 行处，你会找到 `#endregion`。`#region` 这个术语是 C# 中可以包含的预处理器指令之一。**预处理器指令** 表示应在处理之前完成的某些操作。预处理器指令通常与有条件地跳过源文件中的某些部分或报告特定类型的错误有关。

> 根据 C# 语言参考规范，“预处理器”这一术语的使用只是为了保持一致。C# 没有像 C++ 和其他语言那样单独的预处理步骤，在那些语言中，以 # 开头的语句会被识别为预处理器指令。

C# 中的 `#region` 预处理器指令用于显式标记可以展开或折叠的源代码段。如果你在 Visual Studio **代码编辑器** 中查看代码，请注意该指令左侧会出现减号（−）或加号（+）符号。单击（−）符号会折叠 # 符号之间的整个代码块，并以标记为“Windows Forms Designer generated code”的注释表示。单击（+）会展开列表。也可以使用 **Ctrl+M+M** 快捷键展开或折叠该区域。

> 你可以使用 `#region` 预处理器指令创建自己的区域。只需在 `#region` 后面添加一个为区域命名的标签。要结束该块，请使用 `#endregion`，就像 `#region Windows Forms Designer generated code... #endregion` 中那样。这有助于提高代码的可读性和可维护性。

