
| 属性 | 访问 | 类型 | 描述 |
|---|---|---|---|
| Data | 只读 | `IDictionary` | 对键值对集合的引用。通常，引发异常的代码会在引发异常之前向此集合添加条目；捕获异常的代码可以查询这些条目，并在其异常恢复处理中使用这些信息。 |
| Source | 读写 | `String` | 包含生成该异常的程序集的名称。 |
| StackTrace | 只读 | `String` | 包含导致引发异常的方法的名称和签名。此属性对于调试非常宝贵。 |
| TargetSite | 只读 | `MethodBase` | 包含引发异常的方法。 |
| HelpLink | 读写 | `String` | 包含一个 URL（例如 `file:///C:\MyApp\Help.htm#MyExceptionHelp`），指向可帮助用户理解该异常的文档。请记住，良好的编程和安全实践会阻止用户看到原始未处理异常，因此除非你想向其他程序员传达信息，否则此属性很少使用。 |
| InnerException | 只读 | `Exception` | 如果当前异常是在处理异常时引发的，则指示前一个异常。此只读属性通常为 null。`Exception` 类型还提供一个公共 `GetBaseException` 方法，该方法遍历内部异常链表并返回最初引发的异常。 |
| HResult | 读写 | `Int32` | 在跨越托管代码和本机代码边界时使用的 32 位值。例如，当 COM API 返回失败的 HRESULT 值时，CLR 会引发一个派生自 Exception 的对象，并将 HRESULT 值保存在此属性中。 |

我想就 System.Exception 的只读 StackTrace 属性说几句。catch 块可以读取此属性，以获取堆栈跟踪，指示在异常发生前调用了哪些方法。当你试图检测异常原因以便修正代码时，这些信息可能极其宝贵。访问此属性时，你实际上会调用 CLR 中的代码；该属性并不只是返回一个字符串。构造一个派生自 Exception 类型的新对象时，StackTrace 属性会初始化为 null。如果读取该属性，你不会得到堆栈跟踪，而会得到 null。

引发异常时，CLR 会在内部记录 throw 指令发生的位置。当 catch 块接受异常时，CLR 会记录捕获该异常的位置。如果现在在 catch 块内访问所引发异常对象的 StackTrace 属性，实现该属性的代码会调用 CLR，而 CLR 会生成一个字符串，标识从异常引发位置到捕获该异常的筛选器之间的所有方法。

**重要** 引发异常时，CLR 会重置该异常的起始点；也就是说，CLR 只记住最近一次引发异常对象的位置。

以下代码引发它捕获的同一异常对象，并导致 CLR 重置该异常的起始点：

```csharp
private void SomeMethod() {
    try { ... }
    catch (Exception e) {
        throw e;  // CLR thinks this is where exception originated.
                   // FxCop reports this as an error
    }
}
```

相反，如果仅使用 throw 关键字重新引发异常对象，CLR 不会重置堆栈的起始点。以下代码重新引发它捕获的同一异常对象，从而使 CLR 不重置该异常的起始点：

```csharp
private void SomeMethod() {
    try { ... }
    catch (Exception e) {
        ...
        throw;  // This has no effect on where the CLR thinks the exception
                // originated. FxCop does NOT report this as an error
    }
}
```

事实上，这两个代码片段的唯一区别在于 CLR 认为异常最初引发的位置。不幸的是，当你重新引发异常时，Windows 确实会重置堆栈的起始点。因此，如果该异常变为未处理异常，报告给 Windows 错误报告的堆栈位置就是最后一次 throw 或重新 throw 的位置，即使 CLR 知道最初引发异常的堆栈位置。这很不幸，因为它使调试在现场失败的应用程序变得更加困难。一些开发者觉得这实在无法忍受，因此选择另一种方式实现代码，以确保堆栈跟踪真正反映异常最初引发的位置：

```csharp
private void SomeMethod() {
    Boolean trySucceeds = false;
    try {
        ...
        trySucceeds = true;
    }
    finally {
        if (!trySucceeds) { /* catch code goes in here */ }
    }
}
```

StackTrace 属性返回的字符串不包含调用堆栈中位于 catch 块接受异常对象的位置之上的任何方法。如果你想获得从线程开始到异常处理程序的完整堆栈跟踪，可以使用 System.Diagnostics.StackTrace 类型。此类型定义了一些属性和方法，使开发者能够以编程方式操作堆栈跟踪以及构成堆栈跟踪的帧。

你可以使用多个不同的构造函数构造 StackTrace 对象。一些构造函数会构建从线程开始到构造 StackTrace 对象位置的帧。其他构造函数则通过使用作为参数传入的派生自 Exception 的对象来初始化 StackTrace 对象的帧。

如果 CLR 能为你的程序集找到调试符号（位于 .pdb 文件中），则 System.Exception 的 StackTrace 属性或 System.Diagnostics.StackTrace 的 ToString 方法返回的字符串将包含源代码文件路径和行号。此信息对调试非常有用。

每当你获得堆栈跟踪时，可能会发现实际调用堆栈中的一些方法未出现在堆栈跟踪字符串中。原因有两个。第一，堆栈实际上记录的是线程应返回到哪里，而不是线程来自哪里。第二，实时 (JIT) 编译器可以内联方法，以避免调用单独方法并从中返回的开销。许多编译器（包括 C# 编译器）提供 `/debug` 命令行开关。使用此开关时，这些编译器会将信息嵌入生成的程序集，以告诉 JIT 编译器不要内联该程序集的任何方法，从而使堆栈跟踪对调试代码的开发者来说更完整、更有意义。

**注意** JIT 编译器会检查应用于程序集的 System.Diagnostics.DebuggableAttribute 自定义特性。C# 编译器会自动应用此特性。如果此特性指定了 DisableOptimizations 标志，JIT 编译器将不会内联该程序集的方法。使用 C# 编译器的 `/debug` 开关会设置此标志。通过将 System.Runtime.CompilerServices.MethodImplAttribute 自定义特性应用于某个方法，你可以禁止 JIT 编译器在调试版本和发布版本中内联该方法。以下方法定义展示了如何禁止内联该方法：

```csharp
using System;
using System.Runtime.CompilerServices;

internal sealed class SomeType {

    [MethodImpl(MethodImplOptions.NoInlining)]
    public void SomeMethod() {
    } ...
}
```

## FCL 定义的异常类

框架类库 (FCL) 定义了许多异常类型（它们最终都派生自 System.Exception）。以下层次结构显示了 MSCorLib.dll 程序集中定义的异常类型；其他程序集定义的异常类型甚至更多。（用于获得此层次结构的应用程序见第 23 章“程序集加载和反射”。）

```text
System.Exception
    System.AggregateException
    System.ApplicationException
        System.Reflection.InvalidFilterCriteriaException
        System.Reflection.TargetException
        System.Reflection.TargetInvocationException
        System.Reflection.TargetParameterCountException
        System.Threading.WaitHandleCannotBeOpenedException
    System.Diagnostics.Tracing.EventSourceException
    System.InvalidTimeZoneException
    System.IO.IsolatedStorage.IsolatedStorageException
    System.Threading.LockRecursionException
    System.Runtime.CompilerServices.RuntimeWrappedException
    System.SystemException
        System.Threading.AbandonedMutexException
        System.AccessViolationException
        System.Reflection.AmbiguousMatchException
        System.AppDomainUnloadedException
        System.ArgumentException
            System.ArgumentNullException
            System.ArgumentOutOfRangeException
            System.Globalization.CultureNotFoundException
            System.Text.DecoderFallbackException
            System.DuplicateWaitObjectException
            System.Text.EncoderFallbackException
        System.ArithmeticException
            System.DivideByZeroException
            System.NotFiniteNumberException
            System.OverflowException
        System.ArrayTypeMismatchException
        System.BadImageFormatException
        System.CannotUnloadAppDomainException
        System.ContextMarshalException
        System.Security.Cryptography.CryptographicException
            System.Security.Cryptography.CryptographicUnexpectedOperationException
        System.DataMisalignedException
        System.ExecutionEngineException
        System.Runtime.InteropServices.ExternalException
            System.Runtime.InteropServices.COMException
            System.Runtime.InteropServices.SEHException
        System.FormatException
            System.Reflection.CustomAttributeFormatException
        System.Security.HostProtectionException
        System.Security.Principal.IdentityNotMappedException
        System.IndexOutOfRangeException
```
