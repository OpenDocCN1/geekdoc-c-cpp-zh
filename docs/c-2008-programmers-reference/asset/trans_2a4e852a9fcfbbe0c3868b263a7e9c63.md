

## 第15章：程序集与版本控制

按 F11 步入 CallMathUtil() 函数，并观察到现在已加载 Utils.dll 程序集，同时加载了 MathUtil.netmodule（见图15-18）。

![](img/a977a875c7c627b45d939729705a252e_502_0.png)

图15-18

按几次 F11，从 CallMathUtil() 函数中跳出，直到步入 CallStringUtil()。可以看到 StringUtil.netmodule 现在已加载（见图15-19）。

![](img/a977a875c7c627b45d939729705a252e_502_1.png)

图15-19

此示例证明，程序集中的模块仅在需要时才会加载。另外，部署应用程序时，Utils.dll 程序集和这两个模块必须一起提供。如果运行时缺少任何一个模块，就会遇到运行时错误，如图15-20所示。

![](img/a977a875c7c627b45d939729705a252e_503_0.png)

图15-20

## 理解命名空间与程序集

正如第1章所述，.NET Framework 中的各种类库是使用命名空间来组织的。那么命名空间与程序集有何关系？要理解命名空间与程序集之间的关系，最好看一个示例。

在 Visual Studio 2008 中新建一个类库项目，命名为 ClassLibrary1。在默认的 Class1.cs 中，填入以下内容：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Learn2develop.net
{
    public class Class1
    {
        public void DoSomething()
        {
        }
    }
}
```

注意 Class1 的定义包含在 Learn2develop.net 命名空间内。该类还包含 DoSomething() 方法。

在解决方案资源管理器中右击项目名称，选择“添加”⇒“类”，向项目添加一个新类（见图15-21）。

![](img/a977a875c7c627b45d939729705a252e_504_0.png)

图15-21

使用默认名称 Class2.cs。在新添加的 Class2.cs 中，编写以下代码：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Learn2develop.net
{
    public class Class2
    {
        public void DoSomething()
        {
        }
    }
}
```

Class2 包含在同一个命名空间——Learn2develop.net 中，并且也有一个 DoSomething() 方法。编译 ClassLibrary1 项目，以便在项目的 bin\Debug 文件夹中生成一个程序集——ClassLibrary1.dll。向当前解决方案添加另一个类库项目，并将该项目命名为 ClassLibrary2（见图15-22）。

## 第I部分：C# 基础

![](img/a977a875c7c627b45d939729705a252e_505_0.png)

图15-22

按如下内容填充默认的 Class1.cs：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

```
namespace Learn2develop.net
{
    public class Class3
    {
        public void DoSomething()
        {
        }
    }
}

namespace CoolLabs.net
{
    public class Class5
    {
        public void DoSomething()
        {
        }
    }
}
```

该文件包含两个命名空间——Learn2develop.net 和 CoolLabs.net——每个命名空间都包含一个类和一个方法。

编译 ClassLibrary2 项目，以便在项目的 bin\Debug 文件夹中生成一个程序集——ClassLibrary2.dll。

现在，向当前解决方案添加另一个类库项目，这次使用 Visual Basic 语言。将该项目命名为 ClassLibrary3（见图15-23）。

## 第15章：程序集与版本控制

![](img/a977a875c7c627b45d939729705a252e_506_0.png)

图15-23

在 ClassLibrary3 项目的“属性”页中，将其根命名空间设置为 Learn2develop.net（见图15-24）。

![](img/a977a875c7c627b45d939729705a252e_506_1.png)

图15-24

在默认的 Class1.vb 中，定义 Class4 并为其添加一个方法：

```
Public Class Class4
    Public Sub DoSomething()
    End Sub
End Class
```

## 第I部分：C# 基础

编译 ClassLibrary3 项目，以便在项目的 bin\Debug 文件夹中生成一个程序集——ClassLibrary3.dll。

现在向当前解决方案添加一个新的 Windows 应用程序项目（将其命名为 WindowsApp），以便可以使用已创建的三个程序集（ClassLibrary1.dll、ClassLibrary2.dll 和 ClassLibrary3.dll）。

要使用这三个程序集，需要为它们全部添加引用。由于这些程序集与当前 Windows 项目创建在同一解决方案中，因此可以在“添加引用”对话框的“项目”选项卡中找到它们（见图15-25）。

![](img/a977a875c7c627b45d939729705a252e_507_0.png)

在默认 Form1 的后置代码中，键入 Learn2develop.net 命名空间，IntelliSense 将显示有四个类可用（见图15-26）。

![](img/a977a875c7c627b45d939729705a252e_507_1.png)

尽管这些类位于不同的程序集中，但 IntelliSense 仍能找到它们，因为所有这些类都分组在同一个命名空间中。现在可以按如下方式使用这些类：

```
Learn2develop.net.Class1 c1 = new Learn2develop.net.Class1();
c1.DoSomething();

Learn2develop.net.Class2 c2 = new Learn2develop.net.Class2();
c2.DoSomething();
```

```
Learn2develop.net.Class3 c3 = new Learn2develop.net.Class3();
c3.DoSomething();

Learn2develop.net.Class4 c4 = new Learn2develop.net.Class4();
c4.DoSomething();
```

对于 Class5，需要使用 CoolLabs.net 命名空间。如果不这样做，IntelliSense 将检查所有引用的程序集并建议一个合适的命名空间（见图15-27）。

![](img/a977a875c7c627b45d939729705a252e_508_0.png)

图15-27

可以按如下方式使用 Class5：

```
CoolLabs.net.Class5 c5 = new CoolLabs.net.Class5();
c5.DoSomething();
```

## 命名空间别名

有时你希望指定类的完全限定名，以便代码更易于理解。例如，通常会导入类的命名空间，并像这样使用该类：

```
using CoolLabs.net;
//...
Class5 c5 = Class5();
c5.DoSomething();
```

但是，你可能希望为 Class5 使用完全限定名，以明确 Class5 属于 CoolLabs.net 命名空间。为此，可以像这样重写代码：

```
CoolLabs.net.Class5 c5 = new CoolLabs.net.Class5();
c5.DoSomething();
```

但是 CoolLabs.net 命名空间相当长，可能会使代码显得冗长而笨拙。为了简化编码，可以给命名空间指定一个别名，如下所示：

```
using cl = CoolLabs.net;
//...
cl.Class5 c5 = cl.Class5();
c5.DoSomething();
```

然后，不必使用完整命名空间，只需将 CoolLabs.net 命名空间称为 cl。

总之，此示例表明：

- [ ] 属于特定命名空间的类可以位于不同的程序集中。
- [ ] 一个程序集可以包含一个或多个命名空间。
- [ ] 使用不同语言创建的程序集彼此透明。

## 私有程序集与共享程序集

到目前为止，你看到并创建的所有程序集都是私有程序集——也就是说，它们专门供你的应用程序使用，而不用于其他任何用途。作为私有程序集，它们与可执行文件存储在同一个文件夹中，这使得部署非常容易——不存在其他人拥有另一个程序集覆盖你的特定程序集并因此破坏你的应用程序的风险。

> **DLL 地狱**
> 
> 如果你在 .NET 时代之前编写过程序，无疑听说过（甚至可能经历过）“DLL 地狱”这个说法。假设你在客户的计算机上安装了一个应用程序，一切正常，直到有一天客户打电话说你的应用程序突然停止工作。经排查，你发现客户刚刚下载并安装了另一个供应商的新应用程序。你的应用程序停止工作，是因为应用程序中一直使用的某个库（DLL）已被另一个供应商的应用程序覆盖。并且由于你的应用程序再也找不到它所需的那个特定 DLL，它便停止工作。
> 
> .NET 通过确保每个应用程序都有其所需库的自己的副本，消除了这一噩梦。

但程序集也可以是共享的——也就是说，由计算机上运行的多个应用程序使用。如果共享程序集提供大多数应用程序所需的通用功能，那么它们就很有用。为了防止 DLL 地狱，Microsoft 特别用心确保共享程序集得到良好保护。首先，所有共享程序集都存储在称为全局程序集缓存（GAC）的特殊位置。其次，每个共享程序集都必须具有强名称，以唯一标识自身，从而使其他程序集不会拥有相同的名称。

强名称包含以下内容：

- [ ] 程序集的名称
- [ ] 版本号
- [ ] 公钥
- [ ] 区域性

