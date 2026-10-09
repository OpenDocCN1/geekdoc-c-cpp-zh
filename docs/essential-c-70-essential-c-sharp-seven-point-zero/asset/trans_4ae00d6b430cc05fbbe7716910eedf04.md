

```csharp
catch (Exception exception)
{
      // 处理异常
}
finally
{
      // 在此处处理任何清理代码，因为它无论如何都会执行
      // 不管是否发生异常
}
```

清单 11.2 包含五个 catch 块，每个块处理不同类型的异常。当发生异常时，执行流程将跳转到异常类型与当前异常最匹配的 catch 块。匹配程度由继承链决定。例如，虽然抛出的异常类型是 `System.Exception`，但由于 `System.InvalidOperationException` 最终继承自 `System.Exception`，因此通过这种“是一种”的继承关系产生了联系。由于异常类型 `InvalidOperationException` 与抛出的异常匹配度最高，因此 `catch(InvalidOperationException...)` 块将捕获该异常，而不是 `catch(Exception...)` 块。

从 C# 6.0 开始，catch 块提供了额外的条件表达式。不再仅限于基于异常类型匹配来决定是否执行 catch 块，C# 6.0 及更高版本支持使用条件子句。when 子句允许你提供一个布尔表达式；只有当条件为真时，catch 块才会处理该异常。在清单 11.2 中，这是一个相等性比较运算符。尽管如此，例如，你可以调用方法来验证某个条件。

当然，你也可以简单地将条件检查作为一个 if 块放在 catch 主体内部。然而，这样做会导致 catch 块在检查条件之前成为该异常的处理程序。很难编写代码，使得在条件不满足的情况下让不同的 catch 块来处理异常。然而，通过异常条件，现在可以在无需捕获并重新抛出异常的情况下检查程序状态（包括异常）。

谨慎使用条件子句；如果条件表达式本身抛出异常，那么该新异常将被忽略，并且该条件被视为假。因此，应避免在异常条件表达式中抛出异常。

Catch 块必须按顺序排列，从最具体到最通用，以避免编译时错误。例如，将 catch(Exception...) 块移动到任何其他异常之前会导致编译错误，因为所有先前的异常在其继承链的某个点上都继承自 System.Exception。

如 catch (SystemException){ } 块所示，catch 块不需要命中的参数。事实上，甚至没有类型参数的最终 catch 也是允许的，如下一节所示。

## 重新抛出已有异常

在 InvalidOperationException 的 catch 块中，出现了一个没有指定要抛出哪个异常的 throw 语句（throw 是独立存在的），即使在 catch 块的作用域中出现了异常实例（exception）可以重新抛出。抛出特定异常会更新所有堆栈信息以匹配新的抛出位置。结果是，指示异常最初发生位置的调用站点的所有堆栈信息都会丢失，这使得诊断问题变得更加困难。因此，C# 支持在 catch 块内使用没有显式异常引用的 throw 语句或表达式（C# 7.0 或更高版本）。这样，代码可以检查异常以确定是否可能完全处理它，如果不能，则重新抛出异常（即使没有明确指定），就好像它从未被捕获过，并且不替换任何堆栈信息。

### 高级主题

### 重新抛出已有异常而不替换堆栈信息

在 C# 5.0 中，增加了一种机制，允许在不丢失原始异常中的堆栈跟踪信息的情况下，抛出之前已抛出的异常。这允许你重新抛出异常，例如，即使在 catch 块外部，因此无需使用 `throw;`。虽然很少需要这样做，但在某些情况下，异常会被包装或保存，直到程序执行移动到 catch 块之外。例如，多线程代码可能会用 `AggregateException` 包装异常。Microsoft .NET Framework 4.5 提供了一个专门的 `System.Runtime.ExceptionServices.ExceptionDispatchInfo` 类，通过其静态 `Catch()` 和实例 `Throw()` 方法来处理这种场景。（不幸的是，截至 2.0 版本，该类在 .NET Core 中不可用。）清单 11.3 展示了如何重新抛出异常，而无需重置堆栈跟踪信息或使用空的 `throw` 语句。

**清单 11.3：使用 ExceptionDispatchInfo 重新抛出异常**

```csharp
using System
using System.Runtime.ExceptionServices;
using System.Threading.Tasks;
Task task = WriteWebRequestSizeAsync(url);
try
{
    while (!task.Wait(100))
    {
        Console.Write(".");
    }
}
catch (AggregateException exception)
{
    exception = exception.Flatten();
    ExceptionDispatchInfo.Capture(
        exception.InnerException).Throw();
}
```

使用 `ExceptionDispatchInfo.Throw()` 方法时，编译器不会像对待普通 `throw` 语句那样将其视为返回语句。例如，如果方法签名返回一个值，但代码路径在使用 `ExceptionDispatchInfo.Throw()` 时没有返回值，编译器将发出错误，指示没有返回值。因此，在某些情况下，开发人员可能被迫在 `ExceptionDispatchInfo.Throw()` 之后跟一个 return 语句，即使这样的语句在运行时永远不会执行——取而代之的是会抛出异常。

## 语言对比：Java——异常说明符

C# 没有相当于 Java 异常说明符的功能。利用异常说明符，Java 编译器能够验证函数（或函数的调用层级）中抛出的所有可能异常要么被捕获，要么被声明为可能重新抛出。C# 团队考虑过这个选项，并认为其所带来的维护负担不值得预期的好处。因此，没有必要在整个特定调用栈中维护所有可能异常的列表，但也无法轻松地确定可能的异常。（事实证明，这在 Java 中也是不可能的。调用虚方法或使用延迟绑定，例如反射，使得在编译时完全解析方法可能抛出的异常变得不可能。）

## 通用 Catch 块

C# 要求代码抛出的任何对象都必须继承自 System.Exception。然而，这一要求并非所有语言通用。例如，C 和 C++ 允许抛出任何对象类型，包括未从 System.Exception 继承的托管异常。从 C# 2.0 开始，无论是否继承自 System.Exception，所有异常都将作为 System.Exception 的派生类传播到 C# 程序集中。结果是，System.Exception 的 catch 块将捕获未被先前块捕获的所有异常。

C# 还支持**通用 catch 块**（catch{ }），其行为与 catch(System.Exception exception) 块完全相同，只是没有类型或变量名。此外，通用 catch 块必须出现在 catch 块列表的最后。由于通用 catch 块与 catch(System.Exception exception) 块相同，且通用 catch 块必须最后出现，如果两者存在于同一个 try/catch 语句中，编译器会发出警告，因为通用 catch 块永远不会被调用（有关通用 catch 块的更多信息，请参见标题为“C# 1.0 中的通用 Catch 块”的高级主题）。

### 高级主题

### C# 1.0 中的通用 Catch 块

在 C# 1.0 中，如果从方法调用中抛出了一个非 System.Exception 派生的异常（该方法调用所在的程序集并非用 C# 编写），该异常
