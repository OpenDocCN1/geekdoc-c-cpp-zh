
## 第 2 章：开始使用 Visual Studio 2008

![](img/a977a875c7c627b45d939729705a252e_54_0.png)

图 2-32

![](img/a977a875c7c627b45d939729705a252e_54_1.png)

图 2-33

### 代码视图

代码视图是您编写应用程序代码的地方。您可以通过单击相关选项卡在设计视图和代码视图之间切换（参见图 2-34）。

![](img/a977a875c7c627b45d939729705a252e_55_0.png)

图 2-34

在 Visual Studio 中，您可以右键单击选项卡（参见图 2-35）以水平或垂直排列代码视图，以最大化使用您的显示器。

![](img/a977a875c7c627b45d939729705a252e_55_1.png)

图 2-35

## 第 2 章：开始使用 Visual Studio 2008

图 2-36 显示代码视图和设计视图水平显示。

![](img/a977a875c7c627b45d939729705a252e_56_0.png)

图 2-36

图 2-37 显示代码视图和设计视图垂直显示。

## 第 I 部分：C# 基础

![](img/a977a875c7c627b45d939729705a252e_57_0.png)

图 2-37

*同时拥有多个视图在您有大显示器（或多个显示器）时很有用。*

### 代码和文本编辑器

在 Visual Studio 2008 的代码视图中是代码和文本编辑器，它提供了多个丰富的特性，使编辑代码变得简单高效，包括：

- 代码片段
- IntelliSense 语句完成
- IntelliSense 对对象属性、方法和事件的支持
- 重构支持

### 代码片段

Visual Studio 2008 中的代码片段功能使您能够将常用的代码块插入到项目中，从而提高开发过程的效率。要插入代码片段，请在代码编辑器中右键单击要插入代码片段的位置，并选择插入片段（参见图 2-38）。

![](img/a977a875c7c627b45d939729705a252e_58_0.png)

通过单击类别名称选择片段类别（参见图 2-39 顶部），然后选择要插入的代码片段（参见图 2-39 底部）。

![](img/a977a875c7c627b45d939729705a252e_58_1.png)

例如，假设您选择了 try 代码片段。以下代码块将被自动插入：

```
private void Form1_Load(object sender, EventArgs e)
{
    try
    {
    }
    catch (Exception)
    {
        throw;
    }
}
```

您还可以使用“使用...环绕”代码片段功能。假设您有以下语句：

```
private void Form1_Load(object sender, EventArgs e)
{
    int num1 = 5;
    int num2 = 0;
    int result = num1 / num2;
}
```

第三条语句很危险，因为它可能导致除零运行时错误，因此最好将代码包装在 try-catch 块中。为此，您可以突出显示要放入 try-catch 块中的代码块并右键单击它。选择“使用...环绕”（参见图 2-40），然后选择 try 代码片段。

![](img/a977a875c7c627b45d939729705a252e_59_0.png)

图 2-40

您的代码现在如下所示：

```csharp
private void Form1_Load(object sender, EventArgs e)
{
    try
    {
        int num1 = 5;
        int num2 = 0;
        int result = num1 / num2;
    }
    catch (Exception)
    {
        throw;
    }
}
```

### IntelliSense

IntelliSense 是 Visual Studio 2008 中最有用的工具之一。IntelliSense 会在您在代码编辑器中输入时自动检测对象的属性、方法、事件等。您无需记住对象的确切成员名称，因为 IntelliSense 会通过动态为您提供相关成员列表来帮助您输入代码。

例如，当您在代码编辑器中输入单词 Console 后跟 . 时，IntelliSense 会显示与 Console 类相关的成员列表（参见图 2-41）。

![](img/a977a875c7c627b45d939729705a252e_60_0.png)

图 2-41

当您选择要使用的成员时，按 Tab 键，IntelliSense 将把该成员插入到您的代码中。

## 第 I 部分：C# 基础

Visual Studio 2008 中的 IntelliSense 有一些很好的增强功能。例如，IntelliSense 下拉列表在弹出时通常会遮挡后面的代码。现在，您可以通过按 Control 键使下拉列表暂时消失。图 2-42 显示了 IntelliSense 下拉列表遮挡其后面的代码（顶部）以及通过按 Control 键使其半透明（底部）。

![](img/a977a875c7c627b45d939729705a252e_61_0.png)

图 2-42

您还可以使用 IntelliSense 来整理代码顶部的命名空间。例如，您通常会在代码开头导入大量命名空间，其中一些可能永远不会被应用程序使用。在 Visual Studio 2008 中，您可以选择命名空间，右键单击并选择组织使用（参见图 2-43）。

![](img/a977a875c7c627b45d939729705a252e_61_1.png)

图 2-43

## 第 I 部分：C# 基础

您可以在更改应用于代码之前预览更改（参见图 2-46）。

![](img/a977a875c7c627b45d939729705a252e_63_0.png)

图 2-46

单击“应用”按钮以更改变量名称。

### 提取方法

通常，您会在应用程序中编写重复的代码。请考虑以下示例：

```
private void Form1_Load(object sender, EventArgs e)
{
    int num = 10, sum = 0;
    for (int i = 1; i <= num; i++)
    {
        sum += i;
    }
}
```

在这里，您将从 1 到 num 的所有数字相加，这是一个常见的操作。最好将此代码块打包成一个函数。因此，突出显示代码（参见图 2-47），右键单击它，并选择重构 ⇒ 提取方法。

![](img/a977a875c7c627b45d939729705a252e_63_1.png)

图 2-47

## 第 I 部分：C# 基础

如果在重构中排除变量 height 的声明（而不是选择全部三行；参见图 2-49）并将新方法命名为 VolumeofCylinder，则会创建一个具有两个参数的方法：

```
private void Form1_Load(object sender, EventArgs e)
{
    Single radius = 3.5f;
    Single height = 5;
    double volume = VolumeofCylinder(radius, height);
}
```

```
private static double VolumeofCylinder(Single radius, Single height)
{
    return Math.PI * Math.Pow(radius, 2) * height;
}
```

![](img/a977a875c7c627b45d939729705a252e_65_0.png)

图 2-49

以下是一些观察结果：

- 在重构中突出显示的块之外定义的变量将用作新方法中的输入参数。
- 如果变量在选定用于重构的块内声明，则新方法将没有签名。
- 在突出显示的代码块内更改的值将通过引用传递到新方法中。

### 重新排序和删除参数

您可以使用代码重构来重新排序函数中的参数。请考虑来自前一个示例的以下函数：

```
private static double VolumeofCylinder(Single radius, Single height)
{
    return Math.PI * Math.Pow(radius, 2) * height;
}
```

突出显示函数签名，右键单击它，并选择重构 ⇒ 重新排序参数（参见图 2-50）。

## 第 2 章：开始使用 Visual Studio 2008

![](img/a977a875c7c627b45d939729705a252e_66_0.png)

图 2-50

然后您可以重新排列参数列表的顺序（参见图 2-51）。

![](img/a977a875c7c627b45d939729705a252e_66_1.png)

图 2-51

单击“确定”。您可以在更改之前预览更改（参见图 2-52）。

![](img/a977a875c7c627b45d939729705a252e_66_2.png)

图 2-52

## 第 I 部分：C# 基础

一旦单击“应用”按钮，您的代码就会自动更改：

```csharp
private void Form1_Load(object sender, EventArgs e)
{
    Single radius = 3.5f;
    Single height = 5;
    double volume = VolumeofCylinder(height, radius);
}
```

```csharp
private static double VolumeofCylinder(Single height, Single radius)
{
    return Math.PI * Math.Pow(radius, 2) * height;
}
```

所有调用已修改函数的语句都将自动更改其参数顺序。

您还可以通过突出显示函数签名、右键单击并选择重构 ⇨ 删除参数来从函数中删除参数。然后删除您想要删除的参数（参见图 2-53）。所有调用已修改函数的语句都将自动更改其调用。

![](img/a977a875c7c627b45d939729705a252e_67_0.png)

图 2-53

### 封装字段

请考虑以下字符串声明：

```csharp
namespace WindowsFormsApplication1
{
    public partial class Form1 : Form
    {
        public string caption;

        private void Form1_Load(object sender, EventArgs e)
        {
            //...
        }
    }
}
```
