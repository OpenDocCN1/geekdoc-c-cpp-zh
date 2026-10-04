

```cs
private readonly tn fn;
public tn get { return fn; }
```

```cs
public <?>f_AnonymousType<...>(tl a1, ..., tn an) {
    fl1 = a1; ... fn = an; // 设置所有字段
}
```

```cs
public override Boolean Equals(Object value) {
    // 如果任何字段不匹配，则返回 false；
}
```

```cs
public override Int32 GetHashCode() {
    // 返回从每个字段生成的哈希值
}
```

```cs
public override String ToString() {
    // 返回逗号分隔的属性名 = 值对集合
}
```

编译器会生成 Equals 和 GetHashCode 方法，以便匿名类型的实例可以被放置在哈希表中。属性是只读的，而不是可读/可写的，以防止对象的哈希值发生变化。更改用于哈希表的对象的哈希值可能会无法找到该对象。编译器会生成 ToString 方法以帮助调试。在 Visual Studio 调试器中，你可以将鼠标光标悬停在引用匿名类型的变量上，Visual Studio 将调用 ToString 方法并在数据提示窗口中显示结果字符串。顺便说一下，Visual Studio 的 IntelliSense 会在编辑器中编写代码时建议属性——这是一个非常棒的功能。

编译器支持两种匿名语法，用于在匿名类型内部声明属性，它可以从变量中推导出属性名称和类型。

```cs
String Name = "Grant";
DateTime dt = DateTime.Now;
```

```cs
// 具有两个属性的匿名类型
// 1. Name 属性设置为 Grant
// 2. Int32 Year 属性设置为 dt 的 Year
var o2 = new { Name, Year = dt.Year };
```

在这个示例中，编译器确定第一个属性应该命名为 Name。因为 Name 是局部变量的名称，编译器将属性的类型设置为与局部变量相同的类型：String。对于第二个属性，编译器使用字段/属性的类型：Year 是 DateTime 类的一个 Int32 属性，因此匿名类型中的 Year 属性也将是 Int32。现在，当编译器构造此匿名类型的实例时，它将该实例的 Name 属性设置为与 Name 局部变量相同的值，因此 Name 属性将返回相同的 "Grant" 字符串。编译器将该实例的 Year 属性设置为从 dt.Year 属性返回相同的值。

编译器在定义匿名类型方面非常智能。如果编译器发现你在源代码中定义了多个具有相同结构的匿名类型，编译器将仅为该匿名类型创建一个定义，并创建该类型的多个实例。我所说的“结构”是指匿名类型的每个属性具有相同的名称，并且这些名称按相同的顺序指定。在前面的的示例中，变量 o1 的类型和变量 o2 的类型将是相同的类型，因为这两行代码定义了一个具有 Name/String 属性和 Year/Int32 属性的匿名类型，且 Name 在 Year 之前。

由于两个变量是同一种类型，我们可以进行一些很酷的操作，例如检查两个对象是否包含相等的值，并将一个对象的引用赋值给另一个对象的变量，例如。

```cs
// 同一类型允许相等和赋值操作。
Console.WriteLine("Objects are equal: " + o1.Equals(o2));
o1 = o2; // 赋值
```

此外，通过这种类型标识性，我们可以创建一个匿名类型的隐式类型数组（在第16章“数组”的“初始化数组元素”部分中讨论过）。

```cs
// 这可以工作，因为所有对象都是同一种匿名类型
var people = new[] {
  new { Name = "Kristin", Year = 1970 },
  new { Name = "Aidan", Year = 2003 },
  new { Name = "Grant", Year = 2008 }
};
```

```cs
// 这展示了如何遍历匿名类型数组（需要使用 var）
foreach (var person in people)
    Console.WriteLine("Person:{0}, Year={1}", person.Name, person.Year);
```

匿名类型最常用的是语言集成查询 (LINQ) 技术，在该技术中，你对一个全是相同匿名类型的对象集合进行查询。然后，你处理结果集合中的对象。所有这一切都在同一个方法中完成。这里的示例返回了我的文档目录中过去七天内修改过的文件。

```cs
String myDocuments = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
var query =
  from path in Directory.GetFiles(myDocuments)
  let LastWriteTime = File.GetLastWriteTime(path)
  where LastWriteTime > (DateTime.Now - TimeSpan.Days(7))
  orderby LastWriteTime
  select new { Path = path, LastWriteTime=LastWriteTime }; // 匿名类型对象集合
```

```cs
foreach (var file in query)
    Console.WriteLine("LastWriteTime={0}, File={1}", file.LastWriteTime, file.Path);
```

第 10 章 属性 239

匿名类型的实例不应该泄漏到方法之外。方法不能被原型化为匿名类型，因为没有办法可以指定匿名类型。同样，方法无法指示它返回一个匿名类型的引用。虽然可以将匿名类型的实例视为 Object（因为所有匿名类型都派生自 Object），但没有方法可以将 Object 类型的变量转换回匿名类型，因为你无法编译时并不知道匿名类型的名称。如果你想传递元组（tuple），那么你应该考虑使用下一节中讨论的 System.Tuple 类型。

# System.Tuple 类型

在 System 命名空间中，微软提供了几种泛型 Tuple 类型（全部派自 Object），它们在元数（泛型参数的数量）上有所不同。以下是最简单和最复杂的类型本质的样子。

```cs
// 这是最简单的：
[Serializable]
public class Tuple<T1> {
    private T1 m_item1;
    public Tuple(T1 item1) { m_item1 = item1; }
    public T1 Item1 { get { return m_item1; } }
}

// 这是最复杂的：
[Serializable]
public class Tuple<T1, T2, T3, T4, T5, T6, T7, TRest> {
    private T1 m_item1; private T2 m_item2; private T3 m_item3; private T4 m_item4;
// (其余代码遵循该模式)
```

```cs
// ... (Tuple 类定义的其余部分)
    public T1 Item1 { get { return m_item1; }
    public T2 Item2 { get { return m_item2; }
    public T3 Item3 { get { return m_item3; }
    public T4 Item4 { get { return m_item4; }
    public T5 Item5 { get { return m_item5; }
    public T6 Item6 { get { return m_item6; }
    public T7 Item7 { get { return m_item7; }
    public TRest Rest { get { return m_rest; }
}
```

和匿名类型一样，在 Tuple 创建后，它是不可变的（所有属性都是只读的）。此外，Tuple 类实现了 IStructuralEquatable 和 IStructuralComparable，因此你可以相互比较 Tuple 对象。请参考 SDK 文档以了解更多关于这些方法的信息。这里有一个使用 Tuple 返回两个信息的示例。

```cs
// 在 Item1 中返回最小值，在 Item2 中返回最大值
private static Tuple<Int32, Int32> MinMax(Int32 a, Int32 b) {
    return new Tuple<Int32, Int32>(Math.Min(a, b), Math.Max(a, b));
}
```

```cs
// 展示了如何调用该方法以及返回的 Tuple
private static void TupleTypes() {
    var min = MinMax(6, 2);
    Console.WriteLine("Min={0}, Max={1}", min.Item1, min.Item2); // Min=2, Max=6
}
```

当然，Tuple 的生产者和消费者对返回的属性有清晰的是非常重要的。对于匿名类型，属性是从定义匿名类型的源代码中赋予实际名称。对于 Tuple 类型，属性由微软分配为 Item# 名称，你完全无法更改。遗憾的是，这些名称没有意义或重要性，因此需要生产者和消费者为其赋予意义。这还需要对你的代码进行注释。

编译器只有在调用泛型方法时才能推断泛型，而在调用构造函数时不能。由于这个原因，System 命名空间包含一个非泛型的静态 Tuple 类，其中包含许多从参数推断泛型的静态方法。该类作为创建 Tuple 对象的工厂，它的存在是为了简化你的代码。这里是使用静态 Tuple 类对之前的 MinMax 方法进行的重写。

```cs
// 在 Item1 中返回最小值，在 Item2 中返回最大值
private static Tuple<Int32, Int32> MinMax(Int32 a, Int32 b) {
    return Tuple.Create(Math.Min(a, b), Math.Max(a, b)); // 更简单的语法
}
```

如果你想创建一个超过六个元素的 Tuple，你需要按照如下方式为剩余参数传递 Tuple：

```cs
var t = Tuple.Create(0, 1, 2, 3, 4, 5, 6, Tuple.Create(7, 8));
Console.WriteLine("{0}, {1}, {2}, {3}, {4}, {5}, {6}, {7}, {8}",
t.Item1, t.Item2, t.Item3, t.Item4, t.Item5, t.Item6, t.Item7,
t.Rest.Item1, t.Rest.Item2);
```

