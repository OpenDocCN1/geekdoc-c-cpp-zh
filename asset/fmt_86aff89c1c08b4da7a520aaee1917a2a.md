
```csharp
recorder = MyClass.CreateRecorder('Pen'); // 工厂方法是静态的。
```

其中 `CreateRecorder()` 是一个方法（通常在同一个类中），返回的不是 `Pen` 的引用，而是一个 `IRecordable` 的引用：

```csharp
static IRecordable CreateRecorder(string recorderType)
{
    if(recorderType == "Pen") return new Pen();
}
```

我会在本章稍后的部分详细介绍关于工厂的想法。但请注意，`CreateRecorder()` 的返回类型是一个接口类型。

# 作为数组或集合的基类型

假设你有两个类，`Animal` 和 `Robot`，且它们都是抽象的。你想设置一个数组来同时持有 `thisCat`（一个 `Animal`）和 `thatRobot`（一个可爱的机器人）。唯一的方法是退而求 `Object` 类型，它是 C# 中的终极基类，也是 `Animal` 和 `Robot` 及其子类共同拥有的唯一基类：

```csharp
object[] things = new object[] { thisCat, thatRobot };
```

由于许多原因，这种设计很糟糕。但假设你关注的是对象的移动。你可以让每个类实现 `IMovable`：

```csharp
interface IMovable
{
  void Move(int direction, int speed, int distance);
}
```

然后设置一个 `IMovables` 数组来操作这些原本不兼容的对象：

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

你可以将任何实现 `IMovable` 的对象放入变量中。这种做法在面向对象的编程中有广泛且强大的用途，你可以在这一章中看到它。

# 使用 C# 预定义接口类型

由于接口极其有用，你在 .NET 类库中发现接口比 NRA 大会上的枪架还要多。在感到疲劳和压力大之前，我在帮助文件中数了数十个。仅在 `System` 命名空间的十几个接口中，就包括 `IComparable`、`IComparable<T>`、`IDisposable` 和 `IFormatable`。`System.Collections.Generics`

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_364_0.png)

# 340 查看一个可以作为示例的程序

`namespace IEnumerable<T>, IList<T>, ICollection<T>, 和 IDictionary<TKey, TValue>`。还有更多。带有 `<T>` 符号的是泛型接口。我在第一本书第 6 节关于集合类的讨论中解释了 `<T>` 符号。

帮助文档（File）包含了所有添加了小撇标记的 `IEquatable<T>`（`List<T>'`），但请在帮助索引中查找 "`IList<T>`"。

本章中常用的两个接口。`IComparable` —— 很大程度上被它们的泛型版本 `IComparable<T>`（读作 "Comparable of T"）和 `IEnumerable<T>` 所代。

在本章中向你展示了 `IComparable<T>` 接口。它使得各种对象（如 `Students`）之间的比较成为可能，并启用了 `Sort()` 方法。`IEnumerable<T>` 让数组和集合支持 `foreach` 迭代。

# 查看一个可以作为示例的程序

接口的实现非常特殊。我想把 `SortInterface` 程序拆分成若干部分，以展示其工作原理。

```sharp
// 任何实现 Display 方法的接口
interface IDisplayable
{
    // 返回对象自己的描述。
    string Display();
}
```

# 创建你自己的接口

下面的 `IDisplayable` 接口由任何包含 `Display()` 方法的类满足。`Display()` 返回对象的字符串表示，可以使用 `WriteLine()` 显示。

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

`Display()` 使用 `String()` 和 `Format()` 方法（第一本书第 3 节）返回一个格式良好的字符串。

下面的 `DisplayArray()` 方法接收一个实现 `IDisplayable` 接口的数组。这些对象中的每一个都保证（通过接口）拥有自己的 `Display()` 方法（整个程序出现在“汇总”部分）：

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

下面的示例显示了 `DisplayArray()` 的输出：

```
Homer : 0
Marge : 85
Bart : 50
Lisa : 100
Maggio : 30
```

## 342 查看一个可以作为示例的程序

类通过实现 `CompareTo()` 方法来实现 `Comparable<T>` 接口。注意 `CompareTo()` 接收一个类型为 `T` 的参数，这是你在为特定数据类型实例化接口时提供的类型——如本例所示：

```sharp
class SoAndSo : Comparable<SoAndSo> // 使我变得可比较。
```

这听起来有点像达尔文主义，但你可以说，如果一个 `Student` 对象的平均学分更高，那么它就“大于”另一个 `Student` 对象。（好吧，无论是一个更优秀的学生，还是一个更会拍马的人——这并不重要。）

实现 `CompareTo()` 方法意味着对象具有排序顺序。如果一个学生“大于”另一个学生，你必须能够将学生从“最小”到“最大”进行排序。事实上，大多数集合类（包括数组但不包括字典）都提供类似下面所示的 `Sort()` 方法：

```sharp
void Sort(Comparable<T> objects) {
```

此方法对实现了 `Comparable<T>` 接口的对象集合进行排序。这些对象属于哪个类并不重要。例如，它们可以是 `Student` 对象。像数组或 `List<T>` 这样的集合类甚至可以排序这个版本的 `Student`：

```sharp
// Student -- 带有名字和成绩的学生
class Student : Comparable<Student>, IDisplayable
{
    // 构造函数 -- 初始化一个新的学生对象。
    public Student(double grade)
        { Grade = grade;
    public double Grade { get; private set; }
    // 实现 Comparable<T> 接口：
    public int CompareTo(Student other)
    {
        // 比较另一个对象（在此类中为 Student 对象）并
        // 决定哪一个在排序中排在另一个后面。
        Student rightStudent = other;
        
        // 将当前的学生（设为 'left'）与另一个
        // 学生（设为 'right'）进行比较。
        Student leftStudent = this;

        // 现在根据排序标准（学生的成绩）生成 -1, 0 或 1。
        // 我也可以使用 Double 类的 CompareTo() 方法。
        {
            if (rightStudent.Grade < leftStudent.Grade)
                return -1;
        }
}
}
}
```

## 查看一个可以作为示例的程序 343

```sharp
if (rightStudent.Grade > leftStudent.Grade)
    return 1;
else
    return 0;
```

对 `Students` 数组进行排序被简化为这一个调用：

```sharp
void MyMethod(Student[] students) // Student 实现了 IComparable<T>
    Array.Sort(students); // 排序 IComparable<Student> 数组
```

你提供比较器（`CompareTo()`），而 `Array` 完成所有工作——对我来说这很公平。

## 整合一切

这是你一直等待的时刻：一个使用了本章之前描述的特完整接口程序：
