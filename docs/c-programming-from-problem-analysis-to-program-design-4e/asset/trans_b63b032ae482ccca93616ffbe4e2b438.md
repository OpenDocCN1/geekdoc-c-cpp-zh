
## 为 DLL 添加引用

为 Person 和 Student 类都必须添加引用。如果需要帮助添加引用，请参阅图 11-8 至 11-10。两者都应在 PresentationGUI 项目中引用，如图 11-12 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_755_0.png)

**图 11-12** PresentationGUI 类中引用的 DLL

## 为命名空间添加 using 语句

为避免输入完全限定名称，请为 Student 命名空间添加 `using` 指令。在之前的示例中，Student 项目使用的命名空间为 StudentNamespace。因此，示例 11-13 展示了如何为 StudentNamespace 添加 `using` 指令。

### 示例 11-13

```csharp
using StudentNamespace;
```

因为 Student 类已包含对 PersonNamespace 的 `using` 语句，并且没有实例化 Person 对象，因此在 PresentationGUI 类中不必在此添加 PersonNamespace 的 `using` 语句。然而，如果也添加 `using` PersonNamespace; 则不会产生语法错误。

## 声明组件类型的对象

必须声明一个 Student 对象。这在 PresentationGUI 类内部作为私有数据成员完成，如示例 11-14 所示。

### 示例 11-14

```csharp
public class PresentationGUI : System.Windows.Forms.Form
{
    private Student aStudent;
}
```

示例 11-14 中的语句声明了一个 Student 对象。当然，你也可以使用数组定义 Student 对象的集合。

## 实例化对象

要创建或实例化 Student 类的实际对象，必须使用其中一个 Student 构造函数。请记住为 Student 类定义了两个构造函数。因此，实例化该类的一种方法是写：

```csharp
aStudent = new Student("123456789", "Maria", "Woo", "CS", "1111");
```

此实例化放置在处理窗体加载事件的方法中。它也可以放置在 InitializeComponent() 方法中，该方法放置了 Windows Forms 设计器生成的代码。

## 使用派生类和基类成员

向窗体添加了若干控件对象。TextBox 对象被拖到窗体上用于显示姓名、年龄、学生 ID、学生的睡眠量以及他人的睡眠量。添加了一个 Button 对象用于填充 TextBox 对象。示例 11-15 显示了为 PresentationGUI 输入的程序语句。由于篇幅限制，Windows Forms 设计器生成的代码未包含在列表中。

### 示例 11-15

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
using StudentNamespace;      // Added for Student class
```

```csharp
namespace PresentationGUI
{
    public partial class PresentationGUI : Form
    {
        private Student aStudent;

        public PresentationGUI()
        {
            InitializeComponent();
        }

        private void PresentationGUI_Load
            (object sender, EventArgs e)
        {
            aStudent =
                new Student("123456789", "Maria", "Woo", "CS", "1111");
        }

        private void btnShow_Click(object sender, EventArgs e)
        {
            // Uses Age property defined in the Person class
            aStudent.Age = 25;

            // Calls overridden ToString() defined in Person class
            txtBxName.Text = aStudent.ToString();

            // Calls ToString() defined in object class
            txtBxAge.Text = aStudent.Age.ToString();

            // Uses StudentID property defined in Student class
            txtBxID.Text = aStudent.StudentID;

            // Calls GetSleepAmt() defined in Student class
            txtBxStudentSleep.Text =
                Convert.ToString(aStudent.GetSleepAmt());

            // Calls method defined in Student class that
            // has calls to base.GetSleepAmt() in Person class
            txtBxPersonSleep.Text =
                Convert.ToString
                (aStudent.CallOverriddenGetSleepAmt());
        }
    }
}
```

图 11-13 显示了运行 PresentationGUI 生成的输出。它引用了两个 DLL 组件。

![](img/36e48639a06772bcb0fa1ea2525b33a3_758_0.png)

**图 11-13** 引用两个 DLL 的 PresentationGUI 输出

任意数量的类都可以通过实例化其类型的对象来使用 Student 和 Person 组件。所需的只是新应用程序引用以 .dll 结尾的文件。可以为命名空间添加 using 语句，以避免键入类及其成员的完全限定名称。

> 注
> 当然，另一个选项是将实际源代码（.cs 文件）包含在应用程序中，就像你在之前章节开发的项目中所做的那样。继承并不要求使用组件。

## 使用 ILDASM 查看程序集（可选）

DLL 文件不能被修改或作为源代码查看。Visual Studio 包含许多开发人员工具。其中之一是中间语言反汇编程序（ILDASM）工具，有助于处理以 .dll 或 .exe 结尾的文件。该工具用于查看程序集。ILDASM 可以从命令行运行，也可以作为外部工具添加到 Visual Studio 并在 IDE 内运行。程序集显示所有方法、数据字段和属性的签名。ILDASM 的一个选项是在程序集中将源代码作为注释显示。图 11-14 显示了使用 ILDASM 生成的 Student.dll 程序集。

![](img/36e48639a06772bcb0fa1ea2525b33a3_759_0.png)

**图 11-14** 来自 ILDASM 的 Student.dll 程序集

**注** ILDASM 与 Visual Studio 一起自动安装。要运行该工具，可以使用 Visual Studio 命令提示符。在任务栏上，单击 **开始, 所有程序, Microsoft Visual Studio 2012, Visual Studio 工具**，然后单击 **VS2012 的开发人员命令提示符**。在提示符下，键入 **ildasm**。从那里你可以使用 **文件** 菜单浏览到 .dll 文件的位置。

查看程序集有助于确定如何调用或使用方法。ILDASM 输出包括数据字段和属性的标识符及其数据类型。如图 11-14 所示，用红色三角形显示的任何已定义属性在程序集中也作为方法出现。属性方法的标识符以 get_ 或 set_ 为前缀，具体取决于它们是只读还是作为属性的一部分提供 get 和/或 set。程序集还显示构造函数所需的参数。Student 定义了两个构造函数（.ctor）。通过单击方法名称在程序集中向下钻取会显示该方法的中间语言（IL），当选择 CallOverriddenGetSleepAmt( ) 方法时即得到说明。

## 全局程序集缓存

要运行包含 DLL 组件的应用程序，DLL 文件必须位于当前目录、子目录或全局程序集缓存（GAC）中。**全局程序集缓存** 是在安装了通用语言运行时（CLR）的每台机器上都可用的机器范围代码缓存。GAC 存储指定由多个应用程序共享的程序集，并存储一些 .NET 组件。尽管你可以将程序集放入 GAC，但最好不要这样做。因为它是一个缓存资源，空间有限。通过将它们放置在应用程序目录中，保持程序集依赖项为私有。

## 抽象类

通过前面的示例，你可以以与构造 Student 类对象相同的方式实例化 Person 类的对象。包括 C# 在内的大多数现代语言允许你向类添加 **abstract** 修饰符，从而禁止其他类实例化基类的对象。你仍然可以在子类中继承此基类的特征，这使你能够确保子类具有一定量的相同功能。此基类可以具有数据和方法成员。要在 C# 中创建抽象类，你可以写：

```csharp
[access modifier] abstract class ClassIdentifier { }  // Base class
```

当你将 **abstract modifier** 关键字与类一起使用时，你将其标记为只能用作其他类派生的基类。然后不能实例化基类类型的对象。为了表示 `Person` 类仅 intended 用于作为其他类的基类，你添加 abstract 关键字，如示例 11-16 所示。

### 示例 11-16

```csharp
public abstract class Person
{ . . . }
```

在添加 abstract 修饰符后，任何尝试实例化 `Person` 类对象的操作都会导致以下语法错误：“Cannot create an instance of the abstract class or interface PersonNamespace.Person。”添加 abstract 关键字不会阻止你实例化派生自 Person 类的类，例如 Student 类。

## 抽象方法

抽象类可能包含一个或多个抽象方法。抽象方法仅允许在抽象类中使用。**抽象方法** 是不包含方法实现细节的方法。该方法没有主体。该方法的实现细节留给派生自基抽象类的类来决定。创建抽象方法的语法如下：

```csharp
[access modifier] abstract returnType
                    MethodIdentifier([parameter list]); // No { }
```
