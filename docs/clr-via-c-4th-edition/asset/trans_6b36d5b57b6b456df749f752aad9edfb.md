

| 属性 | 访问权限 | 类型 | 描述 |
| :--- | :--- | :--- | :--- |
| InnerException | 只读 | Exception | 如果当前异常是在处理异常时引发的，则指示前一个异常。此只读属性通常为 null。Exception 类型还提供了一个公共的 GetBaseException 方法，该方法遍历内部异常的链接列表并返回最初引发的异常。 |
| HResult | 读/写 | Int32 | 一个 32 位值，在跨越托管代码和本机代码边界时使用。例如，当 COM API 返回失败的 HRESULT 值时，CLR 会引发一个派生自 Exception 的对象，并在此属性中保留该 HRESULT 值。 |

我想就 System.Exception 的只读 StackTrace 属性说几句。catch 块可以读取此属性，以获取堆栈跟踪，指示调用了哪些方法才导致该异常。当你试图检测异常的原因以便修正代码时，这些信息可能极有价值。访问此属性时，实际上会调用 CLR 中的代码；该属性并不是简单地返回一个字符串。构造派生自 Exception 类型的新对象时，StackTrace 属性初始化为 null。如果读取该属性，你不会得到堆栈跟踪，而会得到 null。

当异常被引发时，CLR 会在内部记录引发指令所在的位置。当 catch 块接受该异常时，CLR 会记录捕获该异常的位置。如果现在在 catch 块内访问所引发异常对象的 StackTrace 属性，实现该属性的代码会调用 CLR，后者会生成一个字符串，标识从异常引发位置到捕获该异常的筛选器之间的所有方法。

![](img/857bdf6cef9e242b53a37f88df9a1287_486_0.png)

> **重要** 当你引发异常时，CLR 会重置异常的起始点；也就是说，CLR 只记住最近一次引发异常对象的位置。

以下代码引发它捕获的同一个异常对象，并导致 CLR 重置该异常的起始点。

```csharp
private void SomeMethod() {
    try { ... }
    catch (Exception e) {
        ...
        throw e;   // CLR thinks this is where exception originated.
                   // FxCop reports this as an error
    }
}
```

相比之下，如果仅使用 throw 关键字本身重新引发异常对象，CLR 不会重置堆栈的起始点。以下代码重新引发它捕获的同一个异常对象，导致 CLR 不重置该异常的起始点。

```csharp
    private void SomeMethod() {
        try {
            ...
        }
        catch (Exception e) {
            ...
            throw;   // This has no effect on where the CLR thinks the exception
                     // originated. FxCop does NOT report this as an error
        }
    }
```

事实上，这两段代码的唯一区别在于 CLR 认为异常最初引发的位置。不幸的是，当你引发或重新引发异常时，Windows 确实会重置堆栈的起始点。因此，如果异常变为未处理，报告给 Windows 错误报告的堆栈位置就是最后一次引发或重新引发的位置，即使 CLR 知道最初引发异常的堆栈位置。这很不幸，因为它使调试在现场失败的应用程序变得更加困难。一些开发者觉得这难以忍受，于是选择另一种方式实现其代码，以确保堆栈跟踪真正反映异常最初引发的位置。

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

StackTrace 属性返回的字符串不包含调用堆栈中位于 catch 块接受异常对象所在点之上的任何方法。如果你想要从线程开始到异常处理程序的完整堆栈跟踪，可以使用 System.Diagnostics.StackTrace 类型。此类型定义了一些属性和方法，使开发者能够以编程方式操作堆栈跟踪以及构成堆栈跟踪的帧。

可以使用多个不同的构造函数构造 StackTrace 对象。一些构造函数从线程开始到构造 StackTrace 对象的位置构建帧。另一些构造函数通过使用作为参数传递的派生自 Exception 的对象来初始化 StackTrace 对象的帧。

如果 CLR 能为你的程序集找到调试符号（位于 .pdb 文件中），则 System.Exception 的 StackTrace 属性或 System.Diagnostics.StackTrace 的 ToString 方法返回的字符串将包含源代码文件路径和行号。此信息对调试极为有用。

- System.Diagnostics.Tracing.EventSourceException
- System.InvalidTimeZoneException
- System.IO.IsolatedStorage.IsolatedStorageException
- System.Threading.LockRecursionException
- System.Runtime.CompilerServices.RuntimeWrappedException
- System.SystemException
  - System.Threading.AbandonedMutexException
  - System.AccessViolationException
  - System.Reflection.AmbiguousMatchException
  - System.AppDomainUnloadedException
  - System.ArgumentException
    - System.ArgumentNullException
    - System.ArgumentOutOfRangeException
    - System.Globalization.CultureNotFoundException
    - System.Text.DecoderFallbackException
    - System.DuplicateWaitObjectException
    - System.Text.EncoderFallbackException
    - System.ArithmeticException
      - System.DivideByZeroException
      - System.NotFiniteNumberException
      - System.OverflowException
    - System.ArrayTypeMismatchException
    - System.BadImageFormatException
    - System.CannotUnloadAppDomainException
    - System.ContextMarshalException
    - System.Security.Cryptography.CryptographicException
      - System.Security.Cryptography.CryptographicUnexpectedOperationException
    - System.DataMisalignedException
  - System.ExecutionEngineException
  - System.Runtime.InteropServices.ExternalException
    - System.Runtime.InteropServices.COMException
    - System.Runtime.InteropServices.SEHException
  - System.FormatException
    - System.Reflection.CustomAttributeFormatException
  - System.Security.HostProtectionException
  - System.Security.Principal.IdentityNotMappedException
  - System.IndexOutOfRangeException
  - System.InsufficientExecutionStackException
  - System.InvalidCastException
  - System.Runtime.InteropServices.InvalidComObjectException
  - System.Runtime.InteropServices.InvalidOleVariantTypeException
  - System.InvalidOperationException
    - System.ObjectDisposedException
  - System.InvalidProgramException
  - System.IO.IOException
    - System.IO.DirectoryNotFoundException
    - System.IO.DriveNotFoundException
    - System.IO.EndOfStreamException
    - System.IO.FileLoadException
    - System.IO.FileNotFoundException
    - System.IO.PathTooLongException
  - System.Collections.Generic.KeyNotFoundException
  - System.Runtime.InteropServices.MarshalDirectiveException
  - System.MemberAccessException
    - System.FieldAccessException
    - System.MethodAccessException
    - System.MissingMemberException

