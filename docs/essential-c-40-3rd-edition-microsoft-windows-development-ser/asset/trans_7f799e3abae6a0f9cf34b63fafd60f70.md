
```
{
    System.Console.WriteLine(
        "The age entered {0} is not valid.",
        ageText);
    result = 1;
}
catch(System.Exception exception)
{
    System.Console.WriteLine(
        "Unexpected error: {0}", exception.Message);
    result = 1;
}
catch
{
    System.Console.WriteLine(
        "Unexpected error!");
    result = 1;
}
finally
{
    System.Console.WriteLine("Goodbye {0}",
        firstName);
}
...
```

一个没有数据类型的 catch 块，称为 **泛型 catch 块**，相当于指定一个接受 object 数据类型的 catch 块：例如，`catch(object exception){...}`。由于所有类最终都派生自 `object`，没有数据类型的 catch 块必须出现在最后。

泛型 catch 块很少使用，因为无法捕获有关异常的任何信息。此外，C# 不支持抛出 object 类型的异常。（仅用 C++ 等语言编写的库允许任何类型的异常。）

从 C# 2.0 开始的行为与早期 C# 行为略有不同。在 C# 2.0 中，如果语言允许非 `System.Exception`，则抛出的异常对象将被包装在 `System.Runtime.CompilerServices.RuntimeWrappedException` 中，它确实派生自 `System.Exception`。因此，所有异常，无论是否派生自 `System.Exception`，都将作为派生自 `System.Exception` 传播到 C# 程序集中。

结果是，`System.Exception` catch 块将捕获早期块未捕获的所有异常，而在 System.Exception catch 块之后的常规 catch 块永远不会被调用。因此，在 C# 2.0 或更高版本中，在 System.Exception catch 块之后跟一个常规 catch 块会导致编译器警告，指示常规 catch 块永远不会执行。

## 使用 throw 语句报告错误

正如 int.Parse() 可以抛出异常一样，C# 允许开发者从他们的代码中抛出异常，如清单 4.23 和输出 4.15 所示。

### 清单 4.23：抛出异常

```
using System;
class ThrowingExceptions
{
    static void Main()
    {
        try
        {
            Console.WriteLine("Begin executing");
            Console.WriteLine("Throw exception...");
            throw new Exception("Arbitrary exception.");
            Console.WriteLine("End executing");
        }
        catch (FormatException exception)
        {
            Console.WriteLine(
                "A FormatException was thrown");
        }
        catch(Exception exception)
        {
            Console.WriteLine(
                "Unexpected error: {0}", exception.Message);
        }
        catch
        {
            Console.WriteLine("Unexpected error!");
        }
        Console.WriteLine(
            "Shutting down...");
    }
}
```

```
Begin executing
Throw exception...
Unexpected error: Arbitrary exception
Shutting down...
```

如清单 4.23 中的箭头所示，抛出异常会将执行从抛出异常的位置跳转到堆栈中与抛出的异常类型兼容的第一个 catch 块。在这种情况下，第二个 catch 块处理异常并输出错误消息。在清单 4.23 中，没有 finally 块，因此执行会穿过到 try/catch 块之后的 System.Console.WriteLine() 语句。

为了抛出异常，需要有一个异常的实例。清单 4.23 使用 new 关键字后跟异常的数据类型来创建实例。大多数异常类型允许在抛出异常时包含一条消息，以便在发生异常时可以检索该消息。

有时，catch 块会捕获异常但无法适当或完全处理它。在这种情况下，catch 块可以使用不指定任何异常的 throw 语句重新抛出异常，如清单 4.24 所示。

### 清单 4.24：重新抛出异常

```
...
catch(Exception exception)
{
    Console.WriteLine(
        "Rethrowing unexpected error: {0}",
        exception.Message);
    throw;
}
...
```

## 避免使用异常处理来处理预期情况

开发者应努力避免为预期条件或正常控制流抛出异常。例如，开发者不应指望用户在指定年龄时输入有效文本。因此，开发者不应依赖异常来验证用户输入的数据，而应在尝试转换之前提供一种检查数据的方法。（更好的做法是，你应从一开始就防止用户输入无效数据。）异常专门用于跟踪异常、意外且潜在致命的情况。将其用于预期情况等非预期目的会导致你的代码难以阅读、理解和维护。

此外，（与大多数语言一样）C# 在抛出异常时会产生轻微的性能损耗——耗时微秒，而大多数操作耗时纳秒。这种延迟在人类时间中通常不可察觉——除非异常未被处理。例如，在执行清单 4.19 并输入无效年龄时，异常未被处理，运行时会搜索环境以查看是否有调试器要加载，因此会有明显的延迟。幸运的是，程序关闭时性能缓慢通常不是需要担心的因素。

## 高级主题

### 使用 TryParse() 进行数值转换

Parse() 方法的问题之一是，确定转换是否成功的唯一方法是尝试转换，如果不成功则捕获异常。由于抛出异常是一项相对昂贵的操作，因此最好在不使用异常处理的情况下尝试转换。在 C# 的第一个版本中，唯一支持此功能的数据类型是名为 double.TryParse() 的 double 方法。但是，CLI 在 CLI 2.0 版本中将此方法添加到了所有数值原始类型中。它需要使用 out 关键字，因为 TryParse() 函数的返回值是 bool 而不是转换后的值。下面是一个使用 int.TryParse() 演示转换的代码清单。

- 5. 一般来说，开发者应预期用户会执行意外操作，因此应采取防御性编码来处理“愚蠢的把戏”。

```
...
if (int.TryParse(ageText, out age))
{
    System.Console.WriteLine(
        "Hi {0}! You are {1} months old.", firstName,
        age * 12);
}
else
{
    System.Console.WriteLine(
        "The age entered {0} is not valid.", ageText);
}
...
```

在 .NET Framework 4 中，枚举类型也添加了 TryParse() 方法。

有了 TryParse() 方法，就不再需要仅为了处理字符串到数值转换而包含 try/catch 块。

## 摘要

本章讨论了声明和调用方法的细节。在许多方面，此构造与 C 类语言中的声明相同。但是，添加 out 和 ref 关键字在语法上更类似于 COM（CLI 技术的前身），而不是 C 类语言中使用的“&&”。除了方法声明，本章还介绍了异常处理。

方法是编写可读代码的关键基本构造。与其编写包含大量语句的大型方法，不如将方法用作代码中的“段落”，长度目标大约为十行或更少。将大型函数分解为较小的片段是重构代码以使其更易读和可维护的方法之一。

下一章将探讨类构造及其如何将方法（行为）和字段（数据）封装为一个单元。

*本页故意留空*

## 类

你在第 1 章中简要了解了如何声明名为 HelloWorld 的新类。在第 2 章中，你学习了 C# 包含的内置原始类型。既然你现在还学习了控制流以及如何声明方法，是时候讨论定义你自己的了

- 1 声明和实例化类
- 2 实例字段
  - 声明实例字段
  - 访问实例字段
  - const 和 readonly 修饰符
- 3 实例方法
- 4 访问修饰符
- 5 属性
  - 声明属性
  - 命名约定
  - 使用带验证的属性
  - 只读和只写属性
  - Getter 和 Setter 上的访问修饰符
  - 虚拟属性上的属性
  - 接口上的属性
  - 不允许作为 ref 或 out 参数值的调用
- 6 构造函数和终结器
  - 声明构造函数
  - 默认构造函数
  - 重载构造函数
  - 使用 this 调用一个构造函数
  - 终结器
- 7 静态
  - 静态字段
  - 静态方法
  - 静态构造函数
  - 静态类
- 8 扩展方法
- 9 特殊类
  - 分部类
  - 嵌套类
