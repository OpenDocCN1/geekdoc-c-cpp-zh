
在前面的代码片段中，`XYZCorporation` 是一个命名类 `Corp` 和枚举的命名空间。如果公司使用来自另一个供应商的第三方软件，其在程序中实现了相同的类名，命名空间允许开发者解析现有的代码。这可以通过完成命名约定（例如 `namespace.classname`）来实现。

你编写的所有代码都存在于代码当前上下文隐式命名空间中。或者，通过 C# 中的 `using` 语句使用关键字包含标记，你可以告诉编译器在系统中使用哪些命名空间和代码库。关键字最常用的用法是在程序中使用 `System` 命名空间，这样你就可以使用 `System` 命名空间的大部分常用功能。要使用 `System` 命名空间，你可以编写以下代码片段：

```csharp
using System {
    // 调用 System 命名空间中的 Console 类
    Console.WriteLine("Hello world!");
}
```

或者你可以编写以下代码片段：

```csharp
System.Console.WriteLine("Hello world!");
```

前面代码片段中显示的方法是等价的，并调用 `Console` 类的 `WriteLine` 方法。通常，每当你想在程序中使用包含它的类时，都需要添加命名空间。但是，如果已经在代码顶部使用关键字指定了命名空间，你就不需要在代码的每个实例中指定它。

在嵌套命名空间或具有某些公共方法的命名情况下，你可以为命名空间创建别名。假设你的公司坚持使用三级命名空间——`Corporation`、`Dept`、

## 第 4 章：命名空间、类、对象和结构体

以及项目——封装在你创建的每个类周围。下面的代码片段显示了这些命名空间使用的层级：

```
namespace Corporation {
namespace Dept {
namespace Project {
class InternalClass {
}
}
}
```

你可以看到，我们还创建了 `InternalClass` 类。你需要使用以下代码片段中的语法在你的程序中引用 `InternalClass` 类：

`Corporation.Dept.Project.InternalClass`

输入上述代码片段显示出你使用 `InternalClass` 类的方法是复杂且耗费时间的，因为 C# 提供了另一种可选方案，允许你为 `Corporation.Dept.Project` 命名空间指定别名，如下代码片段所示：

`using DCN=Corporation.Dept.Project;`

现在，在使用别名后，你可以通过以下代码片段访问程序中为创建别名指定的指定命名空间的成员：

`DCN.InternalClass` 是 `Corporation.Dept.Project` 命名空间的别名。上述代码片段显示了如何在程序中使用别名 `DCN` 代替 `Corporation.Dept.Project` 命名空间：

```csharp
using System;
using DCN = Corporation.Dept.Project;
namespace Corporation {
namespace Dept {
namespace Project {
class InternalClass {
public static void Display() {
Console.WriteLine("Hello world");
}
}
}
}
}
public class Main {
public static void Main() {
DCN.InternalClass.Display();
}
}
```

在上述代码片段中使用别名的技术减少了代码的复杂性，并最大限度地减少了输入完整命名空间花费的时间。

以下是 .NET 类库提供的一些常用命名空间：

- `System`——包括本质类和基类，这些类定义了常用的数据类型、事件、事件处理程序、属性和异常。
- `System.Collections`——包括定义各种对象集合的接口和类，包括列表、队列、数组、哈希表和字典。
- `System.Data`——包括构成 ADO.NET 的类，允许你构建数据处理组件，以管理来自多个分布式数据源的数据。

### 深入

- `System.Data.OleDb`——包括支持 OLE DB .NET 数据提供程序的类。
- `System.Data.SqlClient`——包括支持 SQL Server .NET 数据提供程序的类。
- `System.Data.OracleClient`——包括实现 Oracle 数据提供程序的类。
- `System.Data.Odbc`——包括实现开放数据库连接 `ODBC` 数据提供程序的类。
- `System.Diagnostics`——包括允许你调试应用程序并在调试时逐行代码的类。它还包括启动进程、在事件日志中读写以及监控系统性能的方法。
- `System.Drawing`——提供对 GDI+ 图形的访问。`System.Drawing.Drawing2D`、`System.Drawing.Imaging` 和 `System.Drawing.Text` 命名空间提供了额外功能。
- `System.Drawing.Drawing2D`——包括支持高级二维和矢量图形的类。
- `System.Drawing.Imaging`——包括支持高级 GDI+ 的类。
- `System.Drawing.Printing`——包括支持应用程序打印服务的类。
- `System.Text`——包括支持高级 GDI 排操作类。此命名空间中的类允许用户创建和使用字体集合。
- `System.Globalization`——包括支持文化信息的类，包括语言/区域、日历、日期格式、货币和数字。
- `System.IO`——为许多互联网上使用的协议提供简单的编程接口。
- `System.Net.Sockets`——包括支持 Windows Socket 接口的类。如果你工作过 Winsock API，你将可以使用 `Socket` 类开发应用程序。
- `System.Reflection`——包括关于类型、方法和字段的信息以及返回信息。`System.Reflection` 命名空间具有动态创建和调用类型的能力。
- `System.Runtime.Remoting`——包括支持远程调用的类和接口。
- `System.Security`——包括支持公共语言运行时 `CLR` 安全性的类。
- `System.Serialization`——包括将对象或图转换为字节序列的类。反序列化是从该位置重建对象的过程。
- `System.Threading`——包括支持服务器通信的类，例如 `HttpRequest` 类提供请求；`HttpResponse` 类管理输出；`HttpUtility` 类提供工具。
- `System.Web.Security`——包括实现 ASP.NET 安全的类。
- `System.Web.Services`——包括构建 Web 服务的类，这些是可编程的实体。
- `System.Windows.Forms`——包括创建 Windows 表单的类。
- `System.Xml`——包括处理 XML 的类。

在讨论之后，我们现在讨论类。

## 第 4 章：命名空间、类、对象和结构体

### 探索类和对象

类允许你控制一组数据。类还赋予了运行环境的能力。假设你在程序中创建一个名为 `student` 的类对象。为了这样做，你首先需要创建一个包含功能的类。在本节中，你将探索：

- 类的语法
- 方法作为类成员
- 访问修符
- 使用对象访问类
- 构造函数和析构函数
- 静态类以及静态成员、索引器

#### 类的语法

让我们从类的语法开始。

类的基本结构如下代码所示：

```csharp
class <classname> {
    <access-modifier> [static] <return-type> Methodname(<signature>);
    <access-modifier> [static] <variable type> variablename;
}
```

声明对象的基本语法如下代码所示：

`<classname> object = new <classname>();`

你可以在应用程序中声明类。部分类允许你在两个或多个文件中指定类、结构或接口的定义。包含类定义的所有源文件在编译时会合并。当开发者处理大型项目时，可能需要部分类。使用 `partial` 关键字，你可以将类声明为部分类，如下代码所示：

```csharp
public partial class student {
    public void avgmarks() { }
}
public partial class student {
    public void calRank() { }
}
```

`partial` 关键字指定了类、结构或接口的哪些属于命名空间。

#### 方法作为类成员

现在你已经熟悉了类的重要性，让我们继续讨论类的成员——类方法和类变量。类的成员是定义在类中的元素。

### 深度解析

在前面的代码段中，`Square` 类有一个名为 `side` 的变量和一个名为 `area` 的方法。`side` 变量接收一个整数值作为正方形的边长；而 `area` 方法用于计算正方形的面积。

构造函数和析构函数是特殊的，并且默认存在于每个类中。构造函数在访问类时初始化所有类成员。析构函数在不再需要时销毁所有对象以节省内存。任何类的这两个特殊方法在类实例创建或销毁时都会自动调用。

类变量也被称为数据成员 `data members`，方法也被称为函数 `functions` 或方法 `methods`。你可以使用参数向方法传递值。传递参数的语法如下面的代码所示：

```
[modifiers] DataTypeName
```

C# 5.0 具有以下类型的参数：

- 值参数 `Value parameter`——允许通过方法给出的参数为值赋值。这种类型的赋值仅影响本地存储位置，对方法中被赋值的实际参数没有影响。此外，对参数的更改仅在方法内部；不会传递给调用方法。值参数是默认参数。如果你在不使用任何修饰符的情况下声明一个参数，它就是一个值参数。值参数也被称为 `in` 参数。
- 引用参数 `Reference parameter`——它不包含数据，而是携带数据的引用。使用 `ref` 修饰符声明的参数是引用参数。
- 输出参数 `Output parameter`——代表相同的存储位置，而不是为方法中作为参数提供的变量创建新的存储位置。使用 `out` 修饰符声明的参数是输出参数。输出参数在传递给函数之前不需要初始化。输出参数通常用于产生多个返回值的方法。

在定义和调用方法时使用 `out` 修饰符的示例如下代码所示：

```sharp
class {
    static void FirstMethod(out int x) // 方法定义中的修饰符
    {
        x = 81;
    }

    static void Main()
    {
        int y; // 无预先初始化
        FirstMethod(out y); // 方法调用中的修饰符
        // y 的值为 81
    }
}
```

在前面的代码段中，`out` 修饰符在方法定义期间已指定 `static void FirstMethod(out int x)`，以及在方法调用期间 `FirstMethod(out y)`。

在方法定义和方法调用中使用 `ref` 修饰符的示例如下代码所示：

```sharp
class UsingRef
{
    static void secondMethod(ref int x) // 方法定义中的修饰符
    {
        x++;
    }

    static void Main()
    {
        int y = 81; // 必须初始化
        SecondMethod(ref y); // 方法调用中的 ref 修饰符
        Console.WriteLine("Value of y is " + y);
    }
}
```

## 第 4 章：命名空间、类、对象和结构体

在前面的代码段中，你需要初始化变量，但输出参数在被传递之前不需要预先初始化。然而，在方法返回之前，你必须为输出参数分配某些值。当方法返回多个值时，优选输出参数。C++ 不返回多个值，你只能通过编程技巧来实现这一点；而 C# 的 `out` 修饰符允许多个返回值。

- 参数数组 `Parameter array`——允许程序员向方法的成员传递任意数量的参数。参数数组是数组的数组，使用 `params` 修饰符声明。参数数组可以是单维数组或多维数组。如果你传递一个单维数组，该参数的作用就像一个普通值。如果参数列表中包含参数数组，它必须是单维数组并且应该是列表中的最后一个参数。换句话说，它位于参数列表的末尾。无法将带有 `ref` 和 `out` 修饰符的参数结合。

#### 访问修饰符 `Access Modifiers`

访问修饰符有助于避免数据和方法与现有代码合并，并保护对象不受类外部的访问。这些修饰符通过定义特定的访问范围来以受限的方式访问数据和方法来实现这一点。然而，每个方法只能包含一个修饰符。如果你声明的类不在任何其他类内部，那么该类可以使用以下任何一种修饰符：

- `public` 修饰符
- `internal` 修饰符

另一方面：

- `public` 修饰符——允许对类内部和外部的成员进行无限制公共访问。
- `internal` 修饰符——允许内部访问成员。只有当前程序集 `assembly` 可以访问这些成员。如果在定义该成员的程序集外部访问 `internal` 访问级别的成员，则会产生错误。
- `protected` 修饰符——允许对成员进行保护访问。你可以从声明它们的类或从该类的派生类访问保护成员。
- `private` 修饰符——允许对成员进行私有访问。私有成员具有最低的访问权限；你可以在类体内部或声明它们的结构中访问它们。
- `protected internal` 修饰符——允许访问当前程序集、包含类以及来自包含类的派生类的成员。

#### 对象 `Objects`

在 C# 中，对象帮助你使用点 `.` 操作符访问类的成员 `字段、方法和属性`。考虑以下示例说明如何通过对象访问类成员：

```csharp
static void Main(string[] args)
{
    Amount Amt = new Amount();

    Amt.TotalAmount=12000;
    Amt.Deductions=2000;

    Amt.Balance();
    Amt.GetData();
}
public class Amount
{
    double TotalAmount, Deductions;
    public void Balance();
}
```

### 深度解析

```csharp
public class Amount
{
    double TotalAmount, Deductions;
    public void Balance()
    {
        // 方法体
    }
    public void Debit()
    {
        // 方法体
    }
    public void Credit()
    {
        // 方法体
    }
    public void getData()
    {
        Debit();
        Credit();
    }
}
```

在前面的代码段中，`Amount` 对象通过点 `.` 操作符访问数据成员 `TotalAmount`, `Deductions` 以及方法 `Balance` 和 `GetData`。

在某些情况下，程序员需要确保某些值在生命周期内保持不变。例如，在计算任何化学公式时，元素的数值应该保持不变。C# 有两种类型——常量 `Const` 和只读 `Read-Only` 来处理这种情况。常量和只读有相似之处，但也有不同之处。

常量与编译时对应的类相关。这意味着你定义的值是在编译时计算的。常量一旦声明就无法更改。你可以使用 `const` 关键字声明变量。

以下代码段显示了使用：

```csharp
struct atomweight {
  public const double gold = 196.9;
  public const double silver = 107.8;
}
```

在前面的代码段中，金 `196.9` 和银 `107.8` 的原子量是编译时常量，因为它们的值始终相同，不会在运行时更改。

如所述，常量通常在编译时声明；但如果你想让变量在运行时变为常量，可以在下面的代码段中使用 `readonly` 关键字：

```csharp
classClass
  public readonly int Number10;
  public readonly int Number20;
}
```

在前面的代码段中，`Number10` 和 `Number20` 的值分别设置为 10 和 20。

只读字段与类或类的实例相关。它们的值可以在类声明期间设置。你可以使用 `readonly` 关键字将变量声明为只读。在希望同一类的不同对象具有不同值，且字段值在特定对象的整个寿命期间保持不变的情况下，只读变量优于常量。

#### 构造函数和析构函数

如果你用过 C++ 或 Java，你习惯构造函数和析构函数的概念。构造函数在对象首次创建时被调用。析构函数 `或终结器` 在对象销毁和垃圾回收时被调用。构造函数的名称与类名相同；而析构函数的名称由类名加上波浪号 `~` 组成。你可以使用构造函数来

# 第4章：命名空间、类、对象和结构体

初始化对象并设置任何参数。此外，你还可以编写构造函数来接受参数。下面的代码片段了一个名为 `Foo` 的类的构造函数和析构函数的示例：
