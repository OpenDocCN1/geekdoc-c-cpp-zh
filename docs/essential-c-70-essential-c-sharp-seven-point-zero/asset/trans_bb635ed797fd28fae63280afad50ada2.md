
## 提供初始化方法

```csharp
class Employee
{
  public void Deconstruct(
    out int id, out string firstName,
    out string lastName, out string salary)
  {
    (id, firstName, lastName, salary) =
      (Id, FirstName, LastName, Salary);
  }
  // ...
}
```

```csharp
class Program
{
  static void Main()
  {
    Employee employee;
    employee = new Employee("Inigo", "Montoya");
    employee.Salary = "Too Little";
    employee.Deconstruct(out _, out string firstName,
                         out string lastName, out string salary);
    System.Console.WriteLine(
      "{0}: {1}: {2}",
      firstName, lastName, salary);
  }
}
```

你可以直接调用此类方法，正如在第 5 章中所预期的那样，可以内联声明 out 参数。

从 C# 7.0 开始，通过直接将对象实例分配给元组，可以隐式调用 **Deconstruct()** 方法——即**解构器**（此时假设被分配的变量已经声明过）：

```csharp
(_, firstName, lastName, salary) = employee;
```

该语法产生的 CIL 代码与列表 6.34 中高亮显示的部分完全相同——它只是一种更简单的语法（并且不太能体现出调用了 Deconstruct() 方法）。

注意，该语法允许使用元组语法来匹配 out 参数赋值中的变量。它也不允许分配给元组类型，例如：

```csharp
(int, string, string, string) tuple = employee;
```

或者使用命名字项，例如：

```csharp
(int id, string firstName, string lastName, string salary) tuple = employee;
```

要声明一个解构器，方法名必须是 `Deconstruct`，并且具有返回 `void` 且仅接受两个或更多 out 参数的签名。并且，给定这样的签名，可以直接将对象实例分配给元组，而无需显式的方法调用。

## 静态成员

第 1 章中的 `HelloWorld` 示例简要涉及了关键字 `static`。本节更完整地定义了 `static` 关键字。

首先，让我们考虑一个例子。假设每个员工的 `Id` 值需要是唯一的。实现这一点的一种方法是存储一个计数器来跟踪每个员工的 `ID`。然而，如果将值存储为实例字段，那么每次实例化对象时，都会创建一个新的 `NextId` 字段，这意味着每个 `Employee` 对象实例都会为该字段消耗内存。最大的问题是，每次实例化一个 `Employee` 对象时，之前实例化的所有 `Employee` 对象上的 `NextId` 值都需要用下一个 `ID` 值进行更新。在这种情况下，你需要的是一个由所有 `Employee` 对象实例共享的单个字段。

### 语言对比：C++/Visual Basic——全局变量和函数

与之前的许多语言不同，C# 没有全局变量或全局函数。C# 中的所有字段和方法都出现在类的上下文中。在 C# 领域中，全局字段或函数的等价物是静态字段或函数。全局变量/函数与 C# 静态字段/方法之间没有功能差异，除了静态字段/方法可以包含访问修饰符（例如 *private*），从而限制访问并提供更好的封装。

### 静态字段

要定义跨多个实例可用的数据，你使用 `static` 关键字，如列表 6.35 所示。

**列表 6.35：声明静态字段**

```csharp
class Employee
{
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
        Id = NextId;
        NextId++;
    }

    // ...

    public static int NextId;
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Salary { get; set; } = "Not Enough";

    // ...
}
```

在这个例子中，**NextId** 字段声明包含 **static** 修饰符，因此被称为**静态字段**。与 **Id** 不同，**NextId** 在所有的 **Employee** 实例之间共享单一的存储位置。在 **Employee** 构造函数内部，在递增 **Id** 之前，你立即将新 **Employee** 对象的 **Id** 分配为 **NextId** 的值。当创建另一个 **Employee** 类实例时，**NextId** 将会递增，并且新的 **Employee** 对象的 **Id** 字段将持有不同的值。

正如**实例字段**（非静态字段）可以在声明时初始化一样，静态字段也可以，如列表 6.36 所示。

**列表 6.36：在声明时分配静态字段**

```csharp
class Employee
{
    // ...
    public static int NextId = 42;
    // ...
}
```

与实例字段不同，如果没有为静态字段提供初始化，静态字段将自动分配其默认值（0、**null**、**false** 等）——相当于 **default**(T)，其中 T 是类型名称。因此，即使从未在 C# 代码中显式分配，也可以访问静态字段。

非静态字段，或实例字段，为所属的每个对象提供一个新的存储位置。相比之下，静态字段不属于实例，而是属于类本身。因此，你通过类名从类外部访问静态字段。考虑列表 6.37 中显示的新 Program 类（使用列表 6.35 中的 Employee 类）。

**列表 6.37：访问静态字段**

```csharp
using System;

class Program
{
    static void Main()
    {
        Employee.NextId = 1000000;

        Employee employee1 = new Employee(
            "Inigo", "Montoya");
        Employee employee2 = new Employee(
            "Princess", "Buttercup");

        Console.WriteLine(
            "{0} {1} {2}",
            employee1.FirstName,
            employee1.LastName,
            employee1.Id);
        Console.WriteLine(
            "{0} {1} {2}",
            employee2.FirstName,
            employee2.LastName,
            employee2.Id);

        Console.WriteLine(
            $"NextId = { Employee.NextId }");
    }

    // ...
}
```

**输出 6.8**

```
Inigo Montoya (1000000)
Princess Buttercup (1000001)
NextId = 1000002
```

为了设置和检索 `NextId` 静态字段的初始值，你使用类名 `Employee`，而不是类型的实例引用。唯一可以省略类名的地方是在类本身内部（或派生类中）。换句话说，`Employee(...)` 构造函数不需要使用 `Employee.NextId`，因为代码出现在 `Employee` 类本身的上下文中，因此上下文已经明确。变量的范围是可以通过其未限定名称引用的程序文本；静态字段的范围是类的文本（以及任何派生类）。

尽管你引用静态字段的方式与引用实例字段的方式略有不同，但在同一个类中不能定义一个静态字段和一个同名实例字段。错误引用错误字段的可能性很高，因此 C# 设计者决定阻止此类代码。因此，名称重叠会在声明空间中引入冲突。

### 初学者主题

#### 数据可以关联到类和对象

类和对象都可以有关联数据，就像模具和由模具创建的组件一样。

例如，模具可以拥有对应于它创建的组件数量的数据、下一个组件的序列号、注入模具中塑料的当前颜色以及每小时生产的组件数量。同样，组件有自己的序列号、自己的颜色，以及可能的创建组件的日期和时间。虽然组件的颜色对应于创建组件时模具内塑料的颜色，但它显然不包含对应于模具中当前塑料颜色或下一个要生产的组件序列号的数据。

在设计对象时，程序员应小心地适当地声明字段和方法，基于静态或实例。通常，你不应该将不访问任何实例数据的方法声明为静态方法，而应该将访问实例数据（实例不作为参数传入）的方法声明为实例方法。静态字段存储与类相关的数据，例如新实例的默认值或已创建的实例数量。实例字段存储与对象相关的数据。

