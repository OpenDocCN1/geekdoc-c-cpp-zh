

```csharp
static void Main()
{
    // Animal a = new Animal(); // ❌ Error! Cannot instantiate abstract class
    Dog myDog = new Dog(); // ✅ Valid
    myDog.Breathe(); // Inherited method
    myDog.MakeSound(); // Implemented method
}
}
```

**[执行结果]**

```text
Breathing...
Bark!
```

当多个类共享共同逻辑，但在某些行为的实现上有所不同时，会使用抽象类。

要点：

- 不能创建抽象类的实例。
- 可以在抽象类中定义带逻辑的方法（称为具体方法）。
- 必须在派生类中重写抽象方法。
- 它强制实施契约，同时允许共享代码以避免重复。
- 这在游戏引擎或 UI 系统等实际应用中尤其有用，因为许多实体的基础行为是一致的（例如，所有 UI 元素都能“绘制”，但每个元素的绘制方式不同）。

与接口不同，抽象类可以包含字段、构造函数和已实现的方法。

如果任何方法是抽象的，则该类必须声明为抽象类。

一个类只能继承一个抽象类，这符合 C# 的单类继承模型。

## 26. 多个接口，而非多个类

C# 允许一个类实现多个接口，从而实现灵活性。但是，它只能继承一个类，从而避免多类继承带来的歧义。

此示例展示了一个类在继承单个基类的同时实现两个接口。

**[代码示例]**

```csharp
using System;
// Base class
class Machine
{
    public void Start()
    {
        Console.WriteLine("Machine started.");
    }
}

// First interface
interface IPrintable
{
    void Print();
}

// Second interface
interface IScannable
{
    void Scan();
}

// Derived class
class MultifunctionPrinter : Machine, IPrintable, IScannable
{
    public void Print()
    {
        Console.WriteLine("Printing document...");
    }
    public void Scan()
    {
        Console.WriteLine("Scanning document...");
    }
}
class Program
{
    static void Main()
    {
        MultifunctionPrinter mfp = new MultifunctionPrinter();
        mfp.Start();  // Inherited from Machine
        mfp.Print();  // From IPrintable
        mfp.Scan();   // From IScannable
    }
}
```

**[执行结果]**

```text
Machine started.
Printing document.
Scanning document.
```

C# 不支持类的多重继承，以避免菱形问题——即当多个基类中存在相同方法时，编译器无法确定应继承哪个版本的方法的情况。

相反，C# 允许你实现多个接口，这些接口只包含方法声明而不包含实现。这避免了歧义并保持了灵活性。

现实世界类比：

想想智能手机。它可以是一个 Device（基类），并且还可以实现 ICamera、IMusicPlayer 和 IGPS 等功能。这些是由接口描述的能力。

**[补充]**

接口不能包含任何代码（在 C# 8 之前）；它们只定义应该做什么，而不定义如何做。

从 C# 8 开始，接口可以包含默认实现，但应谨慎使用。

与类不同，C# 类可以实现任意数量的接口，从而赋予其模块化能力。

## 27. 在不更改现有类代码的情况下向其添加方法

C# 中的扩展方法允许你向现有类型（如类或结构体）添加新方法，而无需修改原始源代码。

下面是一个简单示例，我们向内置的 string 类添加一个统计单词数的方法。

**[代码示例]**

```csharp
using System;

public static class StringExtensions
{
    // Define an extension method for the string type
    public static int WordCount(this string str)
    {
        // Split the string by spaces and count the resulting parts
        return str.Split(new char[] { ' ' }, StringSplitOptions.RemoveEmptyEntries).Length;
    }
}

class Program
{
    static void Main()
    {
        string message = "Hello from the C# world!";
        // Call the extension method as if it's a built-in method
        int count = message.WordCount();
        Console.WriteLine("Word count: " + count);
    }
}
```

**[执行结果]**

```text
Word count: 5
```

扩展方法在静态类中声明，并且自身必须是静态方法。

第一个参数前的关键字 this（this string str）告诉编译器，此方法是 string 类型的扩展方法。

定义后，你可以像使用被扩展类型的成员一样使用该方法——调用时无需特殊语法。

当你处理 .NET 类型或库，无法修改原始源代码但仍想添加自定义功能时，这尤其有用。

它们也常用于 LINQ，而 LINQ 大量依赖扩展方法。

**[补充]**

在使用扩展方法的文件中，必须包含定义该扩展方法的命名空间（using YourNamespace;）。

Visual Studio 中的 IntelliSense 会用特殊图标（↓）显示扩展方法。

扩展方法不会重写现有方法——它们仅当不存在具有相同签名的实例方法时才起作用。

## 28. 使用泛型进行灵活编程

C# 支持可处理任意数据类型的泛型类、方法和接口，帮助你编写可重用且类型安全的代码。

下面是一个存储任意类型值的泛型类，以及一个交换两个变量的泛型方法的示例。

**[代码示例]**

```csharp
using System;

// A generic class that can hold any data type
class Box<T>
{
    public T Value;
    public Box(T value)
    {
        Value = value;
    }
    public void Display()
    {
        Console.WriteLine("Box holds: " + Value);
    }
}

class Program
{
    // A generic method to swap two values
    static void Swap<T>(ref T a, ref T b)
    {
        T temp = a;
        a = b;
        b = temp;
    }
    static void Main()
    {
        // Using the generic Box class
        Box<int> intBox = new Box<int>(123);
        Box<string> strBox = new Box<string>("C# Rocks");
        intBox.Display(); // Outputs: Box holds: 123
        strBox.Display(); // Outputs: Box holds: C# Rocks
        // Using the generic Swap method
        int x = 1, y = 2;
        Swap(ref x, ref y);
        Console.WriteLine("x: " + x + ", y: " + y); // x: 2, y: 1
    }
}
```

**[执行结果]**

```text
Box holds: 123
Box holds: C# Rocks
x: 2, y: 1
```

泛型允许你编写灵活、可重用的代码，而无需牺牲类型安全性。

Box<T> 类定义了一个类型参数 T，它代表“任意类型”。创建此类的对象时，需要指定实际类型（如 int 或 string）。

Swap<T> 方法可处理任意数据类型，并且不需要为每种类型重复代码。

泛型对于编写库、数据结构和实用函数非常重要。它们消除了强制转换以及装箱/拆箱的需要，从而使代码更快、更安全。

**[补充]**

常见的 .NET 内置泛型类型包括 List<T>、Dictionary<TKey, TValue> 和 Nullable<T>。

可以使用 where 子句约束泛型参数（例如 where T : class）。

泛型在 LINQ 以及 List<T> 和 Queue<T> 等集合中被大量使用。

## 29. 使用 where 约束泛型

C# 允许使用 where 子句向泛型添加约束。这可确保泛型类型参数满足特定要求，例如是类、具有默认构造函数或实现特定接口。

以下代码展示了如何使用 where 子句限制泛型方法，使其仅接受实现特定接口的类型。

**[代码示例]**

```csharp
using System;

// Define an interface
interface IPrintable {
    void Print();
}

// A class that implements IPrintable
class Report : IPrintable {
    public void Print() {
        Console.WriteLine("Printing report...");
    }
}

// Generic class with a constraint
class Printer<T> where T : IPrintable {
    public void PrintItem(T item) {
        item.Print(); // Safe to call Print() because T is guaranteed to implement IPrintable
    }
}

class Program {
    static void Main() {
```

