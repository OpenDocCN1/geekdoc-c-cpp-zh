
```csharp
override public void TakeANote(string note)
{
    // ... 在 PDA 上划写笔记 ...
}
}

public class LapTop : ThingsThatRecord  // 第三个子类
{
    override public void TakeANote(string note)
    {
        // ... 哒、哒、哒 ...
    }
}
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_355_0.png)

如果你对 *abstract*（抽象）一词感到困惑，请参阅本微读本的第 7 章，并阅读本章后面“抽象或具体：何时使用抽象类以及何时使用接口”章节中的讨论。如果整个继承的概念还是个谜团，请查看本微读本的第 6 章。

下面的简单方法展示了继承方法运行良好：

```csharp
void RecordTask(ThingsThatRecord recorder)  // 参数类型是基类。
{
    // 所有扩展 ThingsThatRecord 的类都有 TakeANote 方法。
    recorder.TakeANote("Shopping list");
    // ... 以此类推。
}
```

参数类型是 `ThingsThatRecord`，因此你可以将任何子类传递给此方法，使该方法非常通用。

这看起来像是一个很好的解决方案，但它有两个巨大的缺点：

- **根本性问题**：Pen、PDA 和 LapTop 真的具有 IS_A 关系吗？在现实生活中，这三件物品都是同一种类型吗？我不这么认为，你呢？我只能说，`ThingsThatRecord` 在这里是一个糟糕的基类。
- **纯技术问题**：你可能会合情地将 LapTop 和 PDA 都派生为 Computer 的子类。但没有人会说笔 IS_A 电脑。你必须将笔归类为机械书写设备或会弄脏你衣服的设备。但一个 C# 类不能同时继承两个不同的基类——一个 C# 类只能是一种类型的物品。

所以，Pen、PDA 和 LapTop 类唯一的共同点是它们 CAN_BE_USED_AS 记录设备。继承并不适用。

## 了解什么是接口

C# 中的 *interface*（接口）类似于一个没有数据成员且仅有抽象方法的类，几乎就像一个抽象类——“几乎”：

```csharp
interface IRecordable
{
    void TakeANote(string note);
}
```

接口以 `interface` 关键字开头。它除了抽象方法外什么都不包含。它没有数据成员也没有实现的方法。

接口可以包含其他一些特性，包括属性（在本微读本第 5 章介绍）、事件（在本微读本第 9 章介绍）和索引器（在本书第 7 章介绍）。

C# 接口*不能*展示的元素包括：

- 访问修饰符，例如 `public` 或 `private`（参见本微读本第 5 章）
- 关键字如 `virtual`、`override` 或 `abstract`（参见本微读本第 7 章）
- 数据成员（参见本微读本第 2 章）
- 实现的方法——带有主体的非抽象方法

C# 接口的所有成员都是公共的（你甚至不能在定义接口方法时提到访问修饰符），而且 C# 接口不参与普通的继承；因此，它没有所有这些关键字。（接口本身可以是 `public`、`protected`、`internal` 或 `private`。）

与抽象类不同，C# 接口不是类。它不能被子类化，它包含的任何方法都不能有方法体。

## 如何实现接口

要使用 C# 接口，你需要用一个或多个类来对其进行*实现*。类的头部如下所示：

```csharp
class Pen : IRecordable  // 看起来像继承，但其实不是
```

C# 接口规定，实现接口的类*必须*提供特定的实现。它们*必须*提供。例如，任何实现 `IRecordable` 接口的类都必须为以下内容提供实现

这个概念非常强大，因为它让 `RecordShoppingList()` 方法能够具有极高的通用性——从而可能在其他程序中被重用。该方法比使用如 `ElectronicDevice` 的基类作为参数类型更为通用，因为接口允许你传递几乎任意的对象，这些对象除了实现了接口外，并不一定有任何共同点。它们甚至不需要来自同一个类层次结构，这在某些情况下（例如）真的极大简化了层次结构的设计。

过度使用的词汇警示：程序员在多种方式上使用“接口（interface）”一词。你可以看到 C# 关键字 `interface` 以及它是如何被使用的。人们还会讨论一个类的公共接口（public interface），即它暴露给外部的公共方法和属性。为了保持这种区别的清晰，当我指的是 C# 接口时，大部分都会说 C# interface，而当我指的是类的一组公共方法时，我会说 public interface。

C# 结构体（structs）也可以像类一样实现接口。

## 使用接口

除了你可以将 C# 接口作为参数类型外，接口在以下方面也很有用：

- 方法返回值类型
- 高通用数组或集合的基类型
- 变量类型更通用的对象引用

我在上一个节中解释了将 C# 接口作为方法参数类型的优势。现在我可以告诉你接口的其他用途。

### 作为方法的返回值类型

我喜欢通过一个工厂方法（factory method）来完成创建我所需的关键对象的任务。假设我有像下面这样的变量：

```csharp
IRecordable recorder = null;  // 是的，你可以接口类型的变量。
```

在某个地方，也许在我的构造函数中，我调用一个工厂方法来交付特定类型的 `IRecorable` 对象：

```csharp
recorder = MyClass.CreateRecorder("Pen");  // 工厂方法通常是静态的。
```

其中 `CreateRecorder()` 是一个方法（通常在同一个类中），它返回的不是 `Pen` 的引用，而是一个 `IRecorable` 引用：

![](img/6df7bb88e9302e98442acc219cfbd7fc_359_0.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_359_1.png)

```csharp
static IRecordable CreateRecorder(string recorderType)
{
    if(recorderType == "Pen") return new Pen();
    ...
}
```

我在本章后面的“隐藏在接口之后”节中会详细介绍工厂的想法。但请注意，`CreateRecorder()` 的返回值类型是一个接口类型。

### 作为数组或集合的基类型

假设你有两个类，`Animal` 和 `Robot`，并且它们都是抽象的。你想设置一个数组来同时持有 `thisCat`（一个 `Animal`）和 `thatRobot`（一个可爱的机器人）。唯一的方法是回到 `Object` 类型，它是 C# 中的终极基类，也是 `Animal` 和 `Robot` 及其子类共同唯一的基类：

```csharp
object[] things = new object[] { thisCat, thatRobot };
```

出于很多原因，这是很糟糕的设计。但假设你专注于对象的移动。你可以让每个类都实现一个 `IMovable` 接口：

```csharp
interface IMovable
{
    void Move(int direction, int speed, int distance);
}
```

然后设置一个 `IMovable` 数组来操作你这些原本不兼容的对象：

```csharp
IMovable[] movables = { thisCat, thatRobot };
```

接口为你提供了一个可以在集合中利用的共同性。

### 作为更通用的对象引用类型

下面的变量声明引用了一个特定的、物理的、具体的对象（参见后文节“抽象或具体：何时使用抽象类以及何时使用接口”）：

```csharp
Cat thisCat = new Cat();
```

另一种替代方案是使用 C# 接口作为引用：

```csharp
IMovable thisMovableCat = (IMovable)new Cat();  // 注意这里需要强制类型转换。
```

现在，你可以将任何实现 `IMovable` 的对象放入该变量中。这种做法在面向对象的编程中具有广泛且强大的用途，正如你在下一节中看到的。

## 使用 C# 预定义接口类型

由于接口极其有用，你在 .NET 类库中发现的接口比 NRA 大会上的枪架还要多。我在帮助文档（Help）中数了数十个，直到我累了停下来。。仅在 `System` 命名空间中的十几个接口中就包括 `IComparable`、`IComparable<T>` 和 `IDisposable`。`System.Collections.Generic` 命名空间包含了 `IEnumerable<T>`、`IList<T>`、`ICollection<T>` 和 `IDictionary<Key, TValue>`。还有更多。带有 `<T>` 符号的是泛型接口。

![](img/6df7bb88e9302e98442acc219cfbd7fc_361_0.png)

两个常用的接口是 `IComparable` 和 `IEnumerable` —— 它们现在很大程度上被泛型版本 `IComparable<T>` 和 `IEnumerable<T>` 取代。我在本章后面的“实现 IComparable<T> 接口”节向你展示 `IComparable<T>` 接口。它使得所有对象（如 `Students`）之间的比较成为可能，并启用了所有集合提供的 `Sort()` 方法。`IEnumerable<T>` 使得强大的 `foreach` 循环成为可能，你可以使用 `foreach` 迭代集合。你可以发现 `IEnumerable<T>` 的另一个用途是作为新的 C# 查询表达式的as。你也可以在 http://csharp.info 上阅读更多关于 LINQ 的知识。

## 查看作为示例的程序

下面的 `Sort` 程序是一个特例。不同接口带给能力在任何继承关系中都是无法的。然而，我想将 `Sort` 程序拆分成几个部分，以演示各种原理。（噗！就好像我有什么原理一样，我只是想确保你能确切地看到程序是如何工作的。）

## 创建你自己的接口

下面的 `IDisplayable` 接口由任何包含 `Display()` 方法的类满足（当然还要声明它实现了 `IDisplayable`）。`Display()` 返回对象的字符串表示，可以使用 `()` 进行显示。

```csharp
// IDisplayable -- 任何实现了 Display() 方法的对象
interface IDisplayable
{
    // 返回你自己的描述。
    string Display();
}
```

下面的 `Student` 类实现了 `IDisplayable`：

```csharp
class Student : IDisplayable
{
    public Student(string name, double grade) { Name = name; Grade = grade; }
    public string Name { get; set; }
    public double Grade { get; set; }
    public string Display()
    {
        string padName = Name.PadRight(9);
        return String.Format("{0}: {1:N0}", padName, Grade);
    }
}
```

`Display()` 使用了第 3 章涵盖的 `String` 的 `PadRight()` 和 `Format()` 方法来返回一个格式整齐的字符串。下面的 `DisplayArray()` 方法接收任何实现了 `IDisplayable` 接口的对象的数组。这些每个对象都保证（通过接口）拥有自己的 `Display()` 方法（整个程序出现在后面的节“将所有内容整合”）：

```csharp
// DisplayArray -- 一个实现了
// IDisplayable 接口的对象的数组。
public static void DisplayArray(IDisplayable[] displayables)
{
    foreach(IDisplayable disp in displayables)
    {
        Console.WriteLine("{0}", disp.Display());
    }
}
```

下面的示例显示了 `DisplayArray()` 的输出：

```
Homer: 0
Marge: 85
Bart: 50
Lisa: 100
Maggie: 30
```

注意：`DisplayArray()` 不是任何示例程序的一部分。

## 实现 IComparable<T> 接口

C# 这样定义 `IComparable<T>` 接口：

```csharp
interface IComparable<T>
{
    // 将当前 T 对象与 item 对象进行比较；
    // 如果较大返回 1，较小返回 -1，如果相同返回 0。
    int CompareTo(T item);
}
```

类通过实现 `CompareTo()` 方法来实现 `IComparable<T>` 接口。注意 `CompareTo()` 接收一个类型为 `T` 的参数，该类型是在实例化接口时提供的，如下例所示：

```csharp
class SoAndSo : IComparable<SoAndSo> // 使我可比较。
```

当你为类实现 `IComparable<T>` 时，它的 `CompareTo()` 方法在两个比较的项目（你的类类型）按你定义的方式“相等”时应返回 0。否则，它应该返回 1 或 -1，取决于哪个对象“更大”。

这听起来有点达尔文主义，但你可以说，如果一个 `Student` 对象的平均分更高，它比另一个 `Student` 对象“更大”。好吧，要么是更好的学生，要么是更好的擦苹果工——这并不重要。）

实现 `CompareTo()` 方法意味着对象具有排序。如果一个学生比另一个学生“大”，你必须能够对学生从“最小”到“最大”进行排序。事实上，大多数集合类（包括数组但不包括字典）都提供类似的 `Sort()` 方法：

```csharp
void Sort(IComparable<T>[] objects);
```

该方法排序实现了 `IComparable<T>` 接口的对象集合。它甚至不在乎这些对象属于哪个类。例如，它们甚至可以是 `Student` 对象。集合类如数组或 `List<T>` 甚至可以排序这个版本的 `Student`：

```csharp
// Student -- 带有名称和分数的学生描述
class Student : IComparable<Student>, IDisplayable // 实例化
```

```csharp
// 构造函数 -- 初始化一个新的学生对象。
public Student(double grade)
{ Grade = grade; }
public double Grade { get; private set; }
// 实现 IComparable<T> 接口：
// CompareTo -- 比较另一个对象（在本例中为 Student 对象）
// 并决定它们在排序数组中谁在另一个后面。
public int CompareTo(Student rightStudent)
{
    // 将当前的学生（称为 'left'）与另一个
    // 学生（称为 'right'）进行比较。
    Student leftStudent = this;
    // 现在根据排序准则（学生的成绩）生成 -1, 0 或 1。
    // 我也可以使用 Double 类的 CompareTo() 方法。
    if (rightStudent.Grade < leftStudent.Grade)
    {
        return -1;
    }
    if (rightStudent.Grade > leftStudent.Grade)
    {
        return 1;
    }
    return 0;
}
```

对 Students 数组进行排序简化为这一个调用：

```csharp
void MyMethod(Student[] students) // 其中 Student实现了 IComparable<T>
{
    Array.Sort(students); // 排序 IComparable<Student> 数组
}
```

你提供比较器（CompareTo()），而 Array 完成了所有工作——对我来说这很公平。

# 整合一切

这是你一直等待的时刻：完整的 SortInterface 程序，它使用了本章早些时候描述的功能：

![](img/6df7bb88e9302e98442acc219cfbd7fc_364_0.png)

```csharp
// SortInterface - 演示如何使用接口概念
//     在类的重构和实现中提供更高程度的灵活性。
using System;
namespace SortInterface
{
    // IDisplayable - 一个可以将自己转换为可显示
    //     字符串格式的对象。（这与你通过重写 ToString() 可以的操作重复，
    //     但它有助于我说明一个观点。）
    interface IDisplayable
