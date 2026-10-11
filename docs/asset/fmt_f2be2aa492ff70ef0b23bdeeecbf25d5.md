
`class Employee`

{

  // 实例变量和方法在这里

}

**图 9-1** `Employee` 类外壳

## 创建实例变量和方法

当你创建一个类时，你同时定义了它的属性和方法。你使用大括号来声明类的实例变量，其语法与声明其他变量相同——即你提供一个类型和一个标识符。例如，对于 *Employee* 类，你可以声明一个整数类型的 ID 号给 *Employee* 对象，每个对象将有自己的 `idNumber`。你可以将该 ID 号简单地定义为 `int idNumber;`。然而，程序员经常为类中的每个字段包含一个访问修饰符，并将 `idNumber` 声明为 `private int idNumber;`。图 9-2 显示了一个包含私有 `idNumber` 字段的 *Employee* 类。

```csharp
class Employee
{
  private int idNumber;
}
```

**图 9-2** 包含 `idNumber` 字段的 `Employee` 类

你在日常生活中每天都能看到信息隐藏的例子。例如，你无法看到汽车油箱内部来判断油箱有多少。相反，你使用仪表盘上的刻度来提供所需的信息。同样，在面向对象编程中，数据字段通常是**私有的 `private`**，但这些通过**公共的 `public`** 方法进行访问。类的**私有**数据应该只由自身的方法进行更改或操作，而不是属于其他类的方法。将数据设为**私有**的好处是能够控制它们的值。设置变量的方法可以确保值落在指定的范围内。例如，*Employee* 的工资不应低于最低工资，或者部门编号不应大于 10。

与类的**私有**数据字段相反，大多数实例方法通常不是**私有**的；它们是**公共的 `public`**。这种产生的**私有数据/公共**方法安排提供了一种控制外部访问你数据的方法——只有类的非私有方法可以用于访问类的私有数据。这种情况类似于有一个“公共”前台接待员，他控制着进出你私有办公室的消息。非私有方法的编写方式控制了你如何使用私有数据。

例如，一个包含 `idNumber` 的 `Employee` 类可能需要一个方法向公司客户显示员工的欢迎信息。该方法的合理名称是 `WelcomeMessage()`，其声明为 `public void WelcomeMessage()`，因为它具有公共访问权限且没有返回值。图 9-3 显示了添加了 `WelcomeMessage()` 方法的 `Employee` 类。

```csharp
class Employee  {
    private int idNumber;
    public void WelcomeMessage()
    {
        Console.WriteLine("Welcome from Employee #{0}", idNumber);
        Console.WriteLine("How can I help you?");
    }
}
```

**图 9-3** 包含 `idNumber` 字段和 `WelcomeMessage()` 方法的 `Employee` 类

注意，你创建的 `WelcomeMessage()` 没有使用 `static` 修饰符，这与你创建的许多其他方法不同。`static` 用于类级方法，而不用于“属于”对象的实例。如果你正在创建一个带有 `Main()` 方法的程序并打算执行它来完成某些任务，那么你的许多方法将是静态的。你可以在从 `Main()` 中调用静态方法而无需创建对象。然而，如果你在另一个类中，请使用类名、点 `.` 和方法调用 `()`。如果你正在创建一个将要实例化的类，大多数方法可能是非静态的，因为你将把方法与单个对象和数据关联。（使用对象名、点 `.` 和方法调用。）每当图 9-3 类中的 `WelcomeMessage()` 实例在使用时，它将显示特定对象的 `idNumber`。换句话说，该方法对每个对象实例都能正常工作，它不是静态的。

> 在第 7 章中，你学习了创建一个 `Form`（表单），你在任何方法之外包含了非静态变量声明——例如，如果两个 `Click()` 方法必须访问相同的数据。现在你可以理解此类变量是非静态的，因为它们与对象（即定义的 `Form`）相关联。

图 9-3 中的 `Employee` 类不是一个可以运行的程序；它不包含 `Main()` 方法。相反，它只是描述了当你编写包含一个或多个 `Employee` 对象的程序时，`Employee` 对象将拥有什么（一个 `idNumber`）以及能够做什么（显示问候语）。

类可以包含作为其他类实例的字段。例如，你可能会创建一个名为 `Date` 的类，其中包含月、日、年，并向 `Employee` 类中添加两个 `Date` 字段来存储员工的出生日期和日期。你可能还会创建一个 `BusinessOffice` 类并在其中声明 `Employee` 对象。在另一个对象内部使用对象被称为组合（composition）。创建的关系也被称为“拥有关系”（has-relationship），因为一个对象“拥有”另一个对象的实例。

观看视频《创建类》。

## 创建可以被实例化的类

### 两个真理一个谎言

1. 类头始终包含 `class` 关键字。
2. 当你创建一个类时，你同时定义了它的属性和方法。
3. 类中定义的大多数字段和方法都是私有的。

错误的陈述是 #3。类中的大多数字段是私有的，但大多数方法是公共的。

## 创建对象

声明类不会创建任何实际对象。类只是对如果以后实例化任何对象，该对象将是什么样的的一种抽象描述。就像你可以在第一个产品离开装配线很久以前就了解你打算制造的物品的所有特征一样，你可以在实例化该类的任何对象之前，创建一个包含字段和方法的类。

### 创建对象

在语句 `myAssistant = new Employee();` 中，`new` 操作符之后语句的最后部分 `Employee()` 看起来很像一个带有括号的方法名。事实上，它是一个用于构造 `Employee` 对象的的方法名。`Employee()` 是一个构造函数。在本章中，你将编写你自己的构造函数。现在，请注意，当你没有为类编写构造函数时，C# 会为你自动生成一个，且构造函数的名称始终与构造对象所属的类名称相同。

在本章的后半部分，你将学到类自动生成的类构造函数是“默认构造函数”，这意味着它接受参数。程序员错误地将“自动生成”和“默认”这两个术语等同起来。类自动创建的构造函数是默认构造函数的一个示例，但你也可以显式地创建自己的默认构造函数。

对象实例化后，可以使用对象的标识符、点 `.` 以及公共成员的标识符来访问其非静态公共成员。例如，如果你声明了一个名为 `myAssistant` 的 `Employee` 实例，你可以访问 `myAssistant.WelcomeMessage();`。

像 `myAssistant` 这样使用实例方法的对象被称为“调用对象”。如果 `WelcomeMessage()` 是静态方法，那么语句 `myAssistant.WelcomeMessage();` 将是非法的。由于该方法是非静态的，因此可以恰当地用于每个唯一的 `Employee` 对象。

声明了 `myAssistant` 的程序无法直接访问其 `idNumber`；程序访问私数据的唯一方法是使用对象的公共方法之一。由于 `WelcomeMessage()` 方法和 `idNumber` 一样属于类，而且由于 `WelcomeMessage()` 是公共的，客户端方法（例如程序中的 `Main()` 方法）可以使用该方法。图 9-4 显示了一个类 `CreateEmployee`，其 `Main()` 方法声明了一个 `Employee` 并显示了该对象的欢迎消息。图 9-5 显示了程序的执行结果。

```cs
using static System.Console;
class CreateEmployee
{
    static void Main()
    {
        Employee myAssistant = new Employee();
        myAssistant.WelcomeMessage();
    }
}
```

**图 9-4** `CreateEmployee` 程序

# 第 9 章 使用类和对象

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_386_0.png)

**图 9-5** `CreateEmployee` 程序的输出

在 9-5 的输出中，`Employee` 的 ID 号是 0。默认情况下，对象中所有未分配的数值字段都初始化为 0。当你编译图 9-4 中的程序时，你会收到一条警告消息：

字段 `Employee.idNumber` 始终未被赋值，且将始终具有其默认值 0。

当然，通常你希望为每个 `Employee` 的 `idNumber` 字段提供不同的值。为对象字段提供值的方法之一是创建属性，你将在本章的稍后的部分完成。

## 将对象传递给方法

类代表一种数据类型，你可以像传递简单类型变量一样将对象传递给方法。例如，图 9-6 中的程序显示了如何将字符串变量和 `Employee` 对象传递给 `DisplayEmployeeData()` 方法。每个 `Employee` 被赋值给方法内部的 `emp` 参数。图 9-7 显示了程序的输出。

```cs
using System;
class CreateTwoEmployees
{
    static void Main()
    {
        Employee aWorker = new Employee();
        Employee anotherWorker = new Employee();
        DisplayEmployeeData("First", aWorker);
        DisplayEmployeeData("Second", anotherWorker);
    }
    static void DisplayEmployeeData(string order, Employee emp)
    {
        Console.WriteLine("\n" + order + " employee's message: " + emp.WelcomeMessage());
    }
}
```

**图 9-6** `CreateTwoEmployees` 程序

```
First employee's message:
Welcome from Employee #0
How can I help you?

Second employee's message:
Welcome from Employee #0
How can I help you?
```

**图 9-7** `CreateTwoEmployees` 程序的输出

当你将对象传递给方法时，方法中对对象参数的任何更改也会影响调用方法中作为参数的对象。

在 9-6 中，`DisplayEmployeeData()` 方法默认是内部的 `internal`。由于该方法接受一个 `Employee` 参数，它的访问级别必须不能高于 `Employee` 类（该类也是内部的）。这种限制保护了为 `Employee` 类非成员所提供的安全性。如果你将 `DisplayEmployeeData()` 方法和 `Employee` 类都设置为公共 `public`，程序也可以正常工作。

## 两个真理与一个谎言

1. 声明类会创建一个新数据类型的对象。
2. 在声明类之后，你必须使用 `new` 操作符为该类的对象分配内存并对其进行实例化。
3. 对象实例化后，可以使用对象的标识符、点和方法调用来访问其公共成员。

## 创建属性

通常，你通过对象调用的方法被用来更改其字段的状态。例如，你可能想要设置派对的日期或时间。在 `Employee` 类中，你可以编写一个如 `SetIDNumber()` 的方法来如下设置员工的 `idNumber` 字段：

```cs
public void SetIDNumber(int number)
{
    idNumber = number;
}
```

然后，在实例化一个名为 `myAssistant` 的 `Employee` 对象后，你可以像如下调用该方法：
`myAssistant.SetIDNumber(1234);`

属性是提供灵活读取和写入私有字段机制。它允许你在访问器中包含逻辑，例如验证值。在 C# 中，属性使用 `get` 和 `set` 访问器。你可以像使用方法一样使用属性，但它们看起来更像字段。

属性允许你对字段进行封装，这在面向对象编程中非常重要，因为它可以隐藏内部实现细节，并只暴露必要的接口。

属性的语法如下：

```cs
public int IdNumber
{
    get
    {
        return idNumber;
    }
    set
    {
        idNumber = value;
    }
}
```

如果一个属性只有 `get` 访问器，那么它就是只读的。如果它只有 `set` 访问器，那么它是只写的。此外，你还可以使用 `init` 关键字来创建只读属性，允许仅在对象初始化时进行赋值。

在 C# 中，你还可以自动实现属性（Auto-implemented properties），不需要显式定义私有字段：

```cs
public int IdNumber { get; set; }
```

编译器会为这种属性自动创建一个私有字段。这种方式大大减少了代码量，同时保持了属性的灵活性。
