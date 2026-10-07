
注意抽象属性显示了 `get` 和 `set` 访问器，但它没有指定这些访问器的操作。当抽象属性出现在类中时，要在任何派自该类的类中被重写。在这个示例中，如果一个类派自 `Person` 类，该派生类必须重写 `JobTitle` 属性。

> 注意
> 如果你想创建一个只读属性，请省略 `set` 访问器。

在教程 11-3 中，你完成了一个使用带有抽象属性的抽象基类的应用程序。

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1496_0.png)

# 教程 11-3：完成计算机科学学生申请程序

在本教程中，你将编写一个名为 `Student` 的抽象类。`Student` 类持有所有学生共有的数据，但并不包含特定专业学生所需的所有数据。`Student` 类旨在作为一个基类，可以由其他代表特定专业学生的类派生。

`Student` 类有一个名为 `Name` 的属性用于存储学生的姓名，以及一个名为 `ID` 的属性用于存储学生的学号。它还包含一个名为 `RequiredHours` 的抽象只读属性。`RequiredHours` 属性的目的是存储特定专业所需的学时。任何派自 `Student` 类的类都必须重写 `RequiredHours` 属性。

你还将编写一个派自 `Student` 类的 `CompSciStudent` 类。`CompSciStudent` 类有一个名为 `AcademicTrack` 的字段，用于存储学生学术流向的名称。它还重写了 `RequiredHours` 属性，以计算并返回计算机科学专业所需的学时。

你将在计算机科学应用程序中演示这些类。该应用程序的表单已经为你创建好，如图 11-10 所示。当你运行完成后的应用程序时，将在文本框中输入学生的姓名和学号，并使用单选按钮选择学术流向。当你点击 "Get Required Hours" 按钮时，应用程序将创建一个 `CompSciStudent` 对象并用你输入的数据进行初始化。它将获取 `RequiredHours` 属性的值并将其显示在表单上。

## 图 11-10 计算机科学学生应用程序表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1498_0.png)

第 1 步：启动 Visual Studio。在 Student Sample Programs 的 `Chap11` 文件夹中打开名为 `Computer Science Student` 的项目。

第 2 步：点击 Visual Studio 菜单栏上的 Project（项目）并选择 Add Class...（添加类...）。将出现添加新建项窗口。确保项目类型选择的是 Class（类）。将默认文件名更改为 `Student.cs`，然后点击 Add（添加）按钮。这将向项目添加一个名为 `Student.cs` 的源文件。

第 3 步：现在代码编辑器中应应显示 `Student.cs` 文件。在类头中添加 `abstract` 关键字，如 Program 11-10 中的第 9 行所示。接下来，通过输入 Program 11-10 中的第 11–23 行完成 `Student` 类的代码。

第 4 步：点击 Visual Studio 菜单栏上的 Project（项目）并选择 Add Class...（添加类...）。将添加新建项窗口。确保项目类型选择的是 Class（类）。将默认文件名更改为 `CompSciStudent.cs`，然后点击 Add（添加）按钮。这将向项目添加一个名为 `CompSciStudent.cs` 的源文件。

第 5 步：现在代码编辑器中应显示 `CompSciStudent.cs` 文件。在类头中添加 `: Student` 符号，如 Program 11-11 中的第 9 行所示。然后，通过输入 Program 11-11 中的第 11–33 行完成 `CompSciStudent` 类的代码。

注意第 30–33 行中的 `RequiredHours` 属性重写了基类中的抽象 `RequiredHours` 属性。该属性计算并返回所需的学时。

第 6 步：现在你将为 Button 控件创建 Click 事件处理程序。在设计器（Designer）中切换视图到 `Form1` 表单。双击代码编辑器中的 `getHoursButton.cs` 文件，你将看到一个名为 `getHoursButton_Click` 的空 `Form1.cs` 事件处理程序。通过输入 Program 11-12 中第 22–45 行所示的代码完成事件处理程序。让我们回顾这段代码：

- **第 23 行：** 该语句声明了三个本地字符串变量：`name`、`id` 和 `track`。它们将用于存储用户输入。
- **第 26–27 行：** 这些语句存储用户输入。
- **第 30–37 行：** 这些语句获取用户输入的姓名和 ID 并赋值变量。
- **第 40–41 行：** 该语句创建 `CompSciStudent` 对象并初始化。
- **第 44–45 行：** 该语句获取 `RequiredHours` 属性的值并显示在表单上。

第 7 步：在设计器中切换回 `Form1` 表单。双击代码编辑器中的 `getHoursButton.cs` 文件，你将看到一个名为 `getHoursButton_Click` 的空 `Form1.cs` 事件处理程序。通过输入 Program 11-12 中第 50–51 行所示的代码完成事件处理程序。

第 8 步：保存项目。然后按 `F5` 编译并运行应用程序。在运行时，在 TextBox 中输入数据，通过单选按钮选择学术流向。点击 "Get Required Hours" 按钮，你会看到所需的学时显示。

### Program 11-10 Student.cs 计算机科学应用程序中的代码

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using System.Threading.Tasks;
namespace ComputerScienceStudent{
abstract class Student
{
    // 构造函数
    public Student(string name, string id)
    {
        Name = name;
        ID = id;
    }
    // 属性
    public string Name
    {
        get;
        set;
    }
    public string ID
    {
        get;
        set;
    }
    // 抽象属性
    public abstract double RequiredHours { get; }
}
```

### Program 11-11 CompSciStudent.cs 计算机科学应用程序中的代码

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using System.Threading.Tasks;
namespace ComputerScienceStudent
    class CompSciStudent : Student
    {
        // 常量
        private double MATH_HOURS = 20;
        private double CS_HOURS = 40;
        private double GEN_HOURS = 60;
        // 字段
        private string _academicTrack;
        // 构造函数
        public CompSciStudent(string name, string id, string track)
            : base(name, id)
        {
            _academicTrack = track;
        }
        // AcademicTrack 属性
        public string AcademicTrack
        {
            get;
            set;
        }
        // RequiredHours 属性
        public override double RequiredHours
        {
            return MATH_HOURS + CS_HOURS + GEN_HOURS;
        }
    }
}
```

### Program 11-12 Form1 计算机科学应用程序中的代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
namespace ComputerScienceStudent
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void getHoursButton_Click(object sender, EventArgs e)
        {
            // 存储输入
            string name, id, track;
            // 获取学生的姓名和 ID。
            name = nameTextBox.Text;
            id = idTextBox.Text;
            // 获取学生的学术流向。
            if (infoSystemsRadioButton.Checked)
            {
                track = "Information Systems";
            }
            else
            {
                track = "Software Engineering";
            }
            // 创建 CompSciStudent 对象。
            CompSciStudent csStudent = new CompSciStudent(name, id, track);
            // 显示学生所需的学时。
            requiredHoursLabel.Text = csStudent.RequiredHours.ToString();
        }
        private void exitButton_Click(object sender, EventArgs e)
        {
            // 关闭表单。
            this.Close();
        }
    }
}
```

**11.8** 抽象类的目的是什么？

**11.9** 如果一个类是抽象的，那么该类不能进行哪些操作？

**11.11** 在使用抽象属性之前，必须对其进行什么操作？

**11.12** 如何创建一个抽象的只读属性？

## 11.4 扩展方法

### 概念

扩展方法是一种扩展现有类或数据类型（包括 .NET Framework 中的类和类型）的静态方法。

假设你想扩展一个类，但由于该类是密封的（`sealed`），你无法继承自它。当你想要扩展的类位于 .NET Framework 中，或者是由其他人编写时，就可能会出现这种情况。在这种情况下，你可以使用扩展方法来扩展该类。**扩展方法**是一种可以在不修改类或不继承自该类的情况下将其添加到类中的方法。

扩展方法可以应用于类、`structs` 和接口（将在本章稍后部分进行讨论）。它们甚至可以应用于 `int` 和 `double` 等原始类型。事实上，让我们看看如何将扩展方法应用于原始数据类型 `int`。假设我们想让 `int` 变量拥有一个方法，告诉我们变量是奇数还是偶数。例如，我们希望能够执行类似下面的代码：

```csharp
int number = 4;
if (number.IsEven())
{
    MessageBox.Show("The number is even.");
}
```

为了实现这一点，我们需要为 `int` 类型定义一个名为 `IsEven` 的扩展方法。如果该方法评估的数字是偶数，则返回 `true`，否则返回 `false`。

以下是实现扩展方法需要知道的关键点：

- 扩展方法是静态方法，存储在静态类中。你可以在同一个静态类中编写多个扩展方法。
- 建议将扩展方法的类放在自己的命名空间中，与项目的命名空间分开。
- 扩展方法始终至少有一个参数。方法的第一个参数必须是该方法所扩展的类或类型的对象。第一个参数的声明必须以关键字 `this` 开头。

下面是之前展示的 `IsEven` 扩展方法的示例：

```csharp
namespace ExtensionMethods
{
    public static class Extensions
    {
        public static bool IsEven(this int i)
        {
            return (i % 2) == 0;
        }
    }
}
```

此代码定义了一个名为 `ExtensionMethods` 的命名空间，在该命名空间内有一个名为 `Extensions` 的静态类。（任何使用该扩展方法的程序都需要包含 `using ExtensionMethods;` 语句才能访问该方法。）在 `Extensions` 类中，第 5–8 行定义了静态方法 `IsEven`。仔细观察第 5 行中的参数声明：

```csharp
this int i
```

`this` 关键字告诉编译器该方法是一个扩展方法。参数 `i` 是一个 `int`，因此编译器知道我们正在为 `int` 数据类型定义扩展方法。当方法执行时，`i` 参数将引用方法正在处理的 `int` 变量。例如，查看以下代码：

```csharp
int minValue = 4;
if (minValue.IsEven())
{
    MessageBox.Show("The number is even.");
}
```

在此代码中，当 `IsEven` 方法执行时，`minValue` 变量将隐式地传递给 `i` 参数。这在图 11-11 中所示。这是另一个示例：

```csharp
int num = 4;
if (num.IsEven())
{
    MessageBox.Show("The number is even.");
}
```

### 图 11-11 myValue 被隐式地传递到 i 参数中

```csharp
myValue.IsEven()
public static bool IsEven(this int i)
{
  return (i % 2) == 0;
}
```

> 注意
> 扩展方法可以有多个参数。然而，`this` 关键字仅出现在第一个参数之前。

在此代码中，当 `IsEven` 方法执行时，`num` 变量将隐式地传递给 `i` 参数。

扩展方法必须至少有一个参数，并由 `this` 关键字前置，以引用方法正在处理的对象。如果你需要显式地向扩展方法传递其他参数，只需在第一个参数之后声明额外的参数即可。这是一个示例：

```csharp
public static bool IsGreaterThan(this int a, int b)
{
    return a > b;
}
```

该方法有两个参数：`a` 和 `b`。因为 `a` 前面有 `this` 关键字，我们知道它将隐式引用方法正在处理的 `int`。`b` 参数将持有显式传递给方法的任何值。以下是我们如何调用该方法的示例：

```csharp
int num1 = 5, num2 = 4;
if (num1.IsGreaterThan(num2))
{
    MessageBox.Show("num1 is greater than num2.");
}
```

在此代码中，当 `IsGreaterThan` 方法执行时，`num1` 变量将传递给 `a` 参数，`num2` 变量将传递给 `b` 参数。这在图 11-12 中所示。

## 图 11-12 num1 被隐式地传递到 a 参数，且 num2 被传递

```csharp
num1.IsGreaterThan(num2)
public static bool IsGreaterThan(this int a, int b)
{
    return a > b;
}
```

应用程序输出的三个不同示例，每个示例提供了不同的输入。

### 图 11-14 扩展方法应用程序的示例输出

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1515_0.png)

# 程序 11-14 整数扩展方法应用程序的 Form1 代码

```
