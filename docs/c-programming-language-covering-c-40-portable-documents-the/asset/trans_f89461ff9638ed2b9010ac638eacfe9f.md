

## 8.10 try 语句

try 语句提供了一种机制，用于捕获在块执行期间发生的异常。此外，try 语句还提供了一种能力，可以指定一个代码块，当控制流离开 try 语句时始终执行该代码块。

```
try-statement:
    try block catch-clauses
    try block finally-clause
    try block catch-clauses finally-clause
```

```
catch-clauses:
    specific-catch-clauses general-catch-clause_opt
    specific-catch-clauses_opt general-catch-clause
```

```
specific-catch-clauses:
    specific-catch-clause
    specific-catch-clauses specific-catch-clause
```

```
specific-catch-clause:
    catch ( class-type identifier_opt ) block
```

```
general-catch-clause:
    catch block
```

```
finally-clause:
    finally block
```

try 语句有三种可能的形式：

- 一个 try 块后跟一个或多个 catch 块。
- 一个 try 块后跟一个 finally 块。
- 一个 try 块后跟一个或多个 catch 块，再后跟一个 finally 块。

当 catch 子句指定类类型时，该类型必须是 System.Exception、派生自 System.Exception 的类型，或以 System.Exception（或其子类）作为有效基类的类型参数类型。

当 catch 子句同时指定类类型和标识符时，将声明一个具有给定名称和类型的异常变量。该异常变量对应于一个局部变量，其作用域覆盖 catch 块。在执行 catch 块期间，异常变量表示当前正在处理的异常。为了进行明确赋值检查，该异常变量在其整个作用域内被视为已明确赋值。

除非 catch 子句包含异常变量名，否则无法在 catch 块中访问异常对象。

既不指定异常类型也不指定异常变量名的 catch 子句称为通用 catch 子句。try 语句只能有一个通用 catch 子句，如果存在，它必须是最后一个 catch 子句。

某些编程语言可能支持无法表示为派生自 System.Exception 的对象的异常，尽管此类异常永远不可能由 C# 代码生成。可以使用通用 catch 子句来捕获此类异常。因此，通用 catch 子句在语义上不同于指定 System.Exception 类型的 catch 子句，因为前者还可以捕获来自其他语言的异常。

> ERIC LIPPERT 在当前的 Microsoft C# 和 CLR 实现中，默认情况下，不派生自 Exception 的已引发对象会被转换为 RuntimeWrappedException 对象。因此，catch(Exception e) 会捕获所有异常。
>
> 如果希望禁用此行为并使用 C# 1.0 语义，即其他语言引发的非 Exception 对象不会以这种方式被捕获，则使用以下程序集特性：

```
[assembly:System.Runtime.CompilerServices.RuntimeCompatibility(WrapNonExceptionThrows = false)]
```

为了定位异常的处理程序，catch 子句按词法顺序检查。如果某个 catch 子句指定的类型与同一 try 块中较早的 catch 子句所指定的类型相同，或派生自该类型，则发生编译时错误。如果没有此限制，就可能编写出不可达的 catch 子句。

在 catch 块内，可以使用不带表达式的 throw 语句（§8.9.5）重新引发该 catch 块捕获的异常。对异常变量赋值不会改变重新引发的异常。

在下面的示例中

```
using System;
class Test
{
    static void F() {
        try {
            G();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in F: " + e.Message);
            e = new Exception("F");
            throw;    // Rethrow
        }
    }

    static void G() {
        throw new Exception("G");
    }

    static void Main() {
        try {
            F();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in Main: " + e.Message);
        }
    }
}
```

方法 F 捕获一个异常，向控制台写入一些诊断信息，修改异常变量，然后重新引发该异常。重新引发的是原始异常，因此产生的输出为

```
Exception in F: G
Exception in Main: G
```

如果第一个 catch 块抛出的是 e，而不是重新引发当前异常，则产生的输出将如下所示：

```
Exception in F: G
Exception in Main: F
```

break、continue 或 goto 语句将控制转移出 finally 块属于编译时错误。当 break、continue 或 goto 语句出现在 finally 块中时，该语句的目标必须位于同一个 finally 块内；否则会发生编译时错误。

return 语句出现在 finally 块中属于编译时错误。

try 语句的执行方式如下：

- 控制转移到 try 块。
- 当控制流到达 try 块的结束点时（如果会到达）：
  - 如果 try 语句有 finally 块，则执行 finally 块。
  - 控制转移到 try 语句的结束点。
- 如果在执行 try 块期间有异常传播到 try 语句：
  - 按出现顺序检查 catch 子句（如果有），以定位适合该异常的处理程序。第一个指定该异常类型或该异常类型的基类型的 catch 子句被视为匹配。通用 catch 子句被视为与任何异常类型匹配。如果找到匹配的 catch 子句：
    - 如果匹配的 catch 子句声明了异常变量，则将异常对象赋给该异常变量。
    - 控制转移到匹配的 catch 块。
    - 当控制流到达 catch 块的结束点时（如果会到达）：
      - 如果 try 语句有 finally 块，则执行 finally 块。
      - 控制转移到 try 语句的结束点。
    - 如果在执行 catch 块期间有异常传播到 try 语句：
      - 如果 try 语句有 finally 块，则执行 finally 块。
      - 该异常传播到下一个外层 try 语句。
  - 如果 try 语句没有 catch 子句，或者没有 catch 子句与该异常匹配：
    - 如果 try 语句有 finally 块，则执行 finally 块。
    - 该异常传播到下一个外层 try 语句。

> ERIC LIPPERT 如果调用堆栈包含由其他语言（如 Visual Basic）编写的 try-catch 块保护的代码，则运行时环境可能会执行“异常筛选器”，以确定给定的 catch 块是否适合所引发的异常。因此，用户代码可能会在异常引发之后、关联的 finally 块执行之前执行。如果你的异常处理代码依赖于在任何其他用户代码运行之前由 finally 块使全局状态保持一致，则应采取适当措施，确保你的代码在运行时环境执行可能位于堆栈上的用户定义异常筛选器之前捕获异常。

当控制流离开 try 语句时，finally 块的语句始终会执行。无论控制转移是由于正常执行而发生，还是由于执行 break、continue、goto 或 return 语句而发生，抑或是由于将异常传播出 try 语句而发生，都是如此。

如果在 finally 块执行期间引发异常，且未在同一 finally 块内捕获，则该异常会传播到下一个外层 try 语句。如果另一个异常正在传播过程中，则该异常会丢失。异常传播过程将在 throw 语句（§8.9.5）的说明中进一步讨论。

> BILL WAGNER 这种行为使得以防御性方式编写 finally 子句非常重要，以避免引发第二个异常。

> JON SKEET 当然，如果我们不必以防御性方式编写 finally 子句，那会很好。一个错误由另一个错误引起的概念，已经通过“内部异常”这一思想成为 .NET Framework 的一部分。即便如此，对于两个异常可能相关、但尚不知道其中任何一个由另一个引起的想法，目前还没有一种通用的表示方式。同样，方法可能引发哪些异常，通常也是一个棘手的问题。Java 试图用“受检异常”来解决这个问题——在我看来，这大多并不成功。
>
> 有时感觉我们（作为一个行业）在成功场景方面已经相当擅长，但在错误处理方面仍有很长的路要走。

