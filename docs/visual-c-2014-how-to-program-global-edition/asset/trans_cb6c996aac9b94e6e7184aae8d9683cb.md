

## 15.13 视觉继承

即使名称相同，也可以使用完全限定类名来区分应用程序中的类并防止名称冲突（也称为命名冲突）。

### 步骤 3：编译类库

为了允许其他 Form继承自 VisualInheritanceForm，我们必须将 Visual-InheritanceForm 打包为类库并将其编译为 .dll 文件。此类文件被称为动态链接库——一种可以在其他程序中引用的类打包方式。在“解决方案管理器”中右键点击项目名称并选择“属性”，然后在“应用程序类型”下拉列表中，将“Windows 应用程序”更改为“类库”。生成项目将产生 .dll 文件。在首次创建项目时，可以通过“新建项目”对话框中选择“类库”模板来将项目配置为类库。[注：库不能作为独立程序存在。图 15.45 中的屏幕截图是在项目更改为类库之前拍摄的。]

### 步骤 4：添加类库的引用

一旦类被编译并存储在类库中，就可以通过在 Visual Studio 中查找类库文件，从任何应用程序中引用它。要视觉地继承 VisualInheritanceBaseForm，首先创建一个新的 Windows 应用程序。在“解决方案管理器”窗口中右键点击“引用”，并从弹出菜单中选择“添加引用...”。对话框将包含来自 .NET Framework 的类库列表。某些库（如包含 System 命名空间的库）是你将要添加到 IDE 的库。这些库不会列在其中。

在“引用管理器”对话框中，点击“浏览...”按钮。当你编译类库时，Visual 会将 .dll 文件放在项目的 `bin\Debug` 或 `bin\Release` 文件夹中，取决于 IDE 工具栏中的“解决方案配置”下拉列表是设置为 Debug 还是 Release。在“浏览”选项卡中，你可以导航到包含步骤 3 中创建的类库的目录，如图 15.46 所示。选择 .dll 文件并点击“添加”。

![](img/57baed2319be0bb1b5f98674846f2711_693_0.png)

图 15.46 | 使用引用管理器对话框浏览 DLL。（2 部分中的第 1 部分）

![](img/57baed2319be0bb1b5f98674846f2711_694_0.png)

图 15.46 | 使用引用管理器对话框浏览 DLL。（2 部分中的第 2 部分）

**步骤 5：使用类——派生自基类***

打开定义新应用程序 GUI 的文件，并修改定义类的行，指示应用程序的 Form 应该继承自类 VisualInheritanceBase。类声明现在显示如下：

```
public partial class VisualInheritanceTest:
    VisualInheritanceBase.VisualInheritanceBase
```

除非你在 `using` 指令中指定命名空间 `VisualInheritance`，否则你必须使用完全名 `VisualInheritanceBase.VisualInheritanceBase`。在设计视图中，新应用程序的 Form 现在应该显示继承自基 Form 的控件（图 15.47）。我们现在可以向 Form 添加更多组件。

![](img/57baed2319be0bb1b5f98674846f2711_694_1.png)

图 15.47 | 展示视觉继承的 Form。

## **类 VisualInheritanceTest**

类 VisualInheritanceTest（图 15.48）是 VisualInheritanceBaseForm 的派生类。输出说明了程序的功能。组件、它们的布局以及基类 VisualInheritanceBaseForm 的功能（图 15.45）都被 VisualInheritanceTest 继承。我们额外添加了一个带有文本“About this Program”的按钮。当你按下此按钮时，会调用方法 `button_Click`（图 15.48，第 19–25 行）。此方法显示另一个 `MessageBox`，提供不同的信息文本（第 21–24 行）。

```
// Fig. 15.48: VisualInheritanceTestForm.cs
// 使用视觉继承的派生 Form。
using System;
using System.Windows.Forms;

namespace VisualInheritanceTest
{
    // 使用视觉继承的派生 Form
    public partial class VisualInheritanceTestForm :
        VisualInheritanceBase.VisualInheritanceBase
    {
        // 构造函数
        public VisualInheritanceTestForm()
        {
            InitializeComponent();
        }

        // 点击按钮时显示 MessageBox
        private void aboutButton_Click(object sender, EventArgs e)
        {
            MessageBox.Show("This program was created by Deitel & Associates.",
                "About This Program", MessageBox.OK,
                MessageBoxIcon.Information);
        }
    }
}
```

![](img/57baed2319be0bb1b5f98674846f2711_695_0.png)

图 15.48 | 使用视觉继承的派生 Form。

如果用户点击“Learn More”按钮，该事件将由基类事件处理程序 `learnMoreButton_Click` 处理。由于 VisualInheritanceBase 使用私有访问修饰符声明其控件，VisualInheritanceTestForm 无法通过程序方式修改继承自 VisualInheritanceBase 类的控件。IDE 在视觉继承的控件的左上角显示一个小图标，以指示它们是继承的且无法更改。

## 15.14 用户定义控件

.NET Framework 允许你创建自定义控件。这些自定义控件出现在你的工具箱中，并可以像添加按钮、标签和其他其他预定义控件一样添加到 Form、Panel 或 Group 中。创建自定义控件的最简单方法是从现有控件（如 Label）派生一个类。如果你想为现有控件添加功能，而不是用一个提供所需功能的控件来替换它，这种方法非常有用。例如，你可以创建一个新类型的 Label，它的行为像普通 Label，但外观不同。你可以通过继承自 `Label` 并重写 `OnPaint` 来实现这一点。

### OnPaint 方法

所有控件都有 `OnPaint` 方法，系统在必须重绘组件时（控件调整大小时）会调用该方法。该方法接收一个 `PaintEventArgs` 对象，包含图形信息——属性 `Graphics` 是用于绘图的对象，属性 `ClipRectangle` 定义了控件的矩形边界。当系统引发 `Paint` 事件以在屏幕上绘制控件时，控件捕获该事件并调用其 `OnPaint` 方法。在执行自定义绘图代码之前，应该在重写的 `OnPaint` 实现中显式地调用基类的 `OnPaint`。在大多数情况下，你需要确保执行的原始绘图代码定义在控件类中。

### 创建新控件

要创建一个由现有控件组成的新控件，请使用 `UserControl`。添加到自定义控件的控件被称为组成控件。对于一个程序，你可以创建一个由 `Button`、`Label` 和 `TextBox` 组成的 `UserControl`，每个控件关联某些功能（例如，按钮将标签设置为 TextBox 中的内容）。`UserControl` 作为所添加控件的容器。`UserControl` 处理组成控件，但它并不决定这些组成控件的显示方式。每个控件都可以处理自己的 `Paint` 事件或重写 `OnPaint`。处理程序和 `OnPaint` 都会传递一个 `PaintEventArgs` 对象，可以使用它在控件上绘制图形（线条、矩形等）。

使用另一种技术，可以通过继承 `Control` 来创建一个新控件。该类没有定义任何特定行为；这些交给你。相反，`Control` 处理与所有控件相关的项，例如事件和调整大小的方法。`OnPaint` 方法包含对基类 `OnPaint` 的调用，该方法会调用 `Paint` 事件处理程序。你在重写的 `OnPaint` 方法内部添加绘制自定义图形的代码。这种技术允许最大的灵活性，但也需要最多的规划。所有三种方法都总结在图 15.49 中。

