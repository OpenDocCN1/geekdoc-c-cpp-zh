

finally 块。但是，using 语句为 try/finally 块提供了语法快捷方式。

在 using 语句中，可以通过用逗号分隔每个变量来实例化多个变量。关键是所有变量都属于同一类型，并且都实现了 IDisposable。为强制使用相同类型，数据类型只需指定一次，而不必在每个变量声明前都指定。

## 垃圾回收与终结

IDisposable 模式包含一个额外的重要调用。回到清单 9.21，Close() 方法包含对 System.GC.SuppressFinalize() 的调用（在清单 9.23 中再次捕获）。其目的是将 TemporaryFileStream 类实例从终结（f-reachable）队列中移除。

### 清单 9.23：禁止终结

```
// ...
public void Close()
{
    if(Stream != null)
    {
        Stream.Close();
    }
    if(File != null)
    {
        File.Delete();
    }
    // Turn off calling the finalizer
    System.GC.SuppressFinalize(this);
}
// ...
```

f-reachable 队列是所有准备进行垃圾回收且同时具有终结实现的对象的列表。运行时在对象的终结方法被调用之前，不能对带有终结器的对象进行垃圾回收。但是，垃圾回收本身不会调用终结方法。相反，对终结对象的引用会被添加到 f-reachable 队列中，这反而讽刺地延迟了垃圾回收。这是因为 f-reachable 队列是“引用”的列表，因此，对象在其终结方法被调用且对象引用从 f-reachable 队列中移除之前，都不是垃圾。

### 语言对比：C++—确定性析构

虽然终结器与 C++ 中的析构函数相似，但由于其执行时间无法在编译时确定，因此两者有明显区别。垃圾回收器会在对象最后一次使用之后、程序关闭之前的某个时间点调用 C# 终结器；而 C++ 析构函数会在对象（而非指针）超出作用域时自动调用。

虽然运行垃圾回收器可能是一个相对昂贵的过程，但垃圾回收足够智能，可以在进程利用率有所降低后再运行，这相对于确定性析构函数具有一定优势，因为确定性析构函数会在编译时定义的位置运行，即使处理器负载很高。

### 高级主题

### 复活对象

在调用对象的终结方法时，对该对象的所有引用都已消失，垃圾回收前的唯一步骤是运行终结代码。但是，有可能会无意中将对终结对象的引用重新添加到根引用图中。这样一来，被引用的对象不再不可访问，因此也不再准备好进行垃圾回收。但是，如果该对象的终结方法已经运行过，除非显式标记为终结（使用 GC.ReRegisterForFinalize() 方法），否则不一定会再次运行。

显然，以这种方式复活对象是一种特殊的行为，通常应避免。终结代码应保持简单，并专注于清理其引用的资源。

## 资源利用与终结准则

在定义管理资源的类时，应考虑以下事项。

- 1. 仅在资源稀缺或昂贵的对象上实现 Finalize。终结会延迟垃圾回收。
- 2. 带有终结器的对象应实现 IDisposable 以支持确定性终结。
- 3. 终结方法通常会调用 IDisposable 调用的相同代码，可能只是简单地调用 Dispose() 方法。
- 4. 终结器应避免引起任何未处理的异常。
- 5. 诸如 Dispose() 和 Close() 之类的确定性终结方法应调用 System.GC.SuppressFinalize()，以便垃圾回收更早发生且资源清理不会重复。
- 6. 处理资源清理的代码可能会被多次调用，因此应当是可重入的。（例如，应可以多次调用 Close()。）
- 7. 资源清理方法应保持简单，并专注于仅清理由终结实例引用的资源。它们不应引用其他对象。
- 8. 如果基类实现了 Dispose，则派生类实现应调用基类实现。
- 9. 通常，对象在调用 Dispose() 后应被视为不可用。对象被释放后，除了 Dispose()（可能会被多次调用）之外的方法应抛出 ObjectDisposedException()。

## 惰性初始化

在前一节中，我们讨论了如何使用 using 语句确定性地释放对象，以及在未使用确定性方法的情况下，终结队列将如何释放资源。

一个相关的模式是懒加载或惰性初始化。使用懒加载，可以在需要对象时才创建（或获取）对象，而不是提前创建——尤其是在对象从未被使用时。请考虑清单 9.24 中的 FileStream 属性。

### 清单 9.24：懒加载属性

```
using System.IO;

class DataCache
{
    // ...

    public TemporaryFileStream FileStream
    {
        get
        {
            if (_FileStream == null)
            {
                _FileStream = new TemporaryFileStream();
            }
            return _FileStream;
        }
    }

    private TemporaryFileStream _FileStream = null;

    // ...
}
```

在 FileStream 属性中，只有在调用属性的 getter 时才会实例化 TemporaryFileStream 对象。如果从未调用 getter，则不会实例化 TemporaryFileStream 对象，从而节省实例化所需的执行时间。显然，如果实例化可忽略不计或不可避免（而且推迟不可避免的事情并不理想），那么在声明期间或构造函数中直接赋值是合理的。将对象的初始化推迟到需要时才进行，称为懒加载。

### 高级主题

### 使用泛型和 Lambda 表达式进行懒加载

从 .NET Framework 4.0 开始，CLR 中添加了一个新类来协助懒加载：System.Lazy<T>。清单 9.25 演示了如何使用它。

### 清单 9.25：懒加载属性

```
using System.IO;

class DataCache
{
    // ...

    public string FileStreamName { get; set; }

    public DataCache()
    {
        _FileStream = new Lazy<TemporaryFileStream>(
            () => new TemporaryFileStream(FileStreamName));
    }

    public TemporaryFileStream FileStream
    {
        get
        {
            return _FileStream.Value;
        }
    }

    private Lazy<TemporaryFileStream> _FileStream;

    // ...
}
```

System.Lazy<T> 类接受一个类型参数（T），用于标识 System.Lazy<T> 上的 Value 属性将返回什么类型。与其将完全构造的 TemporaryFileStream 赋值给 _FileStream 字段，不如赋值一个 Lazy<TemporaryFileStream> 实例（一个轻量级调用），从而推迟 TemporaryFileStream 本身的实例化，直到访问 Value 属性（因此也是 FileStream 属性）为止。

如果除了类型参数（泛型）之外还使用委托，则可以在访问 Value 属性时提供一个用于初始化对象的函数。清单 9.25 演示了将委托（在此示例中为 Lambda 表达式）传递给 System.Lazy<T> 构造函数。

需要注意的是，Lambda 表达式本身，即 () => new TemporaryFileStream(FileStreamName)，在调用 Value 之前不会执行。相反，Lambda 表达式提供了一种传递将要发生的操作指令的方式，但不会实际执行这些操作，直到明确请求为止。

