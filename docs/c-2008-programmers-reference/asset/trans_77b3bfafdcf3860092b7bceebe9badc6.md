

```csharp
private void Method3()
{
    //---implementation here---
}
}
```

通常情况下，你会有很多执行特定任务的函数。在这种情况下，最好将它们组织到区域中，以便在需要时折叠和展开。使用此示例，你可以使用 `#region` 和 `#endregion` 预处理指令将所有方法 —— Method1()、Method2() 和 Method3() —— 分组到一个区域中：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TestDefine
{
    class Program
    {
        static void Main(string[] args)
        {
        }

        #region "Helper functions"

        private void Method1()
        {
            //---implementation here---
        }

        private void Method2()
        {
            //---implementation here---
        }

        private void Method3()
        {
            //---implementation here---
        }

        #endregion
    }
}
```

在 Visual Studio 2008 中，现在可以将所有方法折叠到名为“Helper functions”的组中。图 3-19 显示了区域折叠前后代码编辑器的状态。

![](img/a977a875c7c627b45d939729705a252e_145_0.png)

图 3-19

`#region` 和 `#endregion` 预处理指令不会影响代码的逻辑。它们仅在 Visual Studio 2008 中用于更好地组织代码。

### #pragma warning

`#pragma warning` 指令用于启用或禁用编译器警告消息。例如，考虑以下程序：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TestDefine
{
    class Program
    {
        int num = 5;
        static void Main(string[] args)
        {
        }
    }
}
```

在此程序中，变量 `num` 已定义但从未使用。编译应用程序时，C# 编译器将显示一条警告消息（见图 3-20）。

![](img/a977a875c7c627b45d939729705a252e_145_1.png)

图 3-20

要抑制该警告消息，可以将 `#pragma warning` 指令与要抑制的消息的警告编号一起使用：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

#pragma warning disable 414
namespace TestDefine
{
    class Program
    {
        int num = 5;
        static void Main(string[] args)
        {
        }
    }
}
```

此示例抑制了警告消息编号 414（“私有字段‘field’已赋值，但其值从未被使用。”）。使用 `#pragma warning` 指令后，编译器将不再显示该警告消息（见图 3-21）。

![](img/a977a875c7c627b45d939729705a252e_146_0.png)

图 3-21

你可以通过用逗号（,）分隔消息编号来抑制多条警告消息，如下所示：

```csharp
#pragma warning disable 414, 3021, 1959
```

### 小结

在本章中，你探讨了 C# 语言的基本语法，并了解了如何使用 Visual Studio 2008 编译和运行一个可用的 C# 应用程序。你检查了 .NET Framework 中可用的不同数据类型，以及如何将一种类型转换为另一种类型。你还了解了执行循环的各种方式，以及可以用来改变程序编译方式的各种预处理指令。

## 类与对象

在 C# 编程中，最重要的话题之一 —— 事实上，.NET 开发的基石 —— 就是类与对象。

类本质上是你用来创建对象的模板。在 C# .NET 编程中，你处理的一切都涉及类和对象。本章假定你已经对面向对象编程有基本的了解。它涵盖：

- 如何定义类
- 如何从类创建对象
- 类中不同类型的成员
- 所有对象的根源 —— System.Object

### 类

你在 .NET 中遇到的一切都基于类。例如，你有一个 Windows 窗体应用程序，其中包含一个名为 Form1 的默认窗体。Form1 本身是一个继承自基类 System.Windows.Forms.Form 的类，该类定义了 Windows 窗体应表现出的基本行为：

```csharp
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace Project1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
    }
}
```

第一部分：C# 基础

在 Form1 类中，你在方法中编写代码。例如，要在加载窗体时显示“Hello World”消息，请在 `Form1_Load()` 方法中添加以下语句：

```csharp
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
    }

    protected override void OnLoad(EventArgs e)
    {
        MessageBox.Show("Hello World!");
    }
}
```

以下各节将引导你了解定义自己的类的基础知识以及类中可以包含的各种成员。

### 定义类

你使用 `class` 关键字来定义类。以下示例是一个名为 `Contact` 的类的定义：

```csharp
public class Contact
{
    public int ID;
    public string FirstName;
    public string LastName;
    public string Email;
}
```

这个 `Contact` 类有四个公共成员 —— `ID`、`FirstName`、`LastName` 和 `Email`。类定义的语法是：

```csharp
<access_modifiers> class Class_Name
{
    //---Fields, properties, methods, and events---
}
```

### 使用分部类

你可以不用 `class` 关键字定义整个类，而是使用 `partial` 关键字将定义拆分为多个类。例如，上一节中定义的 `Contact` 类可以拆分为两个分部类，如下所示：

```csharp
public partial class Contact
{
    public int ID;
    public string Email;
}

public partial class Contact
{
    public string FirstName;
    public string LastName;
}
```

编译应用程序时，C# 编译器会将所有分部类组合在一起，并将它们视为一个类。

### 分部类的用途

使用分部类有几个很好的理由。首先，使用分部类可以让团队中的程序员在不共享同一物理文件的情况下处理类的不同部分。虽然这对于涉及大型类文件的项目很有用，但要注意：一个巨大的类文件可能表明设计存在缺陷，可能需要进行重构。

其次，也是最有说服力的一点，你可以使用分部类将应用程序业务逻辑与设计器生成的代码分离。例如，Visual Studio 2008 为 Windows 窗体生成的代码与你的业务逻辑是分开的。这可以防止开发人员干扰用于用户界面的代码。同时，当你更改用户界面时，也不会丢失对设计器生成代码所做的更改。

### 创建类的实例（对象实例化）

类的作用类似于模板。要做任何有用的事情，你需要使用模板来创建一个实际的对象，以便对其进行操作。从类创建对象的过程称为实例化。

要实例化前面定义的 `Contact` 类，你首先创建一个 `Contact` 类型的变量：

```csharp
Contact contact1;
```

在此阶段，`contact1` 是 `Contact` 类型，但实际上还不包含对象数据。要使其包含对象数据，你需要使用 `new` 关键字创建 `Contact` 类的新实例，这一过程称为对象实例化：

```csharp
contact1 = new Contact();
```

或者，你可以将这两个步骤合并为一个，如下所示：

```csharp
Contact contact1 = new Contact();
```

对象实例化后，你可以设置对象的各个成员。下面是一个示例：

```csharp
contact1.ID = 12;
contact1.FirstName = "Wei-Meng";
contact1.LastName = "Lee";
contact1.Email = "weimenglee@learn2develop.net";
```

你也可以将一个对象赋值给另一个对象，如下所示：

```csharp
Contact contact1 = new Contact();
Contact contact2 = contact1;
```

在这些语句中，`contact2` 和 `contact1` 现在都指向同一个对象。对一个对象所做的任何更改都会反映在另一个对象中，如下例所示：

```csharp
Contact contact1 = new Contact();
Contact contact2 = contact1;

contact1.FirstName = "Wei-Meng";
contact2.FirstName = "Jackson";

//---prints out "Jackson"---
Console.WriteLine(contact1.FirstName);
```

它输出“Jackson”，因为 `contact1` 和 `contact2` 指向同一个对象，当你将“Jackson”赋值给 `contact2` 的 `FirstName` 属性时，`contact1` 的 `FirstName` 属性也会看到“Jackson”。

### 匿名类型（C# 3.0）

C# 3.0 引入了一个新特性，称为匿名类型。匿名类型使你无需正式定义类即可定义数据类型。考虑以下示例：

```csharp
var book1 = new
{
    ISBN = "978-0-470-17661-0",
    Title="Professional Windows Vista Gadgets Programming",
    Author = "Wei-Meng Lee",
    Publisher="Wrox"
};
```

*第 3 章讨论了新的 C# 3.0 关键字 var。*

在这里，`book1` 是一个具有 4 个属性的对象：ISBN、Title、Author 和 Publisher（见图 4-1）。

