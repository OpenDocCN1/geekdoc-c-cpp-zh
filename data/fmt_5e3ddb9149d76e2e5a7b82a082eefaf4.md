
```
// will be (or has been) called by finalization queue

// processing already

if (disposing)

{

    Stream?.Close();

}

File?.Delete();

}
```

从`Program.Search()`中，在使用`TemporaryFileStream`之后显式调用了`Dispose()`。`Dispose()`是负责清理与内存无关的资源的（在此情况下为文件）方法，因此这些资源不受垃圾回收器的隐式清理管辖。然而，这里的执行存在一个漏洞，会阻止`Dispose()`的执行——即在`TemporaryFileStream`实例化到调用`Dispose()`之间发生异常的可能性。如果发生这种情况，`Dispose()`将不会被调用，资源清理将不得不依赖终结器。为了避免这个问题，调用者需要实现一个`try/finally`块。C#并没有要求程序员显式编写这样的块，而是专门为此提供了一个`using`语句（清单9.22）。

## 清单9.22：调用using语句

```
class Program
{
    // ...
    static void Search()
    {
        using (TemporaryFileStream fileStream1 =
            new TemporaryFileStream(),
            fileStream2 = new TemporaryFileStream())
        {
            // Use temporary file stream;
        }
    }
}
```

所产生的CIL代码与程序员显式指定`try/finally`块（在`finally`块中调用`fileStream.Dispose()`）所生成的代码相同。然而，`using`语句提供了`try/finally`块的一种语法快捷方式。

在`using`语句中，你可以通过逗号分隔每个变量来实例化多个变量。关键注意事项是：所有变量必须属于相同类型，并且它们都实现`IDisposable`。为了强制使用相同类型，数据类型只被指定一次，而不是在每个变量声明前都指定。

## 垃圾回收、终结与IDisposable

在清单9.21中还有几个值得注意的地方。首先，`IDisposable.Dispose()`方法包含一个对`System.GC.SuppressFinalize()`的重要调用。其目的是将`TemporaryFileStream`类实例从终结（f-reachable）队列中移除。这是可行的，因为所有清理工作都在`Dispose()`方法中完成，而不是等待终结器执行。

如果没有对`SuppressFinalize()`的调用，对象实例将被包含在f-reachable队列中——这是一个包含所有“几乎准备好进行垃圾回收”但还具有终结实现”的对象的列表。运行时不能在终结方法被调用之前对具有终结器的对象进行垃圾回收。然而，垃圾回收本身并不会调用终结方法。相反，对终结对象的引用会被添加到f-reachable队列中，并由另一个线程根据执行上下文认为合适的时间进行处理。具有讽刺意味的是，这种方法延迟了对托管资源的垃圾回收——而恰恰是这些资源很可能应该更早地被清理。延迟的原因是f-reachable队列是一个“引用”列表；因此，在终结方法被调用并且对象引用从f-reachable队列中移除之前，这些对象并不被视为垃圾。

注意

未显式释放的带终结器的对象将最终导致对象生命周期延长。即使在所有显式引用都超出作用域之后，f-reachable队列仍然会持有引用，使对象保持存活，直到f-reachable队列处理完毕。

正是由于这个原因，`Dispose()`会调用`System.GC.SuppressFinalize`。调用此方法会通知运行时不要将该对象添加到终结队列中，而是允许垃圾回收器在对象不再具有任何引用（包括任何 f-reachable 引用）时将其释放。

其次，`Dispose()`以参数`true`调用`Dispose(bool disposing)`。结果是调用`Stream`上的`Dispose()`方法（清理其资源并抑制其终结）。接下来，临时文件本身在调用`Dispose()`后立即被删除。这一重要调用无需等待终结队列被处理就能清理可能昂贵的资源。

第三，终结器现在不是调用`Close()`，而是以参数`false`调用`Dispose(bool disposing)`。结果是即使文件被删除，`Stream`也不会被关闭（释放）。关闭`Stream`的条件确保如果从终结器调用`Dispose(bool disposing)`，`Stream`实例本身也会被排队等待终结处理（或者根据顺序可能已经运行）。因此，在执行终结器时，不应清理托管资源所拥有的对象，因为这一操作将由终结队列负责。

第四，在同时创建`Close()`类型方法和`Dispose()`方法时应谨慎。仅从 API 看不出`Close()`会调用`Dispose()`，因此开发人员会疑惑是否需要显式调用`Close()`和`Dispose()`。

> **语言对比：C++——确定性析构**
> 
> 虽然终结器类似于 C++ 中的析构函数，但它们的执行无法在编译时确定，这使得它们截然不同。垃圾回收器会在 C# 终结器最后一次使用后的某个时间、但在程序关闭之前调用它们；C++ 析构函数则在对象（非指针）超出作用域时自动调用。
> 
> 尽管运行垃圾回收器可能是一个相对昂贵的过程，但垃圾回收足够智能，可以延迟运行直到进程利用率有所降低，这比确定性析构函数具有优势，后者会在编译时定义的位置运行，即使处理器负载很高。

## 准则

- 应仅在对象拥有稀缺或昂贵资源时实现终结器方法，尽管终结会延迟垃圾回收。
- 应在具有终结器的类上实现`IDisposable`以支持确定性终结。
- 应在实现`IDisposable`的类上实现终结器方法，以防未显式调用`Dispose()`。
- 应重构终结方法，使其调用与`IDisposable`相同的代码，也许只需调用`Dispose()`方法。
- 不应从终结器方法中抛出异常。
- 应从`Dispose()`调用`System.GC.SuppressFinalize()`，以避免重复清理资源和延迟对象的垃圾回收。
- 应确保`Dispose()`是幂等的（应可多次调用`Dispose()`）。
- 应保持`Dispose()`简单，专注于终结所需的资源清理。
- 应避免对拥有终结器的对象调用`Dispose ()`。相反，应依赖终结队列来清理实例。
- 应避免在终结期间引用尚未被终结的其他对象。
- 当重写`Dispose()`时，应调用基类的`Dispose()`方法。
- 应考虑确保对象在调用`Dispose()`后变得不可用。对象被释放后，除`Dispose()`（可能被多次调用）之外的方法应抛出`ObjectDisposedException`。
- 应在拥有可释放字段（或属性）的类型上实现`IDisposable`，并释放这些实例。

## 高级主题

## 构造函数中的异常传播

即使异常从构造函数中传播出来，对象仍然会被实例化，尽管`new`运算符不会返回新实例。如果类型定义了终结器，当对象符合垃圾回收条件时，该终结方法将运行（这提供了额外的动力，确保终结方法能在部分构造的对象上运行）。还要注意，如果构造函数过早地共享其`this`引用，即使构造函数抛出异常，该引用仍然可以访问。不要让这种情况发生。

## 高级主题

## 对象的复活

当对象的终结方法被调用时，对对象的所有引用都已经消失，垃圾回收前的唯一步骤是运行终结代码。即便如此，仍有可能意外地将一个终结对象的引用添加回根引用图中。在这种情况下，被重新引用的对象将不再不可访问；反过来，它也不会准备好进行垃圾回收。但是，如果对象的终结方法已经运行过，除非显式标记为需要终结（使用`GC.ReRegisterFinalize()`方法），否则它不一定会再次运行。

显然，以这种方式复活对象是一种奇怪的行为；通常应避免。终结代码应该简单，并应专注于仅清理它引用的资源。

## 惰性初始化

在前一节中，我们讨论了如何使用`using`语句确定性地释放对象，以及在没有使用确定性方法时终结队列如何释放资源。

一种相关模式称为惰性初始化或惰性加载。使用惰性初始化，您可以按需创建（或获取）对象，而不是预先创建——当这些对象从未被使用时，后者可能是一个特别有问题的情形。考虑清单 9.23 的`FileStream`属性。

### 清单 9.23：属性的惰性加载

```
using System.IO;

class DataCache
{
    // ...
    public TemporaryFileStream FileStream =>
        InternalFileStream ?? (InternalFileStream =
            new TemporaryFileStream());
    private TemporaryFileStream InternalFileStream
        { get; set; } = null;
    // ...
}
```

在`FileStream`的表达式体属性中，我们检查`InternalFileStream`是否为空，如果不为空则直接返回其值。如果`InternalFileStream`为空，我们首先实例化`TemporaryFileStream`对象并将其赋给`InternalFileStream`，然后返回新实例。因此，只有在调用属性的`getter`时，才会创建`FileStream`属性所需的`TemporaryFileStream`。如果`getter`从未被调用，则不会实例化`TemporaryFileStream`对象，并且我们将节省实例化所需的时间。显然，如果实例化成本可忽略不计或不可避免（并且推迟不可避免的事情不太可取），那么在声明期间或构造函数中直接赋值是有意义的。

## 高级主题

## 使用泛型和 Lambda 表达式的惰性加载

从`.NET Framework 4.0`开始，CLR 中新增了一个类来协助惰性初始化：`System.Lazy<T>`。清单 9.24 演示如何使用它。

### 清单 9.24：使用 System.Lazy<T> 对属性进行惰性加载

```
using System.IO;

class DataCache
{
    // ...
    public TemporaryFileStream FileStream =>
        InternalFileStream.Value;
    private Lazy<TemporaryFileStream> InternalFileStream { get; }
        = new Lazy<TemporaryFileStream>(
            () => new TemporaryFileStream() );
    // ...
}
```

`System.Lazy<T>`类接受一个类型参数 (`T`)，该参数标识`System.Lazy<T>`上的`Value`属性将返回的类型。不是将完全构造好的`TemporaryFileStream`赋值给`_FileStream`字段，而是分配一个`Lazy<TemporaryFileStream>`实例（一次轻量级调用），将`TemporaryFileStream`本身的实例化延迟到访问`Value`属性（因此也就是`FileStream`属性）时。

### 本章小结

本章对构建健壮类库所涉及的许多主题进行了快速浏览。所有主题同样适用于内部开发，但它们对于构建健壮的类更为关键。最终，这里的重点是形成更健壮、更具可编程性的 API。在健壮性这一类别中，我们可以包括命名空间和垃圾回收。这两个主题也属于可编程性类别，此外还有重写对象的虚拟成员、运算符重载以及用于文档的 XML 注释。

异常处理大量使用继承：它定义了一个异常层次结构，并强制自定义异常符合这一层次结构。此外，C# 编译器还使用继承来验证`catch`块的顺序。在下一章中，你将看到为什么继承是异常处理如此核心的一部分。

# 10 异常处理

第 4 章讨论了使用`try/catch/finally`块进行标准异常处理。在那章中，`catch`块总是捕获`System.Exception`类型的异常。本章定义了异常处理的一些额外细节——具体来说，是围绕其他异常类型、定义自定义异常以及用于处理每种类型的多个`catch`块的细节。由于异常对继承的依赖，本章还详细介绍了异常。

![](img/25683ccec0773ba5b8794b11f2b12877_471_0.png)

### 多种异常类型

清单 10.1 抛出的是`System.ArgumentException`，而不是第 4 章演示的`System.Exception`类型。C# 允许代码抛出任何派生自（可能间接派生自）`System.Exception`的类型。

`ArgumentException`可以提供更多上下文信息，例如参数名称。如果即使参数为`null`也有一种无害的继续执行方式，请务必使用 C# 6.0 的`null`传播运算符，以避免运行时抛出`NullReferenceException`。

参数异常类型（包括`ArgumentException`、`ArgumentNullException`和`ArgumentOutOfRangeException`）的一个重要特征是，每种类型都有一个构造函数参数，允许以字符串形式标识参数名称。在 C# 6.0 之前，这意味着需要硬编码一个魔法字符串（例如`"textDigit"`）来标识参数名称。这种方法的问题在于，如果参数名称发生变化，开发人员必须记得更新这个魔法字符串。幸运的是，C# 6.0 提供了一个新运算符`nameof`，它接受参数名称标识符并在编译时生成参数名称（参见清单 10.1 中的`nameof(textDigit)`）。这种方法的优点是，IDE 现在可以使用重构工具（例如自动重命名）在所有位置更改该标识符，包括当它被用作`nameof`运算符的参数时。此外，如果参数名称发生变化（未使用重构工具），那么当传给`nameof`运算符的标识符不再存在时，编译器将生成错误。展望未来，在 C# 6.0（或更高版本）中，一般准则是始终使用`nameof`运算符来提供参数异常类型的参数名称。

其他一些异常仅面向运行时使用，并且（有时间接）派生自`System.SystemException`。它们包括`System.StackOverflowException`、`System.OutOfMemoryException`、`System.Runtime.InteropServices.COMException`、`System.ExecutionEngineException`和`System.Runtime.InteropServices.SEHException`。不要抛出这些类型的异常。同样，应避免抛出`System.Exception`或`System.ApplicationException`，因为这些异常过于笼统，几乎无法指示问题的原因或解决方法。相反，应抛出最适合该场景的派生程度最高的异常。显然，开发人员应避免创建可能导致系统故障的 API。但是，如果正在执行的代码达到某种状态，使得继续执行不安全或无法恢复，则应调用`System.Environment.FailFast()`。这将在向 Windows 应用程序事件日志写入消息后立即终止进程；如果用户如此选择，甚至还会将该消息作为 Windows 错误报告的一部分包含在内。

### 准则

- 如果向成员传递了错误的参数，应抛出`ArgumentException`或其子类型之一。如适用，优先选择派生程度最高的异常类型（例如`ArgumentNullException`）。
- 当抛出`ArgumentException`或其某个子类时，应设置`ParamName`属性。
- 在向`ArgumentException`、`ArgumentOutOfRangeException`和`ArgumentNullException`等接受此类参数的参数异常类型传入`paramName`参数时，应使用`nameof`。
- 应抛出最有意义的最具体（派生程度最高）的异常。
- 不要抛出`NullReferenceException`。当值意外为`null`时，应抛出`ArgumentNullException`。
- 不要抛出`System.SystemException`或从此类型派生的异常类型。
- 不要抛出`System.Exception`或`System.ApplicationException`。
- 如果程序遇到无法安全继续执行的情况，应考虑调用`System.Environment.FailFast()`来终止进程。

### 捕获异常

抛出特定异常类型使捕获者能够使用异常类型本身来识别问题。换句话说，没有必要捕获异常后，再根据异常消息使用`switch`语句来决定针对该异常应采取何种操作。相反，C# 允许多个`catch`块，每个块针对特定的异常类型，如清单 10.2 所示。

**清单 10.2：捕获不同类型的异常**

```csharp
using System;

public sealed class Program
{
    public static void Main(string[] args)
    {
        try
        {
            // ...
            throw new InvalidOperationException(
                "Arbitrary exception");
            // ...
        }
        catch (Win32Exception exception)
            when (exception.ErrorCode == 42)
        {
            // Handle Win32Exception where
```
