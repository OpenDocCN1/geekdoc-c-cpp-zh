
```csharp
Console.WriteLine("The dog is sleeping...");
}
}
class Program
{
    static void Main(string[] args)
    {
        Animal a = new Animal();
        a.Sleep();
        Dog d = new Dog();
        d.Sleep();
        Console.ReadLine();
    }
}
```

清单 2.12 中第一个突出显示的代码片段展示了两个类的定义：基类 **Animal** 及其派生类 Dog。**Animal** 类包含一个方法 **Sleep()**，该方法使用 virtual 关键字声明，并在屏幕上显示消息 **The animal is sleeping...**。**Dog** 类包含一个方法 **Sleep()**，该方法使用 override 关键字声明，并在屏幕上显示消息 **The dog is sleeping...**。在第二个突出显示的代码片段中，我们首先创建了 **Animal** 类的一个对象，并使用该对象调用了 **Sleep()** 方法。此方法调用会调用 **Animal** 类中定义的 **Sleep()** 方法。之后，我们创建了 **Dog** 类的一个对象，并使用该对象调用了 **Sleep()** 方法。此方法调用会调用 **Dog** 类中定义的 **Sleep()** 方法。

- 8. 按键盘上的 **F5** 键运行应用程序。应用程序的输出如图 C#-2.13 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_345_0.png)

图 C#-2.13

本节中，你学习了如何在 C# 中实现多态。下一节将介绍如何使用结构。

## 使用结构

在 C# 中，结构是指用户定义的值类型。它允许你创建与内置类型对象（如 int、double 和 bool）类似的新值类型对象。结构可以包含构造函数、字段、方法和属性。C# 中结构与类的一个主要区别是结构不支持继承。默认情况下，结构的所有成员都是私有的。如果没有为结构的变量赋值，则会自动为该变量分配默认值。

在 C# 中，struct 关键字用于声明结构。定义结构的基本语法如下：

```csharp
[access-modifier] struct <structure-name>
{
    variable-declarations;
    method-declarations;
}
```

在前面的语法中，`struct` 是表示定义结构的关键字，**structure-name** 是正在定义的结构名称。

执行以下步骤来创建和使用结构：

- 1. **启动 Visual Studio 2010。**
- 2. 从菜单栏中**选择“文件”→“新建”→“项目”**。将打开 **“新建项目”** 对话框。
- 3. 在 **“新建项目”** 对话框左窗格的 **“已安装的模板”** 部分中，**选择“Visual C#”→“Windows”**。右窗格中将显示可用于在 Visual C# 中开发 Windows 应用程序的项目模板。
- 4. 从右窗格中**选择“控制台应用程序”**以创建控制台应用程序。
- 5. 在 **“名称”** 文本框中输入应用程序名称 **Structures**（也可在光盘中找到），并在 **“位置”** 框中输入应用程序的适当位置。
- 6. 单击 **“确定”** 按钮关闭 **“新建项目”** 对话框并创建 **Structures** 应用程序。
- 7. 将清单 2.13 中突出显示的代码片段添加到 **Program.cs** 文件中：

### 清单 2.13：创建和使用结构

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Structures
{
    public struct X
    {
        public int a, b, c;
    }
    class Program
    {
        static void Main(string[] args)
        {
            X X1 = new X();
            X1.a = 1;
            X1.b = 2;
            X1.c = 3;
            Console.WriteLine("Data of the X1 object:");
            Console.WriteLine("a = " + X1.a);
            Console.WriteLine("b = " + X1.b);
            Console.WriteLine("c = " + X1.c);
            X X2 = new X();
            Console.WriteLine("Data of the X2 object:");
            Console.WriteLine("a = " + X2.a);
            Console.WriteLine("b = " + X2.b);
            Console.WriteLine("c = " + X2.c);
            Console.ReadLine();
        }
    }
}
```

清单 2.13 中第一个突出显示的代码片段展示了结构 X 的定义。X 结构包含三个 int 类型变量 **a**、**b** 和 **c**。在第二个突出显示的代码片段中，我们创建了 X 结构的一个对象 X1，并分别将值 1、2 和 3 赋给 X1 对象的 **a**、**b** 和 **c** 变量。之后，我们在屏幕上显示了全部三个变量 **a**、**b** 和 **c** 的值。接下来，我们创建了 X 结构的另一个对象 X2，并在屏幕上显示了 X2 对象全部三个变量 **a**、**b** 和 **c** 的值。

- 8. 按键盘上的 **F5** 键运行应用程序。应用程序的输出如图 C#-2.14 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_347_0.png)

图 C#-2.14

你可以在图 C#-2.14 中注意到，X2 对象的全部三个变量都初始化为值 0。讨论结构之后，现在让我们学习匿名类型。

## 使用匿名类型

在应用程序中创建属性时，你可能还需要创建一些只读属性。可以使用匿名类型将这些只读属性封装到单个单元中。匿名类型为你提供了一种简便方法，无需定义新类型即可将一组只读属性封装到单个单元中。匿名类型是未命名的结构类型，可以使用 var 关键字访问。匿名类型声明以 new 关键字开头。

> 创建应用程序时，不能使用匿名类型的名称，因为重新编译应用程序时该名称可能会更改。这是因为匿名类型的名称由编译器生成，并且可能因编译而异。

执行以下步骤来创建和使用匿名类型：

- 1. **启动** Visual Studio 2010。
- 2. 从菜单栏中**选择** **“文件”→“新建”→“项目”**。将打开 **“新建项目”** 对话框。
- 3. 在 **“新建项目”** 对话框左窗格的 **“已安装的模板”** 部分中，**选择** **“Visual C#”→“Windows”**。右窗格中将显示可用于在 Visual C# 中开发 Windows 应用程序的项目模板。
- 4. 从右窗格中**选择** **“控制台应用程序”**以创建控制台应用程序。
- 5. 在 **“名称”** 文本框中输入应用程序名称 **AnonymousTypes**（也可在光盘中找到），并在 **“位置”** 框中输入应用程序的适当位置。
- 6. 单击 **“确定”** 按钮关闭 **“新建项目”** 对话框并创建 **AnonymousTypes** 应用程序。
- 7. **添加**清单 2.14 中突出显示的代码片段到 **Program.cs** 文件中。

### 清单 2.14：创建和使用匿名类型

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace AnonymousTypes
{
    class Program
    {
        static void Main(string[] args)
        {
            var product = new { Name = "Keyboard", Price = 15 };
            Console.WriteLine("Product details");
            Console.WriteLine("Name: " + product.Name);
            Console.WriteLine("Price: " + product.Price);
            Console.ReadLine();
        }
    }
}
```

在清单 2.14 的突出显示代码片段中，我们首先创建了匿名类型的一个对象 product，该对象具有两个属性 **Name** 和 **Price**。接下来，我们为 product 对象的 **Name** 和 **Price** 属性赋值。之后，我们在屏幕上显示了 product 对象 **Name** 和 **Price** 属性的值。

- 8. 按键盘上的 **F5** 键运行应用程序。应用程序的输出如图 C#-2.15 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_348_0.png)

图 C#-2.15

你已经学习了匿名类型。下一节将学习 C# 中的命名空间。

## 使用命名空间

命名空间的概念对 C# 来说并不新鲜。命名空间充当一个或多个结构元素的包装器，使这些元素唯一。换句话说，命名空间是一种将相关类型分组到一个名称下的方式。无论是否在源文件中显式声明命名空间，C# 编译器都会向源文件添加默认命名空间。

C# 中的命名空间可以分为两类：

- **用户定义：** 指代码中定义的命名空间。
- **系统定义：** 指 .NET Framework 基类库中定义的命名空间，例如 System、System.Collections 和 System.Data。

在 C# 中，可以使用 **using** 关键字在程序中包含命名空间。

> 命名空间始终是公共的；因此，命名空间的声明不能包含任何访问修饰符。

现在，让我们执行以下步骤在控制台应用程序中引用命名空间：

- 1. **启动** Visual Studio 2010。
- 2. 通过从菜单栏中选择 **“文件”→“打开”→“项目/解决方案”** 选项，**打开** AnonymousTypes 应用程序。
- 3. **右键单击** **解决方案资源管理器**中的 **“引用”** 节点，并从上下文菜单中选择 **“添加引用”** 选项，如图 C#-2.16 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_348_1.png)

图 C#-2.16

将打开“添加引用”对话框（图 C#-2.17）。

- 4. 在 **“添加引用”** 对话框上**选择**一个选项卡，以从中将命名空间的引用添加到程序中。在本例中，我们选择了 **.NET** 选项卡，因为我们要添加 .NET Framework 基类库中定义的命名空间的引用（图 C#-2.17）。

