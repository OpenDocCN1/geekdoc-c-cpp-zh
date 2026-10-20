

```
public MyClass(int initialCount)
{
    commonConstructor(initialCount, string.Empty);
}

public MyClass(int initialCount, string Name)
{
    commonConstructor(initialCount, Name);
}

private void commonConstructor(int count,
    string name)
{
    coll = (count > 0) ?
        new List<ImportantData>(count) :
        new List<ImportantData>();
    // ERROR changing the name outside of a constructor.
    this.name = name;
}
}
```

C++ 程序员只是接受这种情况，并在所有构造函数中初始化 Name，或者在实用程序例程中去掉 const 属性。C# 的构造函数初始化器提供了一个更好的替代方案。除了最微不足道的类之外，所有类都包含多个构造函数。它们的工作是初始化对象的全部成员。它们本质上具有相似或理想情况下共享的逻辑。使用 C# 构造函数初始化器提取这些通用算法，以便你只编写一次，它们也只执行一次。

默认值和重载各有其用途。一般来说，你应该优先使用默认值而不是重载的构造函数。毕竟，如果你允许客户端开发者指定参数值，那么你的构造函数必须能够处理用户指定的任何值。你的原始默认值始终应该是合理的，并且不应引发异常。因此，即使更改默认值在技术上是破坏性更改，也不应被客户端感知。他们的代码仍将使用原始值，而这些原始值仍应产生合理行为。这最大限度地降低了使用默认值的潜在风险。

这是关于 C# 中对象初始化的最后一项。这是一个回顾构造类型实例的整个事件序列的好时机。你应该了解操作的顺序以及对象的默认初始化。你应该努力在构造期间恰好初始化每个成员变量一次。你实现这一目标的最佳方式是尽可能早地初始化值。构造类型的第一个实例的操作顺序如下：

+   1. 静态变量存储被设为 0。
+   2. 静态变量初始化器执行。
+   3. 基类的静态构造函数执行。
+   4. 静态构造函数执行。
+   5. 实例变量存储被设为 0。
+   6. 实例变量初始化器执行。
+   7. 适当的基类实例构造函数执行。
+   8. 实例构造函数执行。

同一类型的后续实例从步骤 5 开始，因为类初始化器只执行一次。此外，步骤 6 和 7 被优化，以便构造函数初始化器导致编译器删除重复指令。

C# 语言编译器保证在对象创建时以某种方式初始化所有内容。至少，你可以保证当实例创建时，你的对象使用的所有内存都已设为 0。这对静态成员和实例成员都适用。你的目标是确保你按想要的方式初始化所有值，并且只执行一次该初始化代码。使用初始化器初始化简单资源。使用构造函数初始化需要更复杂逻辑的成员。还要对其他构造函数的调用进行分解，以最大限度地减少重复。

## 条目 15：利用 using 和 try/finally 进行资源清理

使用非托管系统资源的类型的显式释放应使用 IDisposable 接口的 Dispose() 方法进行。 .NET 环境的规则使这成为使用该类型的代码的责任，而不是类型或系统的责任。因此，只要你使用具有 Dispose() 方法的类型，释放这些资源并调用 Dispose() 就是你的责任。确保始终调用 Dispose() 的最佳方法是利用 using 语句或 try/finally 块。

所有拥有非托管资源的类型都实现 IDisposable 接口。此外，它们还会为那些你忘记正确释放的时候防御性地创建一个终结器。如果你忘记释放这些项目，这些非内存资源将在终结器有机会执行时稍后被释放。所有这些对象随后会留在内存中更长时间，你的应用程序会变成一个缓慢执行的资源占用大户。

幸运的是，C# 语言设计者知道显式释放资源将是一项常见任务。他们向语言中添加了关键字，使其变得容易。

假设你编写了以下代码：

```
public void ExecuteCommand(string connString,
    string commandString)
{
    SqlConnection myConnection = new SqlConnection(
        connString);
    SqlCommand mySqlCommand = new SqlCommand(commandString,
        myConnection);

    myConnection.Open();
    mySqlCommand.ExecuteNonQuery();
}
```

在此示例中，两个可释放对象未得到正确清理：SqlConnection 和 SqlCommand。这两个对象在它们的终结器被调用之前一直保留在内存中。 （这两个类都从 System.ComponentModel.Component 继承其终结器。）

你通过在完成命令和连接后调用 Dispose 来修复此问题：

```
public void ExecuteCommand(string connString,
    string commandString)
{
    SqlConnection myConnection = new SqlConnection(
        connString);
    SqlCommand mySqlCommand = new SqlCommand(commandString,
        myConnection);

    myConnection.Open();
    mySqlCommand.ExecuteNonQuery();

    mySqlCommand.Dispose();
    myConnection.Dispose();
}
```

这没问题，除非在 SQL 命令执行期间抛出任何异常。在这种情况下，你对 Dispose() 的调用永远不会发生。using 语句确保调用 Dispose()。你在 using 语句内部分配一个对象，C# 编译器会在每个对象周围生成一个 try/finally 块：

```
public void ExecuteCommand(string connString,
    string commandString)
{
    using (SqlConnection myConnection = new
        SqlConnection(connString))
    {
        using (SqlCommand mySqlCommand = new
            SqlCommand(commandString,
            myConnection))
        {
            myConnection.Open();
            mySqlCommand.ExecuteNonQuery();
        }
    }
}
```

每当你在函数中使用一个 Disposable 对象时，using 子句就是确保对象得到正确释放的最简单方法。using 语句会在被分配的对象周围生成一个 try/finally 块。这两个块生成完全相同的 IL：

```
SqlConnection myConnection = null;

// Example Using clause:
using (myConnection = new SqlConnection(connString))
{
    myConnection.Open();
}

// example Try / Catch block:
try
{
    myConnection = new SqlConnection(connString);
    myConnection.Open();
}
finally
{
    myConnection.Dispose();
}
```

如果你使用 using 语句而变量的类型不支持 IDisposable 接口，C# 编译器会生成错误。例如：

```
// Does not compile:
// String is sealed, and does not support IDisposable.
using (string msg = "This is a message")
    Console.WriteLine(msg);
```

using 语句仅在编译时类型支持 IDisposable 接口时才有效。你不能将其用于任意对象：

```
// Does not compile.
// Object does not support IDisposable.
using (object obj = Factory.CreateResource())
    Console.WriteLine(obj.ToString());
```

一个快速的防御性 as 子句就是安全释放可能实现也可能不实现 IDisposable 的对象所需的一切：

```
// The correct fix.
// Object may or may not support IDisposable.
object obj = Factory.CreateResource();
using (obj as IDisposable)
    Console.WriteLine(obj.ToString());
```

如果 obj 实现 IDisposable，using 语句会生成清理代码。如果没有，using 语句会退化为 using(null)，这是安全的，但什么也不做。如果你不确定是否应该将对象包装在 using 块中，请偏向安全：假设它实现了并将其包装在前面显示的 using 子句中。

这涵盖了简单的情况：每当你使用一个局部于方法的可释放对象时，就将该对象包装在 using 语句中。现在你可以查看一些更复杂的用法。第一个示例中需要释放两个不同的对象：连接和命令。我的示例创建了两个不同的 using 语句，一个包装需要释放的两个对象中的每一个。每个 using 语句都生成-

