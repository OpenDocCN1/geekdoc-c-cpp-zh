
在本节中，您了解了垃圾回收机制以及如何在应用程序中强制回收任何未使用的资源。现在，让我们在下一节学习 IDisposable 接口。

## IDisposable 接口

.NET 应用程序中的垃圾回收本质上是非确定性的。这意味着无法预测 GC 何时会执行垃圾回收。因此，对于内存需求较大的应用程序，需要显式强制执行垃圾回收。在这种情况下，建议实现 IDisposable 接口。该接口定义了一个释放已分配未管理资源的方法，因为 GC 对未管理资源（如打开的文件和流）没有任何了解。IDisposable 接口定义了 Dispose() 方法，该方法负责释放托管资源以及未托管资源。Dispose() 方法与 GC 一起使用。

> **注意**
> *当您实现 IDisposable 接口时，请使用 try ... catch ... finally 块，以确保即使出现任何异常，未管理的资源也会被释放。未管理的资源是指未包含在 .NET Framework 中的任何内容，例如操作系统资源，其中包括文本文件或窗口。网络或数据库连接也是未管理资源的示例。*

接下来，让我们学习用于释放 .NET 应用程序对象拥有的任何资源的方法。

## Dispose 和 Close 方法

Dispose() 方法在 IDisposable 接口内部定义，用于释放任何未管理的资源。这是释放分配给对象或为对象重用做准备的资源的首选方法。让我们考虑清单 4.10，其中定义了 Dispose() 方法：

### 清单 4.10：定义 Dispose() 方法

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace ReleasingObject
{
    class Program : IDisposable
    // class Program implements the IDisposable interface
    {
        // calling the Dispose() method
        public void Dispose()
        {
            // some code
            Console.WriteLine("Outside the Dispose() method!");
        }
    }
}
```

在清单 4.10 中，Program 类实现了 IDisposable 接口，其中包含 Dispose() 方法。您可以在 Dispose() 方法内部添加代码以执行任何清理操作。

在 .NET Framework 中，还有另一种释放资源的方法，称为 Close() 方法。Close() 方法用于临时关闭任何托管资源，例如数据库连接。这意味着您已调用 Close() 方法的特定资源可以重新打开。然而，Dispose() 方法会永久从内存中移除未管理的资源，并且该资源不可用于任何进一步处理。

## 使用部分类

C# 中的部分类是使您能够在两个或多个源文件中指定类定义的类。所有源文件都包含类定义的一部分。不同源文件中的定义在应用程序执行时合并。您可以将部分类分布在多个单独的文件中，以便您可以使用一个部分类同时处理单独的文件。

您可以使用 partial 关键字声明部分类。partial 关键字表示必须在编译时提供类的所有部分才能生成最终类型。

让我们执行以下步骤创建一个名为 PartialClass 的应用程序以学习如何使用部分类：

- 1. 重复本章 Defining a Method 部分中创建 CreatingMethod 应用程序时讨论的步骤 1 到 3。
- 2. 在 Name 文本框中输入 PartialClass 以指定应用程序的名称，并在 Location 组合框中指定应用程序的适当位置
- 3. 单击 OK 按钮。PartialClass 应用程序已创建。
- 4. 在 Program.cs 文件中，添加清单 4.11 中给出的突出显示的代码：

### 清单 4.11：使用部分类

```csharp
namespace PartialClass
{
    public partial class Orders
    {
        private int x;
        private int y;
        public Orders(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }
    public partial class Orders
    {
        public void PrintOrders()
        {
            Console.WriteLine("Orders: {0}, {1}", x, y);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Orders ord = new Orders(20, 60);
            ord.PrintOrders();
            Console.ReadLine();
        }
    }
}
```

在清单 4.11 中，Orders 类的字段和构造函数在一种部分类定义中声明，而 PrintOrders() 方法在另一种部分类定义中声明。

- 5. 按 F5 键运行 PartialClass 应用程序。

应用程序的输出显示如下 Fig.C4-4.9 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_119_0.png)

### 图 C4-4.9

图 C4-4.9 显示所有部分类被编译为单个类然后执行。在下一节中，您将了解静态类。

## 使用静态类

C# 中的静态类与非静态类相同；然而，与非静态类不同，它不能被实例化。换句话说，这意味着当您将类声明为 static 时，就不能使用 new 关键字创建该类的对象。C# 中的静态类可用于创建数据成员和函数，即使您未创建该类的任何对象也可以访问。您可以使用类名本身访问静态类的成员。static 关键字用于将类及其成员定义为静态。

静态类不包含用于创建和初始化实例的实例构造函数。静态类的特性如下：

- 静态类只能包含静态成员
- 静态类不能被实例化
- 静态类是密封的
- 您不能继承静态类

现在让我们学习如何声明静态类并在类中使用静态方法。

## 声明静态类

当您在 C# 应用程序中声明静态类时，必须考虑静态类不能被实例化的基本规则。声明静态类类似于创建仅包含静态成员和私有构造函数的类。以下代码片段显示了如何声明静态类：

```csharp
static class Employee
{
    public static int id;
    public static int tele_no;
}
```

在前面的代码片段中，Employee 是静态类，id 和 tele_no 是其静态数据成员。如果一个类是静态的，其成员也是静态的。

## 在类中使用静态方法

您可以在声明静态方法的类内调用静态方法，而无需创建该类的实例。如果您创建了该类的实例，就不能使用它来调用静态成员。静态成员可以存在于静态或非静态类内部。

让我们执行以下步骤创建一个名为 StaticMethod 的应用程序以学习如何在类中使用静态方法：

- 1. 重复本章 Defining a Method 部分中创建 CreatingMethod 应用程序时讨论的步骤 1 到 3。
- 2. 在 Name 文本框中输入 StaticMethod 以指定应用程序的名称，并在 Location 组合框中指定应用程序的适当位置。
- 3. 单击 OK 按钮。StaticMethod 应用程序已创建。
- 4. 在 Program.cs 文件中，添加清单 4.12 中给出的突出显示的代码：

### 清单 4.12：显示在类中添加静态方法的代码

```csharp
namespace StaticMethod
{
    static class MathFunction
    {
        static public double square(double num)
        {
```
