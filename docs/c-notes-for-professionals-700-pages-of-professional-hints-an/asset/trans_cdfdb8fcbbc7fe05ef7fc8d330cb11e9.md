
```
IEnumerable<string> Digits => Enumerable.Range(0, 10).Select(i => i.ToString());
```

在所有其他情况下，可以使用函数成员的旧语法。

表达式体函数成员可以包含 async/await，但这通常是多余的：

```
async Task<int> Foo() => await Bar();
```

可以替换为：

```
Task<int> Foo() => Bar();
```

## 第72.6节：nameof 运算符

nameof 运算符以字符串形式返回代码元素的名称。这在抛出与方法参数相关的异常以及实现 INotifyPropertyChanged 时非常有用。

```
public string SayHello(string greeted)
{
    if (greeted == null)
        throw new ArgumentNullException(nameof(greeted));
    Console.WriteLine("Hello, " + greeted);
}
```

nameof 运算符在编译时计算，并将表达式转换为字符串字面量。这对于与公开它们的成员同名的字符串也很有用。请考虑以下示例：

```
public static class Strings
{
    public const string Foo = nameof(Foo); // Rather than Foo = "Foo"
    public const string Bar = nameof(Bar); // Rather than Bar = "Bar"
}
```

由于 nameof 表达式是编译时常量，因此它们可以用于特性、case 标签、switch 语句等。

将 nameof 与枚举一起使用很方便。不要这样写：

```
Console.WriteLine(Enum.One.ToString());
```

可以使用：

```
Console.WriteLine(nameof(Enum.One))
```

两种情况的输出都是 One。

nameof 运算符可以使用类似静态的语法访问非静态成员。与其这样写：

```
string foo = "Foo";
string lengthName = nameof(foo.Length);
```

可以替换为：

```csharp
string lengthName = nameof(string.Length);
```

两个示例的输出都是 Length。但后一种方式避免了创建不必要的实例。

尽管 nameof 运算符适用于大多数语言构造，但仍有一些限制。例如，不能对开放式泛型类型或方法返回值使用 nameof 运算符：

```csharp
public static int Main()
{
    Console.WriteLine(nameof(List<>)); // Compile-time error
    Console.WriteLine(nameof(Main())); // Compile-time error
}
```

此外，如果将其应用于泛型类型，泛型类型参数将被忽略：

```csharp
Console.WriteLine(nameof(List<int>)); // "List"
Console.WriteLine(nameof(List<bool>)); // "List"
```

更多示例，请参阅专门介绍 nameof 的主题。

## 旧版本的变通方法（更多细节）

尽管在 C# 6.0 之前的版本中不存在 nameof 运算符，但可以使用 MemberExpression 获得类似的功能，如下所示：

版本 < 6.0

表达式：

```csharp
public static string NameOf<T>(Expression<Func<T>> propExp)
{
    var memberExpression = propExp.Body as MemberExpression;
    return memberExpression != null ? memberExpression.Member.Name : null;
}

public static string NameOf<TObj, T>(Expression<Func<TObj, T>> propExp)
{
    var memberExpression = propExp.Body as MemberExpression;
    return memberExpression != null ? memberExpression.Member.Name : null;
}
```

用法：

```csharp
string variableName = NameOf(() => variable);
string propertyName = NameOf((Foo o) => o.Bar);
```

请注意，这种方法会导致每次调用都创建表达式树，因此性能远低于 nameof 运算符，后者在编译时计算，运行时零开销。

## 第72.7节：使用静态类型

using static [Namespace.Type] 指令允许导入类型的静态成员和枚举值。扩展方法作为扩展方法（仅从一种类型）导入，而不是导入到顶级作用域。

版本 ≥ 6.0

```csharp
using static System.Console;
using static System.ConsoleColor;
using static System.Math;

class Program
{
    static void Main()
    {
        BackgroundColor = DarkBlue;
        WriteLine(Sqrt(2));
    }
}
```

在线演示 Fiddle

版本 < 6.0

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.BackgroundColor = ConsoleColor.DarkBlue;
        Console.WriteLine(Math.Sqrt(2));
    }
}
```

## 第72.8节：索引初始化器

索引初始化器使得可以在创建对象的同时使用索引对其进行初始化。

这使得初始化字典变得非常容易：

```csharp
var dict = new Dictionary<string, int>()
{
    ["foo"] = 34,
    ["bar"] = 42
};
```

任何具有索引 getter 或 setter 的对象都可以使用此语法：

```csharp
class Program
{
    public class MyClassWithIndexer
    {
        public int this[string index]
        {
            set
            {
                Console.WriteLine($"Index: {index}, value: {value}");
            }
        }
    }
}
```

```
public static void Main()
{
    var x = new MyClassWithIndexer()
    {
        ["foo"] = 34,
        ["bar"] = 42
    };
    Console.ReadKey();
}
```

输出：

索引: foo, 值: 34
索引: bar, 值: 42

查看演示

如果类有多个索引器，则可以在单个语句组中同时为它们赋值：

```
class Program
{
    public class MyClassWithIndexer
    {
        public int this[string index]
        {
            set
            {
                Console.WriteLine($"Index: {index}, value: {value}");
            }
        }
        public string this[int index]
        {
            set
            {
                Console.WriteLine($"Index: {index}, value: {value}");
            }
        }
    }

    public static void Main()
    {
        var x = new MyClassWithIndexer()
        {
            ["foo"] = 34,
            ["bar"] = 42,
            [10] = "Ten",
            [42] = "Meaning of life"
        };
    }
}
```

输出：

索引: foo, 值: 34
索引: bar, 值: 42
索引: 10, 值: Ten
索引: 42, 值: Meaning of life

需要注意的是，索引器 set 访问器的行为可能与 Add 方法（用于集合初始化器）不同。

例如：

```
var d = new Dictionary<string, int>
{
    ["foo"] = 34,
    ["foo"] = 42,
}; // does not throw, second value overwrites the first one
```

与以下方式对比：

```
var d = new Dictionary<string, int>
{
    { "foo", 34 },
    { "foo", 42 },
}; // run-time ArgumentException: An item with the same key has already been added.
```

## 第72.9节：改进的重载解析

以下代码片段演示了在需要委托时传递方法组（而不是 lambda）的示例。由于 C# 6 能够检查所传递方法的返回类型，重载解析现在可以解决此问题，而不会引发不明确的重载错误。

```
using System;
public class Program
{
    public static void Main()
    {
        Overloaded(DoSomething);
    }

    static void Overloaded(Action action)
    {
        Console.WriteLine("overload with action called");
    }

    static void Overloaded(Func<int> function)
    {
        Console.WriteLine("overload with Func<int> called");
    }

    static int DoSomething()
    {
        Console.WriteLine(0);
        return 0;
    }
}
```

结果：

版本 = 6.0

### 输出

> 调用了 Func<int> 重载

查看演示

版本 = 5.0

### 错误

> 错误 CS0121: 调用在以下方法或属性之间存在歧义: 'Program.Overloaded(System.Action)' 和 'Program.Overloaded(System.Func)'

C# 6 还可以很好地处理以下 lambda 表达式的精确匹配情况，而这在 C# 5 中会产生错误。

```csharp
using System;

class Program
{
    static void Foo(Func<Func<long>> func) {}
    static void Foo(Func<Func<int>> func) {}

    static void Main()
    {
        Foo(() => () => 7);
    }
}
```

## 第72.10节：在 catch 和 finally 中使用 await

在 C# 6 中，可以在 catch 和 finally 块中使用 await 表达式将 await 运算符应用于 Task 或 Task(Of TResult)。

由于编译器限制，在早期版本中无法在 catch 和 finally 块中使用 await 表达式。C# 6 通过允许使用 await 表达式，使等待异步任务变得容易得多。

```csharp
try
{
    //since C#5
    await service.InitializeAsync();
}
catch (Exception e)
{
    //since C#6
    await logger.LogAsync(e);
}
finally
{
    //since C#6
    await service.CloseAsync();
}
```

在 C# 5 中，需要使用 bool 或在 try-catch 外部声明一个 Exception，才能执行异步操作。

