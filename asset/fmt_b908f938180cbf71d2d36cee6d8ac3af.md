
如果你在这个阶段尝试运行程序，你将得到一个错误，说 `Member` 不包含 `CalculateAnnualFee` 的定义。这是因为 `clubMembers` 被声明为 `Member` 类型的数组。因此，当我们编写 `m.CalculateAnnualFee()` 时，编译器尝试执行 `Member` 类中的 `CalculateAnnualFee()` 方法。出现错误的原因是我们的 `Member` 父类中没有这样的方法；它只在两个子类中。为了纠正这个错误，我们必须向我们的父类中添加以下方法。

```csharp
public virtual void CalculateAnnualFee()
```

```csharp
{
  annualFee = 0;
}
```

现在运行程序并注意每个成员的“年度总费用”（Total Annual Fee）。你发现了什么？它们应该都显示为 $0。这意味着被调用的 `CalculateAnnualFee()` 方法是父类中的那。这并不意外，因为 `clubMembers` 被声明为 `Member` 类型。

如果你想调用子方法，你需要进行两处更改。

首先，你需要将父方法声明为 `virtual`，如下：

```csharp
public virtual void CalculateAnnualFee()
{
  annualFee = 0;
}
```

`virtual` 关键字告诉编译器该方法可以在派生类中重写。当编译器遇到这个关键字时，它会在派生类中寻找相同的方法并执行该方法。

接下来，在派生类中，你必须使用 `override` 关键字声明你的方法重写了父类中的方法，如下：

```csharp
// 在 VIPMember 子类中
public override void CalculateAnnualFee()
{
  annualFee = 1200;
}
```

```csharp
// 在 NormalMember 子类中
public override void CalculateAnnualFee()
{
  annualFee = 100 + 12 * 30;
}
```

现在如果你再次运行程序，前三个成员（`NormalMember`）和后两个成员（`VIPMember`）的年度费用分别为 $460 和 $1200。

这就是多态的结果。在运行时（即程序运行期间），程序确定 `clubMembers` 的前三个成员是 `NormalMember` 类型，并执行该类中的 `CalculateAnnualFee()` 方法。它还确定后两个成员是 `VIPMember` 类型，并执行该类的方法。

多态简单来说意味着在运行时，程序足够智能，即使该对象被声明为 `Member` 类型，它也能使用正确子类中的 `CalculateAnnualFee()` 方法。

我们说 `clubMembers` 的前三个元素的运行时类型是 `NormalMember`，而后两个元素的运行时类型是 `VIPMember`。所有 5 个元素的声明类型都是 `Member`。

## GetType() 和 typeof()

在之前的示例中，我们让程序来确定 `clubMembers` 数组中每个成员的运行时类型并调用 `CalculateAnnualFee()` 方法。然而，有时我们可能需要在编写代码时自己确定每个单独成员的运行时类型。我们将在项目的后部分看到相关的示例。

下面的 `if` 语句展示了你如何在运行时确定 `clubMember` 数组的第一个元素是否为 `VIPMember` 类型：

```csharp
if (clubMembers[0].GetType() == typeof(VIPMember))
    Console.WriteLine("Yes");
else
    Console.WriteLine("No");
```

`GetType()` 方法返回对象的运行时类型。

`typeof()` 方法接收一个数据类型的名称（例如 `int`、`float` 或类的名称）并返回该类型，然后我们可以将其结果与左侧 `GetType()` 方法的结果进行比较。

如果你运行上面的代码，你将得到输出“No”，因为 `clubMembers[0]` 不是 `VIPMember` 类型。

## 抽象类和方法类和 Methods

既然我们已经熟悉了继承（以及多态），让我们继续讨论 C# 中两种特殊的“父类”类型——抽象类和接口。

首先，让我们来看抽象类。

抽象类是一种特殊的类，其创建的完全是为了作为基类供其他类派生。它们不能被实例化。换句话说，如果 `FourWheelVehicles` 是一个抽象类，语句

```csharp
FourWheelVehicle myVeh = new FourWheelVehicle();
```

将给你一个错误，因为你不能创建一个抽象类的对象。

抽象类可以拥有字段、属性和方法，就像其他类一样。然而，它们不能拥有静态成员。此外，抽象类可以具有特殊类型的方法，称为抽象方法。抽象方法是没有体的方法，并且**必须**在派生类中实现。它们只能存在于抽象类中。在某种程度上，抽象方法就像一份合同。如果你想确保任何继承该类的类都实现某个方法，你可以将类声明为抽象类，并将该方法声明为抽象方法。

要声明抽象类，只需在 `class` 关键字之前添加 `abstract` 关键字如下：

```csharp
abstract class Class
```

在抽象类内部声明抽象方法，在返回类型之前添加 `abstract` 关键字，如下：

```csharp
abstract void AbstractMethod();
```

由于抽象方法没有体，我们用分号（;）结束声明。要在派生类中实现抽象方法，我们使用 `override` 关键字，如下：

```csharp
class Class
{
    public override void AbstractMethod();
}
```

下面的代码展示了一个抽象类的示例。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace Abstract
{
    class Program
    {
        static void Main(string[] args)
        {
            AbstractClass a = new AbstractClass();
            a.PrintMessage();
        }
    }
    abstract class AbstractClass
    {
        protected string message = "Hello C!";
        public abstract void PrintMessage();
    }
    class AbstractClass : AbstractClass // 注意：此处原文代码类名冲突，保持原样翻译
    {
        public override void PrintMessage()
        {
            Console.WriteLine(message);
        }
    }
}
```

## Interfaces

接下来，让我们来看接口。接口与抽象类的相似之处在于它们不能被实例化。然而，接口比抽象类更具概念性。它们不能包含字段，但可以包含属性。

抽象类和接口之间的关键区别之一是，类只能继承一个抽象类，但可以实现多个接口。我们 own不会展示多个接口的示例，因为那超出了本书的范围。

接口的名称通常以字母 `I` 开头。接口中的所有属性和方法都是公共的，因此不需要为它们添加任何修饰符。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace Interface
{
    class Program
    {
        static void Main(string[] args)
        {
            InterfaceA a = new ClassA();
            a.MyNumber = 5;
            a.InterfaceMethod();
        }
    }
    interface IShape
    {
        int MyNumber
        {
            get;
            set;
        }
        void InterfaceMethod();
    }
    class ClassA : IShape
    {
        private int myNumber;
        public int MyNumber
        {
            get
            {
                return myNumber;
            }
            set
            {
                if (value < 0)
                    myNumber = 0;
                else
                    myNumber = value;
            }
        }
        public void InterfaceMethod()
        {
            Console.WriteLine("The number is {0}", MyNumber);
        }
    }
}
```

## 复习访问修饰符

现在我们已经涵盖了与继承相关的主题，让我们再次查看面向对象编程中访问修饰符的概念。之前，我们了解到访问修饰符就像守门员。它控制谁可以访问特定的字段、属性或方法。C# 带有 4 种访问修饰符：`private`, `public`、`protected` 和 `internal`。

任何声明为 `internal` 的成员只能在当前程序集（assembly）中访问。由于本书不会介绍程序集，因此我们不会演示 `internal` 的工作原理。

为了理解 `private`、`public` 和 `protected` 如何工作，请考虑下面的示例。我们将使用字段来演示这一概念。方法和属性同样适用于。

假设我们有一个三个字段的类：

```csharp
class ClassA
{
    private int privateNum = 1;
    public int publicNum = 2;
    protected int protectedNum = 3;
}
```

如果 `ClassB` 继承自 `ClassA`，

```csharp
class ClassB:ClassA
{
    public void PrintMessages()
    {
        // 这是可以的
        Console.WriteLine(publicNum);
        // 这是可以的
        Console.WriteLine(protectedNum);
        // 这是不允许的
        Console.WriteLine(privateNum);
    }
    public void WriteLine()
```

前两个 `WriteLine()` 语句不会产生任何错误，因为派生类可以访问父类中的任何 `public` 和 `protected` 字段。

然而，第三条语句会报错，因为 `privateNum` 是一个 `private` 字段，因此只能在 `ClassA` 内部访问。

如果一个类没有继承自 `ClassA`，我们需要实例化一个 `ClassA` 对象来访问 `ClassA` 的 `public` 字段。然而，即使有了 `ClassA` 对象，我们也无法访问 `ClassA` 的 `private` 和 `protected` 字段。在下面的示例中，`ClassC` 没有继承自 `ClassA`。因此，第一个 `WriteLine()` 语句不会产生任何错误，但第二个和第三条语句会。

```csharp
class ClassC
{
    ClassA a = new ClassA();
    public void PrintMessages()
    {
        // 这是可以的
        Console.WriteLine(a.publicNum);
        // 这是不允许的
        Console.WriteLine(a.protectedNum);
        // 这是不允许的
        Console.WriteLine(a.privateNum);
    }
}
```

简而言之，任何声明为 `public` 的内容在处处可见；访问 `public` 成员没有限制。相反，任何声明为 `private` 的内容只能在声明它的类内部访问。任何声明为 `protected` 的内容在声明它的类以及任何派自它的类中都可以访问。

# 第 9 章：枚举（Enum）和结构体（Struct）

在第 3 和第 4 章中，我们了 C# 提供的一些内置数据类型。这些包括如 `int`、`float` 和 `double` 等值类型，以及如数组、字符串和列表等引用数据类型。此外，我们还在第 7 和第 8 章学习了如何编写自己的类。类可以被看作是一种高级的用户定义数据类型，它将一组相关的字段、属性和方法分组为一个逻辑单元。

在本章中，我们将查看 C# 中的另外两种用户定义数据类型——`enum` 和 `struct`。

## Enum（枚举）

枚举（enumerated type 的缩写）是一种特殊的数据类型，允许程序员为一组整数常量提供有意义的名称。

要声明枚举，我们使用 `enum` 关键字后跟枚举的名称。枚举成员包含在一在大括号中，并用逗号分隔。

下文是一个示例：

```csharp
enum DaysOfWeek
{
    Sun, Mon, Tues, Wed, Thurs, Fri, Sat
}
```

注意，我们不在最后一个成员末尾加分号。

在声明 `DaysOfWeek` 枚举后，我们可以像这样声明并初始化一个 `DaysOfWeek` 变量：

```csharp
DaysOfWeek myDays = DaysOfWeek.Mon;
```

变量的名为 `myDays`。如果我们写

```csharp
Console.WriteLine(myDays);
```

我们将得到

Mon

默认情况下，枚举中的每个成员都被分配一个整数值，从零开始。也就是说，在我们的示例中，`Sun` 被赋值为 0，`Mon` 为 1，`Tues` 为 2，依此类推。

由于枚举本质上是整数，我们可以将 `DaysOfWeek` 变量转换为 `int`，反之亦然。例如，

```csharp
Console.WriteLine((int)Days);
```

给了我们整数 1，而

```csharp
Console.WriteLine((DaysOfWeek)1);
```

给了我们 Mon。

如果你想为枚举成员分配一组不同的整数，可以采取以下操作

```csharp
enum DaysOfWeekTwo {
  Sun = 5, Mon = 10, Tues, Wed, Thurs, Fri, Sat
}
```

现在，`Sun` 被赋值为 5，`Mon` 被赋值为 10。由于我们没有为 `Tues` 到 `Sat` 分配值，10之后的连续数字将被分配给它们。即 `Tues = 11`，`Wed = 12` 等。

所有枚举在内部都存储为整数（`int`）。如果你想将底层数据类型从 `int` 更改为其他类型，可以在枚举名称后添加冒号，然后是所需的数据类型。允许 `char` 外的任何整数数据类型。例如

```csharp
enum DaysOfWeekThree : byte {
  Sun, Mon, Tues, Wed, Thurs, Fri, Sat
}
```

当然，如果你使用 `byte` 数据类型，你无法执行类似

```csharp
enum DaysOfWeekFour : byte {
  Sun = 300, Mon, Tues, Wed, Thurs, Fri, Sat
}
```

因为 `byte` 的范围是从 0 到 255。

使用枚举有两个主要原因。第一个是提高代码的可读性。第二个原因是限制变量可以取的值。如果我们有一个存储星期的枚举，我们可能会无意中给它赋值。如果我们使用 `byte` 数据类型，我们就无法执行此类操作，因为 `byte` 的范围是从 0 到 255。

## Struct（结构体）

结构体在许多方面与类相似。像类一样，它们包含属性、构造函数和字段等元素来组合相关的成员。要声明结构体，使用 `struct` 关键字。示例：

```csharp
struct MyStruct
{
    // 字段
    private int x, y;
    private AnotherClass myCamera;
    private Days myDays;
    // 构造函数
    public MyStruct(int a, int b, int c)
    {
```

