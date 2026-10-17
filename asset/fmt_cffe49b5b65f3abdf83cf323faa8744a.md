
```csharp
while (enumerator.MoveNext())
{
    number = enumerator.Current;
    Console.WriteLine(number);
}
}
finally
{
    // 用于 IEnumerator<T> 的显式强制转换
    disposable = (IDisposable) enumerator;
    disposable.Dispose();
    // 除非在编译时已知支持 IDisposable，否则 IEnumerator 将使用 as 运算符
    // disposable = (enumerator as IDisposable);
    // if (disposable != null) 
    // {
    //     disposable.Dispose();
    // }
}
```

请注意，由于 `IDisposable` 接口受 `IEnumerator<T>` 支持，`using` 语句可以将清单 15.7 中的代码简化为清单 15.8 中所示的形式。

### 清单 15.8：使用 using 进行错误处理和资源清理

```csharp
System.Collections.Generic.Stack<int> stack =
new System.Collections.Generic.Stack<int>();
int number;
using(
System.Collections.Generic.Stack<int>.Enumerator enumerator = stack.GetEnumerator())
{
while (enumerator.MoveNext())
{
number = enumerator.Current;
Console.WriteLine(number);
}
}
```

然而，请记住 CIL 并不直接支持 `using` 关键字。因此，清单 15.7 中的代码实际上是 `foreach` CIL 代码更准确的 C# 表示形式。

## 进阶主题：没有 IEnumerable 的 foreach

C# 并不要求实现 `IEnumerable`/`IEnumerable<T>` 才能使用 `foreach` 迭代数据类型。相反，编译器使用一种称为**鸭子类型**的概念；它寻找一个返回具有 `Current` 属性和 `MoveNext()` 方法的类型的 `GetEnumerator()` 方法。鸭子类型涉及按名称搜索，而不是依赖接口或对方法的显式调用。（“鸭子类型”这个名称源于一个异想天开的想法：要被当作鸭子，对象只需实现一个 `Quack()` 方法即可；它无需实现 `IDuck` 接口。）如果鸭子类型未能找到可枚举模式的合适实现，编译器将检查该集合是否实现了这些接口。

## 在 foreach 迭代过程中不要修改集合

第 4 章指出，编译器禁止对 foreach 变量（`number`）进行赋值。正如清单 15.7 所示，对 `number` 的赋值并不会改变集合元素本身，因此 C# 编译器完全禁止此类赋值。

此外，在 foreach 循环执行期间，通常既不能修改集合中的元素数量，也不能修改元素本身。例如，如果在 foreach 循环内部调用 `stack.Push(42)`，那么迭代器是否应该忽略或纳入对 `stack` 的这一更改将会变得模糊不清——换句话说，迭代器是应该遍历新添加的元素，还是应该忽略该更改并假定其状态与实例化时相同。

由于这种模糊性，如果在 foreach 循环中修改了集合，通常在访问枚举器时会抛出类型为 `System.InvalidOperationException` 的异常，并报告该集合在枚举器实例化之后已被修改。

### 标准查询运算符

除了 `System.Object` 上的方法外，任何实现了 `IEnumerable<T>` 的类型都只需要再实现一个方法，即 `GetEnumerator()`。然而，这样做使得所有实现 `IEnumerable<T>` 的类型都可以使用 50 多个方法（不包括任何重载），而这甚至不需要显式实现除 `GetEnumerator()` 方法以外的任何方法。这些额外功能是通过 C# 3.0 的扩展方法提供的，并且位于类 `System.Linq.Enumerable` 中。因此，只需包含 `System.Linq` 的 `using` 声明即可使这些方法可用。

`IEnumerable<T>` 上的每个方法都是一个标准查询运算符；它提供了对其所操作的集合的查询能力。在以下几节中，我们将考察其中一些最突出的标准查询运算符。这些示例中的许多将依赖于 `Inventor` 和/或 `Patent` 类，这两个类都定义在清单 15.9 中。

![](img/ef6a8a417630b222bfb3f3b949facff0_649_0.png)

### 清单 15.9：用于标准查询运算符的示例类

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
public class Patent
{
    // Title of the published application
    public string Title { get; set; }
    // The date the application was officially published
    public string YearOfPublication { get; set; }
    // A unique number assigned to published applications
    public string ApplicationNumber { get; set; }
    public long[] InventorIds { get; set; }
    public override string ToString()
    {
        return $"{ Title } ({ YearOfPublication })";
    }
}
public class Inventor
{
    public long Id { get; set; }
    public string Name { get; set; }
    public string City { get; set; }
    public string State { get; set; }
    public string Country { get; set; }
    public override string ToString()
    {
        return $"{ Name } ({ City }, { State })";
    }
}
class Program
{
    static void Main()
    {
        IEnumerable<Patent> patents = PatentData.Patents;
        Print(patents);
        Console.WriteLine();
        IEnumerable<Inventor> inventors = PatentData.Inventors;
        Print(inventors);
    }
    private static void Print<T>(IEnumerable<T> items)
    {
        foreach (T item in items)
        {
            Console.WriteLine(item);
        }
    }
}
public static class PatentData
{
    public static readonly Inventor[] Inventors = new Inventor[]
    {
        new Inventor(){
            Name="Benjamin Franklin", City="Philadelphia",
            State="PA", Country="USA", Id=1 },
        new Inventor(){
            Name="Orville Wright", City="Kitty Hawk",
            State="NC", Country="USA", Id=2},
        new Inventor(){
            Name="Wilbur Wright", City="Kitty Hawk",
            State="NC", Country="USA", Id=3},
        new Inventor(){
            Name="Samuel Morse", City="New York",
            State="NY", Country="USA", Id=4},
        new Inventor(){
            Name="George Stephenson", City="Wylam",
            State="Northumberland", Country="UK", Id=5},
        new Inventor(){
            Name="John Michaelis", City="Chicago",
            State="IL", Country="USA", Id=6},
        new Inventor(){
            Name="Mary Phelps Jacob", City="New York",
            State="NY", Country="USA", Id=7},
    };
    public static readonly Patent[] Patents = new Patent[]
    {
        new Patent(){
            Title="Bifocals", YearOfPublication="1784",
            InventorIds=new long[] {1}},
        new Patent(){
            Title="Phonograph", YearOfPublication="1877",
            InventorIds=new long[] {1}},
        new Patent(){
            Title="Kinetoscope", YearOfPublication="1888",
            InventorIds=new long[] {1}},
        new Patent(){
            Title="Electrical Telegraph",
            YearOfPublication="1837",
            InventorIds=new long[] {4},
        },
        new Patent(){
            Title="Flying Machine", YearOfPublication="1903",
            InventorIds=new long[]{2,3}},
        new Patent(){
            Title="Steam Locomotive",
            YearOfPublication="1815",
            InventorIds=new long[]{5}},
        new Patent(){
            Title="Droplet Deposition Apparatus",
            YearOfPublication="1989",
            InventorIds=new long[]{6}},
        new Patent(){
            Title="Backless Brassiere",
            YearOfPublication="1914",
            InventorIds=new long[]{7}},
    };
}
```

清单 15.9 还提供了一些示例数据。输出 15.1 显示了运行此代码的结果。

### 输出 15.1

```text
Bifocals (1784)
Phonograph (1877)
Kinetoscope (1888)
Electrical Telegraph (1837)
Flying Machine (1903)
Steam Locomotive (1815)
Droplet Deposition Apparatus (1989)
Backless Brassiere (1914)
Benjamin Franklin (Philadelphia, PA)
Orville Wright (Kitty Hawk, NC)
Wilbur Wright (Kitty Hawk, NC)
Samuel Morse (New York, NY)
George Stephenson (Wylam, Northumberland)
John Michaelis (Chicago, IL)
Mary Phelps Jacob (New York, NY)
```

## 使用 Where() 进行筛选

要从集合中筛选数据，我们需要提供一个返回 true 或 false 的筛选方法，以指示某个特定元素是否应被包含。接受一个参数并返回布尔值的委托表达式被称为**谓词**，而集合的 `Where()` 方法依赖于谓词来确定筛选条件，如清单 15.10 所示。（从技术上讲，`Where()` 方法的结果是一个**对象**，它封装了使用给定谓词筛选给定序列的操作。）结果如输出 15.2 所示。

### 清单 15.10：使用 System.Linq.Enumerable.Where() 进行筛选

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
class Program
{
    static void Main()
    {
        IEnumerable<Patent> patents = PatentData.Patents;
        patents = patents.Where(
            patent => patent.YearOfPublication.StartsWith("18"));
        Print(patents);
    }
    // ...
}
```

### 输出 15.2

```text
Phonograph (1877)
Kinetoscope (1888)
Electrical Telegraph (1837)
Steam Locomotive (1815)
```

请注意，代码将 `Where()` 调用的输出重新赋值给 `IEnumerable<T>`。换句话说，`IEnumerable<T>.Where()` 的输出是一个新的 `IEnumerable<T>` 集合。在清单 15.10 中，它是 `IEnumerable<Patent>`。

一个不那么明显的事实是，`Where()` 表达式的参数并不一定在赋值时就已经执行。这对于许多标准查询运算符都是正确的。以 `Where()` 为例，表达式会被传入集合并被“保存”但尚未执行。相反，只有当需要开始迭代集合中的项目时，表达式的执行才会发生。例如，像清单 15.9 中 `Print()` 方法里的 `foreach` 循环，将触发针对集合中每个项目对该表达式求值。至少在概念上，`Where()` 方法应被理解为一种指定查询的手段，即关于集合中应包含什么内容，而不是实际涉及迭代以生成可能包含更少项目的新集合的工作。

## 使用 Select() 进行投影

由于 `IEnumerable<T>.Where()` 方法的输出是一个新的 `IEnumerable<T>` 集合，因此可以在同一集合上再次调用标准查询运算符。例如，我们不仅可以简单地从原始集合中过滤数据，还可以转换数据（参见列表 15.11）。

### 列表 15.11：使用 System.Linq.Enumerable.Select() 进行投影

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
class Program
{
    static void Main()
    {
        IEnumerable<Patent> patents = PatentData.Patents;
        IEnumerable<Patent> patentsOf1800 = patents.Where(
            patent => patent.YearOfPublication.StartsWith("18"));
        IEnumerable<string> items = patentsOf1800.Select(
            patent => patent.ToString());
        Print(items);
    }
```
