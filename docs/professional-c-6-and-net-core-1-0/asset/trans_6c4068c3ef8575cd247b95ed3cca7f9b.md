

BubbleSorter/Employee.cs:

```csharp
class Employee
{
    public Employee(string name, decimal salary)
    {
        Name = name;
        Salary = salary;
    }

    public string Name { get; }
    public decimal Salary { get; private set; }

    public override string ToString() => $"{Name}, {Salary:C}";

    public static bool CompareSalary(Employee e1, Employee e2) =>
        e1.Salary < e2.Salary;
}
```

请注意，为了匹配 `Func<T, T, bool>` 委托的签名，你必须在该类中将 `CompareSalary` 定义为接受两个 `Employee` 引用并返回布尔值。在实现中，基于薪水的比较被执行。

现在你可以编写一些客户端代码来请求排序（代码文件 BubbleSorter/Program.cs）：

```csharp
using static System.Console;

namespace Wrox.ProCSharp.Delegates
{
    class Program
    {
        static void Main()
        {
            Employee[] employees =
            {
                new Employee("Bugs Bunny", 20000),
                new Employee("Elmer Fudd", 10000),
                new Employee("Daffy Duck", 25000),
                new Employee("Wile Coyote", 1000000.38m),
                new Employee("Foghorn Leghorn", 23000),
                new Employee("RoadRunner", 50000)
            };

            BubbleSorter.Sort(employees, Employee.CompareSalary);

            foreach (var employee in employees)
            {
                WriteLine(employee);
            }
        }
    }
}
```

运行此代码显示员工已根据薪水正确排序：

```text
Elmer Fudd, $10,000.00
Bugs Bunny, $20,000.00
Foghorn Leghorn, $23,000.00
Daffy Duck, $25,000.00
RoadRunner, $50,000.00
Wile Coyote, $1,000,000.38
```

## 多播委托

到目前为止，你使用的每个委托都只包装一个方法调用。调用委托相当于调用该方法。如果你想调用多个方法，你需要通过委托显式地多次调用。然而，委托可以包装多个方法。这种委托被称为多播委托。当多播委托被调用时，它会按顺序依次调用每个方法。为此工作，委托签名应返回 void；否则，你只会得到委托调用的最后一个方法的结果。

对于 void 返回类型，你可以使用 `Action<double>` 委托（代码文件 MulticastDelegates/Program.cs）：

```csharp
class Program
{
    static void Main()
    {
        Action<double> operations = MathOperations.MultiplyByTwo;
        operations += MathOperations.Square;
```

在之前的示例中，你想存储对两个方法的引用，因此你实例化了一个委托数组。在这里，你只需将两个操作都添加到同一个多播委托中。多播委托识别运算符 `+` 和 `+=`。或者，你可以扩展前述代码的最后两行，如以下片段所示：

```csharp
Action<double> operation1 = MathOperations.MultiplyByTwo;
Action<double> operation2 = MathOperations.Square;
Action<double> operations = operation1 + operation2;
```

多播委托还识别运算符 `-` 和 `-=` 以从委托中移除方法调用。

> **注意** 就内部实现而言，多播委托是一个派生自 `System.MulticastDelegate` 的类，而 `System.MulticastDelegate` 又派生自 `System.Delegate`。`System.MulticastDelegate` 具有额外的成员，允许将方法调用链接到一个列表中。

为了说明多播委托的使用，以下代码将 SimpleDelegate 示例重写为一个新的示例：MulticastDelegate。因为现在委托需要引用返回 void 的方法，所以你必须重写 MathOperations 类中的方法，使其显示结果而不是返回它们（代码文件 MulticastDelegates/MathOperations.cs）：

```csharp
class MathOperations
{
    public static void MultiplyByTwo(double value)
    {
        double result = value * 2;
        WriteLine($"Multiplying by 2: {value} gives {result}");
    }

    public static void Square(double value)
    {
        double result = value * value;
        WriteLine($"Squaring: {value} gives {result}");
    }
}
```

为了适应这一变化，你还必须重写 ProcessAndDisplayNumber（代码文件 MulticastDelegates/Program.cs）：

```csharp
static void ProcessAndDisplayNumber(Action<double> action, double value)
{
    WriteLine();
    WriteLine($"ProcessAndDisplayNumber called with value = {value}");
    action(value);
}
```

现在你可以尝试你的多播委托：

```csharp
static void Main()
{
    Action<double> operations = MathOperations.MultiplyByTwo;
    operations += MathOperations.Square;

    ProcessAndDisplayNumber(operations, 2.0);
    ProcessAndDisplayNumber(operations, 7.94);
    ProcessAndDisplayNumber(operations, 1.414);
    WriteLine();
}
```

每次调用 ProcessAndDisplayNumber 时，它都会显示一条消息，说明它已被调用。然后以下语句会导致 action 委托实例中的每个方法调用依次被调用：

```csharp
action(value);
```

运行前述代码会产生以下结果：

```text

ProcessAndDisplayNumber called with value = 2
Multiplying by 2: 2 gives 4
Squaring: 2 gives 4

ProcessAndDisplayNumber called with value = 7.94
Multiplying by 2: 7.94 gives 15.88
Squaring: 7.94 gives 63.0436

ProcessAndDisplayNumber called with value = 1.414
Multiplying by 2: 1.414 gives 2.828
Squaring: 1.414 gives 1.999396
```

如果你使用多播委托，请注意，链接到同一委托的方法的调用顺序在形式上是未定义的。因此，避免编写依赖于此类方法按特定顺序调用的代码。

通过一个委托调用多个方法可能会导致更大的问题。多播委托包含一组委托，按顺序依次调用它们。如果委托调用的方法之一抛出异常，整个迭代就会停止。考虑以下 MulticastIteration 示例。这里使用了返回 void 且无参数的简单委托 Action。该委托旨在调用方法 One 和 Two，它们满足委托的参数和返回类型要求。请注意方法 One 抛出异常（代码文件 MulticastDelegateWithIteration/Program.cs）：

```csharp
using System;
using static System.Console;

namespace Wrox.ProCSharp.Delegates
{
    class Program
    {
        static void One()
        {
            WriteLine("One");
            throw new Exception("Error in one");
        }

        static void Two()
        {
            WriteLine("Two");
        }
    }
}
```

在 Main 方法中，委托 d1 被创建以引用方法 One；接下来，方法 Two 的地址被添加到同一委托中。调用 d1 以调用两个方法。异常在 try/catch 块中被捕获：

```csharp
static void Main()
{
    Action d1 = One;
    d1 += Two;

    try
    {
        d1();
    }
    catch (Exception)
    {
        WriteLine("Exception caught");
    }
}
```

只有第一个方法被委托调用。因为第一个方法抛出异常，委托的迭代在此停止，方法 Two 从未被调用。结果可能有所不同，因为调用方法的顺序未定义：

> **注意** *错误和异常在第 14 章“错误和异常”中有详细解释。*

在这种情况下，你可以通过自行迭代列表来避免该问题。Delegate 类定义了 GetInvocationList 方法，它返回一个 Delegate 对象数组。现在你可以使用此委托直接调用与它们关联的方法，捕获异常并继续下一次迭代：

```csharp
static void Main()
{
    Action d1 = One;
    d1 += Two;

    Delegate[] delegates = d1.GetInvocationList();
    foreach (Action d in delegates)
    {
        try
        {
            d();
        }
        catch (Exception)
        {
            WriteLine("Exception caught");
        }
    }
}
```

当你使用代码更改运行应用程序时，你可以看到在捕获异常后迭代会继续下一个方法：

```text
One
Exception caught
Two
```

## 匿名方法

到目前为止，委托工作时必须已经存在一个方法（即委托使用与将要使用的一个或多个方法相同的签名定义）。然而，使用委托的另一种方式是使用匿名方法。匿名方法是一段用作委托参数的代码块。

定义使用匿名方法的委托的语法不会改变。变化发生在委托实例化时。以下简单的控制台应用程序展示了如何使用匿名方法（代码文件 AnonymousMethods/Program.cs）：

```csharp
using static System.Console;
using System;

namespace Wrox.ProCSharp.Delegates
{
```

