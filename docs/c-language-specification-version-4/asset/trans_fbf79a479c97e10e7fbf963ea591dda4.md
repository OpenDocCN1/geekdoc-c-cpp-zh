
```
static void Main() {
    try {
        F();
    }
    catch (Exception e) {
        Console.WriteLine("Exception in Main: " + e.Message);
    }
}
```

方法 F 捕获一个异常，将一些诊断信息写入控制台，修改异常变量，并重新抛出异常。被重新抛出的异常是原始异常，因此产生的输出为：

```
Exception in F: G
Exception in Main: G
```

如果第一个 catch 块抛出 e 而不是重新抛出当前异常，则产生的输出如下：

```
Exception in F: G
Exception in Main: F
```

如果 break、continue 或 goto 语句将控制权转移出 finally 块，则为编译时错误。当 break、continue 或 goto 语句出现在 finally 块中时，该语句的目标必须在同一个 finally 块内，否则会发生编译时错误。

在 finally 块中出现 return 语句是编译时错误。

try 语句的执行方式如下：

- 控制权转移到 try 块。
- 当且仅当控制权到达 try 块的终点时：
  - 如果 try 语句有 finally 块，则执行 finally 块。
  - 控制权转移到 try 语句的终点。
- 如果在 try 块执行期间有异常传播到 try 语句：
  - 按出现顺序检查 catch 子句（如果有），以定位适合处理异常的处理程序。第一个指定异常类型或异常类型的基类型的 catch 子句被视为匹配。一般 catch 子句被视为与任何异常类型匹配。如果找到匹配的 catch 子句：
    - 如果匹配的 catch 子句声明了异常变量，则将异常对象赋给异常变量。
    - 控制权转移到匹配的 catch 块。
    - 当且仅当控制权到达 catch 块的终点时：
      - 如果 try 语句有 finally 块，则执行 finally 块。
      - 控制权转移到 try 语句的终点。
    - 如果在 catch 块执行期间有异常传播到 try 语句：
      - 如果 try 语句有 finally 块，则执行 finally 块。
      - 该异常传播到下一个封闭的 try 语句。
  - 如果 try 语句没有 catch 子句或没有 catch 子句匹配该异常：
- 如果 try 语句有 finally 块，则执行 finally 块。
- 该异常传播到下一个封闭的 try 语句。

当控制权离开 try 语句时，finally 块的语句总是会被执行。这无论控制转移是由于正常执行、执行 break、continue、goto 或 return 语句的结果，还是由于将异常从 try 语句传播出来的结果，都为真。

如果在 finally 块执行期间抛出异常，并且未在同一 finally 块内捕获，则该异常传播到下一个封闭的 try 语句。如果另一个异常正在传播过程中，则该异常会丢失。异常传播的过程在 throw 语句 (§8.9.5) 的描述中进一步讨论。

如果 try 语句可达，则 try 语句的 try 块可达。

如果 try 语句可达，则 try 语句的 catch 块可达。

如果 try 语句可达，则 try 语句的 finally 块可达。

如果以下两点均为真，则 try 语句的终点可达：

- try 块的终点可达，或至少一个 catch 块的终点可达。
- 如果存在 finally 块，则 finally 块的终点可达。

## 8.11 checked 和 unchecked 语句

checked 和 unchecked 语句用于控制整数类型算术运算和转换的溢出检查上下文。

```
checked-statement:
    checked block

unchecked-statement:
    unchecked block
```

checked 语句导致块中的所有表达式都在已检查上下文中求值，而 unchecked 语句导致块中的所有表达式都在未检查上下文中求值。

checked 和 unchecked 语句与 checked 和 unchecked 运算符 (§7.6.12) 精确等价，只是它们操作的是块而不是表达式。

## 8.12 lock 语句

lock 语句为给定对象获取互斥锁，执行一个语句，然后释放该锁。

```
lock-statement:
    lock ( expression ) embedded-statement
```

lock 语句的表达式必须表示已知为引用类型的类型的值。lock 语句的表达式永远不会执行隐式装箱转换 (§6.1.7)，因此表达式表示值类型的值是编译时错误。

形式为的 lock 语句

```
lock ( x ) ...
```

其中 x 是引用类型的表达式，精确等价于

如果资源的类型为 dynamic，则在获取期间通过隐式动态转换 (§6.1.8) 动态转换为 IDisposable，以确保转换在使用和释放之前成功。

形式为的 using 语句

```
using (ResourceType resource = expression) statement
```

对应于三种可能的展开之一。当 ResourceType 是非可空值类型时，展开为

```
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        ((IDisposable)resource).Dispose();
    }
}
```

否则，当 ResourceType 是可空值类型或除 dynamic 之外的引用类型时，展开为

```
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        if (resource != null) ((IDisposable)resource).Dispose();
    }
}
```

否则，当 ResourceType 为 dynamic 时，展开为

```
{
    ResourceType resource = expression;
    IDisposable d = (IDisposable)resource;
    try {
        statement;
    }
    finally {
        if (d != null) d.Dispose();
    }
}
```

在任一展开中，资源变量在嵌入语句中为只读，且 d 变量在嵌入语句中不可访问且对嵌入语句不可见。

实现可以以不同方式实现给定的 using 语句，例如出于性能原因，只要行为与上述展开一致即可。

形式为的 using 语句

```
using (expression) statement
```

具有相同的三种可能展开，但在这种情况下 ResourceType 隐式为表达式的编译时类型，且资源变量在嵌入语句中不可访问且对嵌入语句不可见。

当资源获取采用局部变量声明的形式时，可以获取给定类型的多个资源。形式为的 using 语句

```
using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) statement
```

精确等价于一组嵌套的 using 语句：

```
using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
        ...
            using (ResourceType rN = eN)
                statement
```

下面的示例创建一个名为 `log.txt` 的文件并向其中写入两行文本。然后示例打开同一个文件进行读取并将包含的行文本复制到控制台。

```csharp
using System;
using System.IO;

class Test
{
    static void Main() {
        using (TextWriter w = File.CreateText("log.txt")) {
            w.WriteLine("This is line one");
            w.WriteLine("This is line two");
        }
        using (TextReader r = File.OpenText("log.txt")) {
            string s;
            while ((s = r.ReadLine()) != null) {
                Console.WriteLine(s);
            }
        }
    }
}
```

由于 `TextWriter` 和 `TextReader` 类实现了 `IDisposable` 接口，示例可以使用 `using` 语句确保在写入或读取操作后底层文件被正确关闭。

## 8.14 yield 语句

`yield` 语句用于迭代器块 (§8.2) 中，将值传递给迭代器的枚举器对象 (§10.14.4) 或可枚举对象 (§10.14.5)，或用于发出迭代结束的信号。

```
yield-statement:
    yield return expression ;
    yield break ;
```

`yield` 不是保留字；只有在 `return` 或 `break` 关键字之前立即使用时才有特殊含义。在其他上下文中，`yield` 可用作标识符。

`yield` 语句可以出现的位置有若干限制，如下所述。

- `yield` 语句（任一形式）出现在 *方法体*、*运算符体* 或 *访问器体* 之外是编译时错误
- `yield` 语句（任一形式）出现在匿名函数内部是编译时错误。
- `yield` 语句（任一形式）出现在 *try* 语句的 *finally* 子句中是编译时错误。
- `yield return` 语句出现在包含任何 *catch* 子句的 *try* 语句中的任何位置是编译时错误。

以下示例展示了 `yield` 语句的一些有效和无效用法。

```csharp
delegate IEnumerable<int> D();
```
