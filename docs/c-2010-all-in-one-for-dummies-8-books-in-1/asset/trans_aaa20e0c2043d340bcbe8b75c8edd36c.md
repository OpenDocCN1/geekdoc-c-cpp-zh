
虽然它只能继承一个基类，但它还可以实现任意数量的接口。在我将“可记录性”（recordability）视为一个接口后，一些录制设备看起来如下：

```sharp
public class Pen : IRecordable    // 基类是 Object。
{
    public void TakeNote(string note)
    {
        // 用笔记录笔记。
    }
}

public class PDA : ElectronicDevice, IRecordable
{
    public void TakeNote(string note)
    {
        // 用拇指或手写笔记录笔记。
    }
}
```

类 PDA继承自一个基类并实现了一个接口。

# 然后，重点来了

为了开始看到像 IRecordable 这样的接口的用，，考虑这个示例：

```sharp
public class Program
{
    static public void RecordShoppingList(IRecordable recorder)
    {
        // 使用传入的任何设备记录下来。
        recorder.TakeNote(...);
    }
    public static void Main(string[] args)
    {
        PDA pda = new PDA();
        RecordShoppingList(pda); // 哎呀，电量低了...
        RecordShoppingList(pen);
    }
}
```

IRecordable 是实现 IRecordable 接口的类的实例。RecordShoppingList() 对录制对象的具体类型没有任何假设。设备是 PDA 还是某种 ElectronicDevice 类型并不重要，只要该设备可以记录笔记即可。

这个概念非常强大，因为它让 RecordShoppingList 方法具有高度的通用性，从而可能在其他程序中重用。该方法甚至比使用基类 ElectronicDevice 作为参数类型更通用，因为接口允许你传递几乎任意的对象，这些对象除了实现接口之外，并不一定有任何其他共同点。

# 338 使用接口

程序员在多种方式上使用“接口”一词。你可以看到 C# 关键字 `interface` 以及它是如何被使用的。人们还会讨论类的公共接口，即它暴露给外部世界的公共方法和属性。每当我指代 C# 接口时，大多数时候会说“C# interface”，而在我指的是类的一组方法时，说“公共接口”（public interface），以保持区分清晰。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_363_0.png)

C# 结构体可以像类一样实现接口。

# 使用接口

除了你可以将 C# 接口作为参数类型外，接口在以下方面也很有用：

- 方法返回值类型
- 高度通用数组或集合的基类型
- 变量类型中更通用的对象引用类型

我在上一节中解释了使用 C# 接口作为方法参数类型的优势。现在我告诉你其他接口的用法。

# 作为方法的返回值类型

我喜欢将创建我所需的关键对象的任务交给一个工厂方法。假设我有这样一个变量：

```csharp
IRecordable recorder = null; // 是的，你可以拥有接口类型的变量。
```

在某处，也许在我的构造函数中，我调用工厂方法来交付特定类型的 IRecordable 对象：

```csharp
recorder = MyClass.CreateRecorder('Pen'); // 工厂方法是静态的。
```

其中 CreateRecorder() 是一个方法（通常在同一个类中），返回的不是 Pen 的引用，而是一个 IRecordable 的引用：

```csharp
static IRecordable CreateRecorder(string recorderType)
{
    if(recorderType == "Pen") return new Pen();
}
```

我会在本章稍后的部分详细介绍关于工厂的想法。但请注意，CreateRecorder() 的返回类型是一个接口类型。

# 作为数组或集合的基类型

假设你有两个类，Animal 和 Robot，且它们都是抽象的。你想设置一个数组来同时持有 thisCat（一个 Animal）和 thatRobot（一个可爱的机器人）。唯一的方法是退而求 `Object` 类型，它是 C# 中的终极基类，也是 Animal 和 Robot 及其子类共同拥有的唯一基类：

```csharp
object[] things = new object[] { thisCat, thatRobot };
```

由于许多原因，这种设计很糟糕。但假设你关注的是对象的移动。你可以让每个类实现 IMovable：

```csharp
interface IMovable
{
  void Move(int direction, int speed, int distance);
}
```

然后设置一个 IMovables 数组来操作这些原本不兼容的对象：

```csharp
IMovable[] movables = { thisCat, thatRobot };
```

接口为你提供了一种你可以在集合中利用的共性。

# 作为更通用的对象引用类型

下面的变量声明引用一个特定的、物理的实体对象（参见后文“抽象或具体：何时使用抽象类以及何时使用接口”）：

```csharp
Cat thisCat = new Cat();
```

另一种方案是使用 C# 接口作为引用：

```csharp
IMovable thisMoveCat = (IMovable)new Cat(); // 注意这里强制强制转换。
```

你可以将任何实现 IMovable 的对象放入变量中。这种做法在面向对象的编程中有广泛且强大的用途，你可以在这一章中看到它。

# 使用 C# 预定义接口类型

由于接口极其有用，你在 .NET 类库中发现接口比 NRA 大会上的枪架还要多。在感到疲劳和压力大之前，我在帮助文件中数了数十个。仅在 System 命名空间的十几个接口中，就包括 IComparable、IComparable<T>、IDisposable 和 IFormatable。System.Collections.Generics

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_364_0.png)

# 340 查看一个可以作为示例的程序

namespace IEnumerable<T>, IList<T>, ICollection<T>, 和 IDictionary<TKey, TValue>。还有更多。带有 <T> 符号的是泛型接口。我在第一本书第 6 节关于集合类的讨论中解释了 <T> 符号。

帮助文档（File）包含了所有添加了小撇标记的 IEquatable<T>（List<T>'），但请在帮助索引中查找 "IList<T>"。

本章中常用的两个接口。IComparable —— 很大程度上被它们的泛型版本 IComparable<T>（读作 "Comparable of T"）和 IEnumerable<T> 所代。

在本章中向你展示了 IComparable<T> 接口。它使得各种对象（如 Students）之间的比较成为可能，并启用了 Sort() 方法。IEnumerable<T> 让数组和集合支持 foreach 迭代。

# 查看一个可以作为示例的程序

接口的实现非常特殊。我想把 SortInterface 程序拆分成若干部分，以展示其工作原理。

```sharp
// 任何实现 Display 方法的接口
interface IDisplayable
{
    // 返回对象自己的描述。
    string Display();
}
```

# 创建你自己的接口

下面的 IDisplayable 接口由任何包含 Display() 方法的类满足。Display() 返回对象的字符串表示，可以使用 WriteLine() 显示。

```sharp
// Student 类实现了 IDisplayable
class Student : IDisplayable
{
    public Student(string name, double grade)
        Name = name; Grade = grade;
    public string Name { get; private set; }
    public double Grade { get; private set; }
    public string Display()
    {
        string packageName = Name.PadRight(9);
        return String.Format("{0}: {1:NO0}", packageName, Grade);
    }
}
```

Display() 使用 String() 和 Format() 方法（第一本书第 3 节）返回一个格式良好的字符串。

下面的 DisplayArray() 方法接收一个实现 IDisplayable 接口的数组。这些对象中的每一个都保证（通过接口）拥有自己的 Display() 方法（整个程序出现在“汇总”部分）：

```csharp
// DisplayArray -- 显示一个实现
// IDisplayable 接口的数组。
public static void DisplayArray(IDisplayable[] displays)
{
    foreach(IDisplayable disp in displays)
    {
        Console.WriteLine("{0}: {1}", disp.Display());
    }
}
```

下面的示例显示了 DisplayArray() 的输出：

```
Homer : 0
Marge : 85
Bart : 50
Lisa : 100
Maggio : 30
```
