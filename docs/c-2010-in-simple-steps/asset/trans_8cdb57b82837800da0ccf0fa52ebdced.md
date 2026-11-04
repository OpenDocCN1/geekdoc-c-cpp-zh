
```
}
}
}
```

在清单 4.18 中，所有类成员都是可访问的，除了私有成员。私有成员只能在其声明的类中访问。为了在 MyClass 类中实现封装，使用 private 关键字声明数据成员，即 x、y 和 z。

按 F5 键运行 EncapsulationExample 应用程序。

应用程序的输出显示如下，如图 C#4.16 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_130_0.png)

图 C#4.16

接下来，让我们讨论 C# 中的继承。

## 实现继承

使用 OOP 在 .NET 应用程序中最重要的原因是促进代码的重用并消除代码的冗余。为了确保可重用性，OOP 语言提倡使用继承。继承被定义为子类获得其父类中定义的所有特征的属性。与子相比，父类在类层次结构中处于更高级别。例如，如果我们将鹦鹉类视为子，则它从父类，即鸟类获得其特征。

当一个类继承另一个类的公共属性时，继承属性的类称为派生类，而允许其公共属性被继承的类称为基类。OOP 中的继承有四种类型：

- 单继承：指继承类型中有一个基类和一个派生类
- 层级继承：指继承类型中一个基类被多个派生类继承
- 多层继承：指继承类型中一个类派生自一个类，而该类又派生自另一个类
- 多重继承：指继承类型中一个派生类继承多个基类

C# 支持单继承、层级继承和多层继承。在 C# 中，不能通过在单个派生类中直接从多个基类继承来实现多重继承，而是使用接口。

### 注意

> 接口是数据成员和成员函数的集合。你将在本章后面详细了解接口。

继承代表 C# 中两种类之间的一种关系。让我们通过一个示例来理解。假设有两个类名为 Class A 和 Class B，且 Class B 派生自 Class A，如图 C#4.17 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_130_1.png)

图 C#4.17

让我们执行以下步骤创建一个名为 AccessingMembers 的应用程序，以学习如何访问基类成员：

1. 重复本章 Defining a Method 部分中创建 CreatingMethod 应用程序时讨论的步骤 1 到 3。
2. 在 Name 文本框中输入 AccessingMembers 以指定应用程序的名称，并在 Location 下拉组合框中指定应用程序的适当位置。
3. 单击 OK 按钮。AccessingMembers 应用程序已创建。
4. 在 Program.cs 文件中，添加清单 4.19 中给出的高亮代码：

### 清单 4.19：访问基类成员

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace AccessingMembers
{
    public class BaseClass
    {
        public void BaseClassMethod()
        {
            Console.WriteLine("I am a Base Class Method()");
        }
    }
    public class DerivedClass : BaseClass
    {
        public void DerivedClassMethod()
        {
            Console.WriteLine("I am a Derived Class Method()");
            base.BaseClassMethod();
        }
    }
    public class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("I am accessing Base Class Object:");
            BaseClass bc = new BaseClass();
            bc.BaseClassMethod();
            Console.WriteLine("");
            Console.WriteLine("I am accessing Derived Class Object:");
            DerivedClass dc = new DerivedClass();
            dc.DerivedClassMethod();
            Console.WriteLine("\nPRESS ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

在清单 4.19 中，BaseClass 是父类，DerivedClass 是派生类。DerivedClass 类继承了 BaseClass 类的特性，因此是 BaseClass 类的子类。

5. 按 F5 键运行 AccessingMembers 应用程序。

应用程序的输出显示如下，如图 C#4.18 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_133_0.png)

在本节中，你学习了如何通过派生类访问基类的成员。在下一节中，你将学习如何使用抽象类。

## 使用抽象类

不能实例化对象的类称为抽象类。如果创建了基类并且希望确保以后不会创建基类的对象，可以将基类设为抽象类。类中的 abstract 关键字表示该类不能被实例化并且是抽象类。

抽象类的一些特征如下：

- 不能直接实例化。这意味着你不能创建抽象类的对象；它必须被继承。
- 包含抽象成员和非抽象成员。
- 你必须在抽象类中声明至少一个抽象方法。
- 总是用 public 访问修饰符声明。

抽象类的基本目的是提供可被多个派生类共享的基类的通用定义。

让我们执行以下步骤创建一个名为 AbstractClass 的应用程序，以学习如何使用抽象类：

1. 重复本章 Defining a Method 部分中创建 CreatingMethod 应用程序时讨论的步骤 1 到 3。
2. 在 Name 文本框中输入 AbstractClass 以指定应用程序的名称，并在 Location 下拉组合框中指定应用程序的适当位置。
3. 单击 OK 按钮。AbstractClass 应用程序已创建。
4. 在 Program.cs 文件中，添加清单 4.20 中给出的高亮代码：

### 清单 4.20：访问抽象类

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace AbstractClass
{
    abstract class absClass
    {
        public int Add(int Num1, int Num2)
        {
            return Num1 + Num2;
        }
        public int Multiply(int Num1, int Num2)
        {
            return Num1 * Num2;
        }
    }
}
```

当你执行前面的语句时，你将收到错误消息：DerivedClass 无法从密封类 MyClass 继承。这是因为 MyClass 基类被声明为密封类。现在，让我们在下一节学习多态。

## 实现多态

一般来说，多态可以解释为一个实体包含多种形式。在 C# 中，你可以借助多态以多种方式使用一个过程。例如，假设你需要编写一个计算某些几何图形面积的程序。你可以使用相同的方法名，通过不同的参数计算圆、三角形或矩形的面积。

多态的重要特征如下：

- 允许你在运行时通过基类引用调用派生类的方法
- 有助于实现通过相同名称调用的多个方法的不同实现。
- 有助于调用类的方法，而不考虑其提供的具体实现。

在 C# 中，实现多态有两种方式：

- 编译时多态
- 运行时多态

让我们在下一节详细了解它们。

### 实现编译时多态

当编译器编译程序时，编译器拥有关于方法参数的信息。因此，编译器在编译时本身就将适当的方法绑定到相应的对象。此过程称为编译时多态或早期绑定。你可以通过重载方法和运算符来实现编译时多态。传递的参数在数量、类型和顺序方面进行匹配；然后调用重载方法。

编译时多态分为以下几类：

- 方法重载
- 运算符重载

### 方法重载

方法重载是一个概念，其中方法根据传递给它的参数的数量和类型而表现。方法重载允许你使用相同的名称定义多个方法，但具有不同的签名。当你调用重载方法时，编译器会根据方法调用中指定的签名自动确定应使用哪个方法。

### 注意

> 如前所述，方法签名是方法名称与参数的数量和类型的组合。

让我们执行以下步骤创建一个名为 MethodOverloading 的应用程序，以学习如何重载方法：

1. 重复本章 Defining a Method 部分中创建 CreatingMethod 应用程序时讨论的步骤 1 到 3。
2. 在 Name 文本框中输入 MethodOverloading 以指定应用程序的名称，并在 Location 下拉组合框中指定应用程序的适当位置。
3. 单击 OK 按钮。MethodOverloading 应用程序已创建。
