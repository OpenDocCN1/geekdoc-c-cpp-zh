
类型被视为匹配。通用 catch 子句被视为与任何异常类型匹配。如果找到匹配的 catch 子句：

-   如果匹配的 catch 子句声明了异常变量，则异常对象将被赋给该异常变量。
-   控制权转移到匹配的 catch 块。
-   当且仅当控制流到达 catch 块的结束点时：
  -   如果 try 语句有 finally 块，则执行 finally 块。
  -   控制权转移到 try 语句的结束点。
-   如果在 catch 块执行期间异常被传播到 try 语句：
  -   如果 try 语句有 finally 块，则执行 finally 块。
  -   异常被传播到下一个外层 try 语句。
-   如果 try 语句没有 catch 子句或没有 catch 子句与异常匹配：
  -   如果 try 语句有 finally 块，则执行 finally 块。
  -   异常被传播到下一个外层 try 语句。

finally 块的语句在控制流离开 try 语句时始终执行。这无论控制转移是由于正常执行、执行 break、continue、goto 或 return 语句的结果，还是由于将异常从 try 语句传播出来而发生的结果都是如此。

如果在 finally 块执行期间抛出异常，并且未在同一 finally 块内捕获，则该异常将被传播到下一个外层 try 语句。如果另一个异常正在被传播过程中，则该异常会丢失。传播异常的过程在 throw 语句的描述（§13.10.6）中进一步讨论。

如果 try 语句可达，则 try 语句的 try 块可达。如果 try 语句可达，则 try 语句的 catch 块可达。如果 try 语句可达，则 try 语句的 finally 块可达。try 语句的结束点可达当且仅当以下两个条件都为真时：

-   try 块的结束点可达或至少一个 catch 块的结束点可达。
-   如果存在 finally 块，则 finally 块的结束点可达。

## 13.12 checked 和 unchecked 语句

checked 和 unchecked 语句用于控制积分类型算术运算和转换的溢出检查上下文。

```
checked-statement:
    checked block

unchecked-statement:
    unchecked block
```

checked 语句导致块中的所有表达式在 checked 上下文中求值，而 unchecked 语句导致块中的所有表达式在 unchecked 上下文中求值。checked 和 unchecked 语句与 checked 和 unchecked 运算符（§12.7.14）精确等效，只是它们对块而不是表达式进行操作。

## 13.13 lock 语句

lock 语句为给定对象获取互斥锁，执行语句，然后释放锁。

```
lock-statement:
    lock ( expression ) embedded-statement
```

lock 语句的表达式必须表示已知为引用的类型的值。lock 语句的表达式永远不会执行隐式装箱转换（§11.2.8），因此表达式表示值类型的值是编译时错误。

形式为

```
lock ( x ) ...
```

的 lock 语句，其中 x 是引用类型的表达式，精确等效于：

```
bool __lockWasTaken = false;
try {
    System.Threading.Monitor.Enter(x, ref __lockWasTaken);  ...
}
finally {
    if (__lockWasTaken) System.Threading.Monitor.Exit(x);
}
```

只是 x 只被求值一次。

在持有互斥锁期间，同一执行线程中执行的代码也可以获取和释放锁。然而，其他线程中执行的代码在锁被释放之前无法获取锁。

## 13.14 using 语句

using 语句获取一个或多个资源，执行语句，然后释放资源。

```
using-statement:
    using ( resource-acquisition ) embedded-statement
resource-acquisition:
    local-variable-declaration
    expression
```

资源是实现 System.IDisposable 接口的类或结构体，该接口包含一个名为 Dispose 的无参数方法。使用资源时，代码可以调用 dispose 来表示资源不再需要。

形式为

```
using (ResourceType resource = expression) statement
```

的 using 语句对应于三种可能的展开之一。当 ResourceType 是不可为空的值类型或具有值类型约束的类型参数（§15.2.5）时，展开在语义上等效于

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

只是 resource 到 System.IDisposable 的强制转换不得导致装箱发生。

否则，当 ResourceType 为 dynamic 时，展开为

```
{
    ResourceType resource = expression;
    IDisposable d = resource;
    try {
        statement;
    }
    finally {
        if (d != null) d.Dispose();
    }
}
```

否则，展开为

```
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        IDisposable d = (IDisposable)resource;
        if (d != null) d.Dispose();
    }
}
```

在任何展开中，资源变量在嵌入语句中为只读，且 d 变量在嵌入语句中不可访问且对嵌入语句不可见。

实现可以以不同的方式实现给定的 using 语句，例如出于性能原因，只要行为与上述展开一致即可。

形式为：

```
using (expression) statement
```

的 using 语句具有相同的三种可能的展开。在这种情况下，ResourceType 隐式为表达式的编译时类型（如果有）。否则，接口 IDisposable 本身用作 ResourceType。资源变量在嵌入语句中不可访问且对嵌入语句不可见。

当 *resource-acquisition* 采用 *local-variable-declaration* 的形式时，可以获取给定类型的多个资源。形式为

```
using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) statement
```

的 using 语句精确等效于一系列嵌套的 using 语句：

```
using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
        ...
            using (ResourceType rN = eN)
                statement
```

[示例：下面的示例创建一个名为 log.txt 的文件并向文件中写入两行文本。然后示例打开同一文件进行读取并将包含的行复制到控制台。

```
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

由于 TextWriter 和 TextReader 类实现了 IDisposable 接口，示例可以使用 using 语句确保在写入或读取操作后底层文件被正确关闭。*示例结束*]

## 13.15 yield 语句

yield 语句用于在迭代器块（§13.3）中向迭代器的枚举器对象（§15.14.5）或可枚举对象（§15.14.6）产生值，或表示迭代结束。

```
yield-statement:
    yield return expression ;
    yield break ;
```

yield 是上下文关键字（§7.4.4），只有在紧跟 return 或 break 关键字时才具有特殊含义。

yield 语句可以出现的位置有若干限制，如下所述。

-   如果 yield 语句（任一形式）出现在 *method-body*、*operator-body* 或 *accessor-body* 之外，则为编译时错误。
-   如果 yield 语句（任一形式）出现在匿名函数内部，则为编译时错误。
-   如果 yield 语句（任一形式）出现在 try 语句的 finally 子句中，则为编译时错误。
-   如果 yield return 语句出现在包含任何 catch 子句的 try 语句中的任何位置，则为编译时错误。

[示例：下面的示例显示了 yield 语句的一些有效和无效用法。

```
delegate IEnumerable<int> D();
```
