
`public static bool sameValue<T>(T a, T b) {`

    `if(a == b) return true; // 无法工作`

}

由于 `T` 是泛型类型，编译器无法知道如何对两个对象进行相等性比较。应该进行位比较吗？应该只比较某些字段吗？应该使用引用相等性吗？编译器无法回答这些问题。

## C# 3.0：学者指南

乍一看这似乎是一个严重的问题。幸运的是，并非如此，因为 C# 提供了一种机制，可以通过它可以判断两个类型参数的实例是否相同。要允许两个泛型类型的对象进行比较，请使用由标准接口之一 `IComparable` 定义的 `CompareTo()` 方法。该接口具有泛型和非泛型形式。所有 C# 内置类型（包括 `int`、`string` 和 `double`）都实现了 `IComparable`。对于你创建的类，也很实现。

`IComparable` 接口只定义了 `CompareTo()` 方法。其泛型形式所示：

```cs
int CompareTo(T obj)
```

它将调用对象与 `obj` 进行比较。如果两个对象相等，则返回零；如果调用对象大于 `obj`，返回正值；如果调用对象小于 `obj`，则返回负值。

要使用 `CompareTo()`，你必须指定一个约束，要求每个参数都实现 `IComparable` 接口。然后，当你需要比较两个类型参数类型的对象时，只需调用 `CompareTo()`。例如，这里是 `SameValue()` 的修正后版本：

```cs
// IComparable接口.
public static bool SameValue<T>(T a, T b) : IComparable<T> {
    if(a.CompareTo(b) == 0) return true; // 已修复
    return false;
}
```

由于接口约束要求 `T` 实现 `IComparable<T>`，可以使用 `CompareTo()` 方法来确定相等性。当然，这意味着只有实现了 `IComparable<T>` 的类实例可以传递给 `SameValue()`。

## 尝试创建一个泛型队列

在之前的章节中，你创建并增强了一个队列类。在那些章节中，在队列上操作的数据类型被硬编码为 `char`。通过使用泛型，你可以轻松地将队列类转换为可以操作任何类型数据的形式。这是本节的主题。

### 步骤

- 1. 创建一个名为 `IQ` 的泛型接口，它接受一个指定存储数据的类型参数：

```cs
// 泛型接口.
// 这里指定队列存储的数据类型.
public interface IQ<T> {
    void Put(T obj);
    T Get();
}
```

- 2. 包含异常类以便实现 `IQ`。

```cs
// 队列满异常.
class QueueFullException : Exception {
    public QueueFullException(string str) : base(str) {}
    public override string ToString() {
        return "\n" + Message;
    }
}

// 队列空异常.
class QueueEmptyException : Exception {
    public QueueEmptyException(string str) : base(str) {}
    public override string ToString() {
        return "\n" + Message;
    }
}
```

- 3. 修改 `SimpleQueue` 类以实现 `IQ`。

```cs
// 泛型固定大小队列类.
// 此类实现了 IQ 接口.
class SimpleQueue<T> : IQ<T> {
    T[] q;
    int putloc, getloc;
    // 给定大小构造空队列.
    public SimpleQueue(int size) {
        q = new T[size+1];
        putloc = 0;
    }
    // 将项放入队列.
    public void Put(T obj) {
        if(putloc==q.Length-1)
            throw new QueueFullException("队列满！最大长度为 " + (q.Length-1) + ".");
        putloc++;
        q[putloc] = obj;
    }
    // 从队列中获取项.
    public T Get() {
        if(getloc == putloc)
            throw new QueueEmptyException("队列为空.");
        getloc++;
        return q[getloc];
    }
}
```

- 4. 下面程序展示了泛型队列的操作：

```cs
// 演示泛型队列.
class GenQueueDemo {
    static void Main() {
        SimpleQueue<int> intQueue = new SimpleQueue<int>(5);
        intQueue.Put(10);
        intQueue.Put(20);
        Console.WriteLine(intQueue.Get());
        Console.WriteLine(intQueue.Get());
    }
}
```

## 502 C# 3.0: 初学者指南

```cs
// Create a queue for chars and a queue for doubles.
SimpleQueue<char> charQ = new SimpleQueue<char>(10);
SimpleQueue<double> doubleQ = new SimpleQueue<double>(5);
```

```cs
char ch;
double d;
int i;
```

```cs
try {
  // Use a queue.
  for(i=0; i < 10; i++) {
    Console.WriteLine(" " + (char) ('A' + i));
    charQ.Put((char) ('A' + i));
  }
  Console.WriteLine();
```

```cs
for(i=0; i < 10; i++) {
  Console.Write("Getting next char: ");
  ch = charQ.Get();
  Console.WriteLine(ch);
}
```

```cs
catch (QueueFullException exc) {
  Console.WriteLine(exc);
}
Console.WriteLine();
```

```cs
try {
  // Use a double queue.
  for(i=1; i <= 5; i++) {
    Console.Write(" " + i * 3.1416 );
    doubleQ.Put(i * 3.1416);
  }
  Console.WriteLine();
```

```cs
for(i=0; i < 5; i++) {
  Console.Write("Getting next double: ");
  d = doubleQ.Get();
  Console.WriteLine(d);
}
```

```cs
catch (QueueEmptyException exc) {
  Console.WriteLine(exc);
}
```

输出如下：

```
Storing: A
Storing: B
Storing: C
Storing: D
Storing: E
Storing: F
Storing: G
Storing: H
Storing: I
Storing: J
```

```
Getting next char: A
Getting next char: B
Getting next char: C
Getting next char: D
Getting next char: E
Getting next char: F
Getting next char: G
Getting next char: H
Getting next char: I
Getting next char: J
```

```
Storing: 3.1416
Storing: 6.2832
Storing: 9.4248
Storing: 12.5664
Storing: 15.708
```

```
Getting next double: 3.1416
Getting next double: 6.2832
Getting next double: 9.4248
Getting next double: 12.5664
Getting next double: 15.708
```

## 第 13 章自测

- 1. 泛型简化了以类型安全的方式处理各种类型数据的类的创建。正确或错误？
- 2. 什么是类型参数？
- 3. 什么是类型参数？
- 4. 正如所解释，在引入泛型之前，C# 已经通过使用对象引用来实现通用代码。这种方法的一个问题是与提供所需的强制类型转换时非常繁琐且容易出错。另一个问题是什么？
- 5. 基类约束的作用是什么什么？值类型约束的作用又是什么？
- 6. 接口可以是泛型的吗？
- 7. 如何为类型创建一个默认值？
- 8. 创建泛型方法时，类型参数列表是在哪里指定的？
- 9. 泛型方法可以使用类型约束吗？
- 10. 如前所述，虽然不能创建泛型属性，但属性可以使用其所在作用域内的类型参数。重构本中所示 ITwoDCoord 接口和 XYCoord 类，将 GetX() 和 GetY() 等方法转换为属性。

## 第 14 章

## 介绍 LINQ

### 关键技能与概念

- LINQ 基础
- 查询中的类型对应
- 使用 where 过滤值
- 使用 orderby 排序结果
- 使用 select 选择值
- 使用 group 分组结果
- 使用 into 创建延续
- 使用 join 关联两个序列
- 匿名类型和对象初始化器
- 创建分组连接 `group join`
- 使用 let 创建变量

如你所见，`nums` 数组中只显示了正值。尽管这个程序非常简单，但它展示了 LINQ 的核心特性。让我们仔细观察。
程序中首先要注意到的是 `using` 指令：

```
using System.Linq;
```

要使用 LINQ 特性，你必须包含 `System.Linq` 命名空间。
接下来，声明了一个名为 `nums` 的 `int` 类型的数组。C# 中的所有数组都可以隐式转换为 `IEnumerable<T>`。这使得任何 C# 数组都可以作为 LINQ 数据源。
接着，声明了一个查询，用于检索 `nums` 中的正数元素。显示如下：

```
var posNums = from n in nums
              where n > 0
              select n;
```

变量 `posNums` 被称为*query*（查询）变量。它引用了查询定义的规则集。注意它使用 `var` 来声明 `posNums`。如你所知，这使得 `posNums` 成为一个隐式类型变量。使用隐式类型变量通常很方便，尽管你也可以显式声明类型（该类型必须是某种形式的 `IEnumerable<T>`）。然后为变量 `posNums` 赋值查询表达式。
所有查询都以 `from` 开始。该子句指定了两项：第一个是*range*（范围）变量，它将接收来自数据源的元素；第二个项是数据源，在这种情况下是 `nums` 数组。范围变量的类型是从数据源推断出来的。在这种情况下，`n` 的类型是 `int`。泛化来说，这是 `from` 子句的语法: data-source

查询的下一个子句是 `where`。它指定了数据源中的元素必须满足的条件才能被查询获取。其通用格式如下：

```
where boolean-expression
```

`boolean-expression`（布尔表达式）必须产生 `bool` 结果。（此表达式也称为 *predicate*，谓词）。一个查询中可以有多个 `where` 子句。程序中使用了这个 `where`：

```
where n > 0
```

它仅对值大于零的元素结果为真。当查询执行时，此表达式将对 `nums` 中的每个 `n` 进行求值。只有满足此条件的值会被获取。换句话说，`where` 子句充当数据源的过滤器，允许某些元素通过。
所有查询都以 `select` 子句或 `group` 子句结束。在本示例中，使用了 `select` 子句。它指定了查询获取的内容。对于简单查询（如本例所示），选择了范围值。因此，它返回了 `nums` 中满足 `where` 子句的整数。在更复杂的情况下，可以精细地选择内容。例如，查询邮件列表时，你可能会返回每个收件者的姓，而不是整个地址。注意 select 子句以分号结束。因为 select 结束了一个查询，所以它结束了语句并需要分号。但注意，查询中的其他子句并不以分号结束。

到此时，查询变量 `posNums` 已经创建，但尚未获得任何结果。重要的是要理解查询仅仅定义了一组规则。只有在执行查询时，才会获得结果。此外，同一个查询可以执行两次或多次，如果底层数据源在执行之间发生变化，结果可能会不同。因此，简单地声明查询 `posNums` 并不意味着它包含了查询结果。

要执行查询，程序使用了此处所示的 `foreach` 循环：

```
foreach(int i in posNums) Console.WriteLine(i);
```

注意 `posNums` 是正在迭代的集合。当 `foreach` 执行时，由 `posNums` 指定的查询所定义的规则将被执行。随着循环的每次通过，都会获取查询返回的下一个元素。当没有更多元素可以检索时，过程结束。在这种情况下，迭代变量 `i` 的类型被显式指定，因为它是查询获取的元素的类型。在某种情况下显式指定迭代变量的类型是可以的，因为很容易知道查询选取值的类型。然而，在更复杂的情况下，使用 `var` 隐式指定迭代变量的类型会更容易（或者在某些情况下是必要的）。

## 查询可以执行多次

同一个查询定义了一组规则。如果数据源在执行之间发生变化，结果可能会有所不同。因此，范围的类型是 `int`。这是一个示例：

```csharp
using System;
using System.Linq;
using System.Collections.Generic;
class SimpleQuery {
    static void Main() {
        int[] nums = { 1, -2, 3, -4, 5 };
        // 创建一个简单查询
        var posNums = from n in nums
                      where n > 0
                      select n;
        // 执行查询
        foreach(int i in posNums) {
            Console.WriteLine(i);
        }
    }
}
```

## 查询中类型之间的关系

范围变量的类型是从数据源推断出来的。在这种情况下，`n` 的类型是 `int`。只要数据源实现了 `IEnumerable<T>`，范围变量的类型就可以推断出来。这是一个关键点。

## 查询的通用形式

所有查询共享一个通用形式，该形式基于一组上下文关键字，如下：

| ascending | descending | equals | from |
|---|---|---|---|
| group | in | into | join |
| let | on | orderby | select |
| where | | | |

在这些中，以下开始了查询子句：

| from | group | join | let |
|---|---|---|---|
| orderby | select | | |
| where | | | |

## 第 14 章：介绍 LINQ

如前所述，查询必须以 `from` 关键字开始，并以 `select` 或 `group` 子句结束。`select` 子句决定了查询枚举的值的类型。`group` 子句按分组返回数据，每个组都将被单独枚举。如前面的示例所示，`where` 子句指定了项目返回时必须满足的标准。剩余的子句则帮助你精调查询。

## 使用 where 过滤值

如所解释，`where` 用于通过查询返回数据。之前的示例仅展示了最简单的形式，即使用单个条件。需要理解的一个关键点是，你可以使用 `where` 根据多个条件来过滤数据。实现此点的方法之一是使用多个子句。例如，考虑以下程序，它只显示数组中大于且小于 10 的值。

```csharp
// 使用多个子句.
using System;
using System.Linq;
class TwoWheres {
    static void Main() {
        int[] nums = { 1, -2, 3, -3, 0, -8, 12, 19, 6, 9, 10 };
