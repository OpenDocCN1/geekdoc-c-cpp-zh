
每个对象都有其类实例变量的副本。在某些情况下，某个变量的唯一副本应该被该类的所有对象共享。在这种情况下，使用静态变量（或属性）。静态变量或属性代表类级信息——该类的所有对象共享同一份数据。静态变量或属性的声明以 `static` 关键字开头。

让我们用一个例子来说明数据的动机。假设我们有一个包含火星人和和其他太空生物的视频游戏。每个火星人在意识到至少有四个火星人存在时，倾向于勇敢并攻击其他太空生物。如果火星人少于五个，则每个火星人都会变得胆小。每个火星人都需要知道 `MartianCount`。我们可以将类 `Martian` 的 `MartianCount` 统计为实例变量（作为属性，但为了讨论，这里使用实例变量）。如果我们这样做，每个火星人都将有一份独立的实例变量副本，每当我们创建一个新的火星人时，都必须更新每个火星人的实例变量 `MartianCount`。这浪费了冗余副本的空间，更新这些独立的副本且容易出错。相反，我们将 `MartianCount` 声明为静态，使得有了 `MartianCount`，但只维护一份静态 `MartianCount` 副本。我们通过让火星人构造函数实现静态的 `oldCount` 来节省空间——只有一份副本，所以我们不需要为每个火星人对象实现独立的 `martCount` 副本。

![](img/57baed2319be0bb1b5f98674846f2711_454_0.png)

> 软件工程观察 10.10
> 当类的所有对象共享同一份变量副本时，使用变量

# 静态变量作用域

每个对象都有其类实例变量的副本。在某些情况下，某个变量的唯一副本应该被该类的所有对象共享。在这种情况下，使用静态变量（或属性）。静态变量或属性代表类级信息——该类的所有对象共享同一份数据。静态变量或属性的声明以 `static` 关键字开头。

静态变量的作用域是类体。该类的公共静态成员可以通过类名和访问运算符 `(. )` 访问，如 `Math` 所示。私有静态成员只能通过类的方法访问。若要从类外部访问私有静态成员，可以提供公共方法。

![](img/57baed2319be0bb1b5f98674846f2711_454_1.png)

> 常见错误 10.2
> 通过类的实例引用静态成员是编译错误，非静态成员

![](img/57baed2319be0bb1b5f98674846f2711_454_2.png)

> 软件工程观察 10.11
> 静态方法在类加载后就可用

# 静态方法与非静态类成员

静态变量的作用域是类体。该类的公共静态成员可以通过类名和访问运算符 `(. )` 访问，如 `Math` 所示。私有静态成员只能通过类的方法访问。若要从类外部访问私有静态成员，可以提供公共方法。

# Employee 类

我们的下一个应用包含了 `Employee` 类（图 10.10）和 `EmployeeTest`（图 10.11）。`Employee` 类声明了静态自动属性 `Count` 来维护创建的 `Employee` 对象数量。

```cs
// 图 10: Employee.cs
// 静态属性用于维护创建的 Employee 对象数量。
using System;
public class Employee {
    public static int Count { get; private set; }
    public string FirstName { get; }
    public string LastName { get; }

    // 初始化姓名，对静态 Count 加 1
    // 输出指示构造函数调用的字符串
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
        Count++; // 增加员工计数
        Console.WriteLine($"Employee constructor: {FirstName}{LastName} = {Count}");
    }
}
```

图 10.10 | 静态属性用于维护创建的 Employee 对象数量。

**EmployeeTest**

`EmployeeTest` 方法 `Main`（图 10.11）实例化两个 `Employee` 对象（第 14–15 行）。当每个对象的构造函数被调用时，图 10.10 的第 17–18 行将员工的姓和名属性赋值给 `FirstName` 和 `LastName`。这些状态并没有对原始字符串参数创建副本。

当 `Employee` 对象存在时，可以在任何方法或属性中使用 `Count`。客户端可以通过表达式 `Employee.Count` 访问 `Count`，其求值为为创建的 Employee 对象数量。

# 第 10 章 类与对象：深入探讨

```csharp
// 图 10.11: EmployeeTest.cs
// 静态成员演示。
using System;
class EmployeeTest{
    static void Main()
{
        // 显示在创建 Employees 之前 Count 为 0
        Console.WriteLine($"{实例化前的 Employees 数量: {Employee.Count}}");

        // 创建两个 Employees; Count 应变为 2
        var el1 = new Employee("Susan", "Baker");
        var el2 = new Employee("Bob", "Blue");

        // 显示在创建两个 Employees 之后 Count 变为 2
        Console.WriteLine($"\n实例化后的 Employees 数量: {Employee.Count}");

        // 获取 Employees 的名称
        Console.WriteLine($"\nEmployee 1: {el1.FirstName} {el1.LastName}");
        Console.WriteLine($"\nEmployee 2: {el2.FirstName} {el2.LastName}");

        // 在此示例中，每个 Employee 只有一个引用，
        // 因此以下语句允许 CLR 将每个 Employee
        // 标记为可以进行垃圾回收
        el1 = null; // 标记 el1 引用的对象不再需要
        el2 = null; // 标记 el2 引用的对象不再需要
    }}
```

```
实例化前的 Employees 数量: 0
Employee 构造函数: Susan Baker; Count = 1
Employee 构造函数: Bob Blue; Count = 2
实例化后的 Employees 数量: 2
Employee 1: Susan Baker
Employee 2: Bob Blue
```

图 10.11 | 静态成员演示。

图 10.11 的第 18–19 行显示了更新后的 `Count`。当 `Main` 完成对两个 `Employee` 对象的使用后，第 28–29 行将 `el1` 和 `el2` 设置为 `null`，因此它们不再引用第 14–15 行中实例化的对象。由于不再有对这些对象的引用，这些对象变为可以被销毁的状态。在对象的析构函数被调用后，对象变为可以被垃圾回收的状态。（注意，我们这里不需要将 `el1` 和 `el2` 设置为 `null`——它们是局部变量——引用类型的局部变量超出作用范围时，对象的引用计数会自动递减。）

最终，垃圾回收器可能会回收这些对象的内存（或者在应用程序终止时由操作系统回收）。`C#` 不保证垃圾回收器何时执行，甚至不保证是否会执行；可能没有对象被回收，或者只回收了可用对象的一部分。

## 10.10 readonly 实例变量

最小权限原则是软件工程的基础。在应用程序的上下文中，该原则规定，代码应该被授予完成指定任务所需的权限和访问权限，但不能更多。让我们看看这一原则如何应用于实例变量。

某些实例变量需要是可以修改的，而有些不需要。在第 8.4 节中，我们使用 `const` 来声明常量，它必须在声明时初始化——该类的所有对象对该常量具有相同的值。假设我们希望一个常量对于类的每个对象可以有不同的值。为了这个目的，`C#` 提供了 `readonly` 关键字，用于指定对象的实例变量是不可修改的，并且在对象构造后任何尝试修改它的行为都是错误。例如：

```csharp
private readonly int Increment;
```

声明了一个类型为 `int` 的实例变量。像常量一样，`readonly` 标识符约定使用帕驼命名法（Pascal Case）。虽然 `readonly` 实例变量可以在声明时初始化，但并非强制要求。`readonly` 变量应该由类的每个构造函数之一初始化，或在其声明中初始化。每个构造函数可以多次为 `readonly` 实例变量赋值——该变量在构造函数执行完成之前可以保持未修改状态。如果构造函数没有初始化 `readonly` 变量，该变量将像其他实例变量一样使用默认值（数值类型为 0，`bool` 为 false，引用类型为 `null`）——这些值在构造函数执行之前被设置。
