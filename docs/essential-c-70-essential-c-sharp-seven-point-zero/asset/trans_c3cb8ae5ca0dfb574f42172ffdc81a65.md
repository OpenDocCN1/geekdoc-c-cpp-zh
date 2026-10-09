
其次，`Dispose()` 调用带有参数 `true` 的 `Dispose(bool disposing)`。其结果是 `Stream` 上的 `Dispose()` 方法被调用（清理其资源并抑制其终结处理）。接下来，临时文件本身在调用 `Dispose()` 时立即被删除。这个重要调用消除了等待终结队列处理完毕后再清理潜在昂贵资源的必要性。

第三，终结方法现在调用带有参数 `false` 的 `Dispose(bool disposing)`，而不是调用 `Close()`。其结果是，尽管文件已被删除，但 `Stream` 并未关闭（释放）。围绕关闭 `Stream` 的条件确保，如果 `Dispose(bool disposing)` 从终结方法中调用，`Stream` 实例本身也将被加入等待终结处理的队列（或者根据执行顺序，它可能已经执行过了）。因此，在执行终结方法时，不应清理由托管资源拥有的对象，因为该操作将是终结队列的责任。

第四，在创建 `Close()` 类型和 `Dispose()` 方法时，你应当谨慎。仅通过查看 API 并不清楚 `Close()` 是否调用了 `Dispose()`，因此开发者会困惑是否需要显式调用 `Close()` 和 `Dispose()`。

## 准则

- 应当仅对拥有稀缺或昂贵资源的对象实现终结方法，即使终结处理会延迟垃圾收集。
- 应当实现对具有终结方法的类的 `IDisposable`，以支持确定性终结。
- 应当在对实现 `IDisposable` 的类上实现终结方法，以防 `Dispose()` 未被显式调用。
- 应当重构终结方法以调用与 `IDisposable` 相同的代码，或许只是简单地调用 `Dispose()` 方法。
- 不要在终结方法中抛出异常。
- 应当从 `Dispose()` 中调用 `System.GC.SuppressFinalize()`，以避免重复资源清理并延迟对象的垃圾收集。
- 应当确保 `Dispose()` 是幂等的（应允许多次调用 `Dispose()`）。
- 保持 `Dispose()` 简单，专注于终结所需的资源清理。
- 避免对拥有终结方法的自有对象调用 `Dispose()`。相反，依靠终结队列来清理该实例。
- 避免在终结过程中引用未处于终结过程的其他对象。
- 在重写 `Dispose()` 时，应当调用基类的 `Dispose()` 方法。
- 考虑在调用 `Dispose()` 后使对象变为不可用状态。对象被释放后，除 `Dispose()`（可能会被多次调用）之外的其他方法应抛出 `ObjectDisposedException`。
- 应当在对拥有可释放字段（或属性）的类型上实现 `IDisposable`，并释放这些实例。

### 语言对比：C++——确定性析构

尽管终结方法与 C++ 中的析构函数相似，但由于其执行时间无法在编译时确定，它们有着本质的区别。垃圾收集器会在最后使用 C# 终结方法后的一段时间内调用它们，但在程序关闭之前；C++ 析构函数在对象（而非指针）超出作用域时自动被调用。

虽然运行垃圾收集器可能是一个相对昂贵的过程，但垃圾收集足够智能，能够推迟执行直到进程利用率有所降低，这比确定性析构函数具有优势，后者会在编译时定义的位置运行，即使处理器处于高负载状态也是如此。

### 高级主题

#### 从构造函数传播的异常

即使异常从构造函数中传播出去，对象仍然会被实例化，尽管 `new` 运算符没有返回新的实例。如果类型定义了终结方法，当对象变得可被垃圾收集时，该方法将会运行（这提供了确保终结方法可以在部分构造的对象上运行的额外动机）。另外请注意，如果构造函数过早共享其 `this` 引用，即使构造函数抛出异常，该引用仍然是可访问的。不要让这种情况发生。

### 高级主题

## 对象复活

当对象的终结方法被调用时，所有指向该对象的引用都已消失，垃圾收集前的唯一步骤是运行终结代码。即便如此，仍有可能无意中将终结对象的引用重新添加回根引用图中。在这种情况下，被重新引用的对象将不再不可访问；反过来，它将不再准备好进行垃圾收集。然而，如果对象的终结方法已经运行过，除非显式标记为终结（使用 `GC.ReRegisterFinalize()` 方法），否则它不一定会再次运行。

显然，以这种方式复活对象是一种特殊的行为，通常应避免这种情况。终结代码应当简单，并专注于清理它所引用的资源。

## 延迟初始化

在前面的部分中，我们讨论了如何使用 `using` 语句确定性地释放对象，以及在没有使用确定性方法的情况下，终结队列将如何释放资源。

一个相关的模式被称为 *延迟初始化* 或 *延迟加载*。使用延迟初始化，你可以在需要时（而不是之前）创建（或获取）对象——后者在那些对象从未被使用的情况下可能是一个特别有问题的情况。考虑列表 10.23 中的 `FileStream` 属性。

### 列表 10.23：延迟加载属性

```csharp
using System.IO;

class DataCache
{
    // ...
    public TemporaryFileStream FileStream =>
        InternalFileStream ?? (InternalFileStream = new TemporaryFileStream());
}

private TemporaryFileStream InternalFileStream
{ get; set; } = null;

// ...
```

在 `FileStream` 表达式体属性中，我们在直接返回其值之前检查 `InternalFileStream` 是否为 null。如果 `InternalFileStream` 为 null，我们先实例化 `TemporaryFileStream` 对象并将其分配给 `InternalFileStream`，然后返回新实例。因此，`FileStream` 属性所需的 `TemporaryFileStream` 仅在调用该属性的 getter 时创建。如果 getter 从未被调用，`TemporaryFileStream` 对象将不会被实例化，我们会节省这种实例化所需的任何执行时间。显然，如果实例化开销可忽略不计或不可避免（且推迟不可避免的操作并不理想），在声明时或在构造函数中直接赋值是有意义的。

### 高级主题

## 使用泛型和 lambda 表达式的延迟加载

从 Microsoft .NET Framework 4.0 开始，CLR 中新增了一个类来辅助延迟初始化：`System.Lazy<T>`。列表 10.24 演示了如何使用它。

### 列表 10.24：使用 System.Lazy<T> 延迟加载属性

```csharp
using System.IO;

class DataCache
{
    // ...
    public TemporaryFileStream FileStream =>
        InternalFileStream.Value;
    private Lazy<TemporaryFileStream> InternalFileStream { get; }
        = new Lazy<TemporaryFileStream>(
            () => new TemporaryFileStream());
    // ...
}
```

`System.Lazy<T>` 类接受一个类型参数 (T)，用于标识 `System.Lazy<T>` 上的 `Value` 属性将返回哪种类型。不再将完全构造好的 `TemporaryFileStream` 分配给 `_FileStream` 字段，而是分配一个 `Lazy<TemporaryFileStream>` 实例（这是一个轻量级调用），从而延迟 `TemporaryFileStream` 本身的实例化，直到访问 `Value` 属性（因此也是 `FileStream` 属性）时为止。

除了类型参数（泛型）之外，如果你使用委托，你甚至可以提供如何在访问 `Value` 属性时初始化对象的功能。列表 10.24 演示了将委托——在此情况下是一个 lambda 表达式——传递给 `System.Lazy<T>` 的构造函数。

请注意，lambda 表达式本身，`() => new TemporaryFileStream (FileStreamName)`，直到调用 `Value` 时才执行。相反，lambda 表达式提供了一种传递将要发生之指令的手段；它不会实际执行这些指令，除非被明确要求这样做。

一个显而易见的问题是，何时应使用 `System.Lazy<T>` 而不是列表 10.23 中概述的方法。差异微乎其微：事实上，列表 10.23 可能更简单。也就是说，简单到有多个线程参与时，关于实例化可能会发生竞态条件。在列表 10.23 中，在实例化之前可能会发生多次 null 检查，导致创建多个实例。相比之下，`System.Lazy<T>` 提供了线程安全的机制，确保只创建一个对象。

## 总结

本章对许多与构建坚固类库相关的主题进行了快速回顾。所有主题都涉及内部开发，但对于构建稳健的类更为关键。最终，这里的重点是形成更坚固和可编程的 API。在稳健性类别中，我们可以包括命名空间和垃圾收集。这两个主题也属于可编程性类别，along with 重写 `object` 的虚成员、运算符重载以及用于文档的 XML 注释。

异常处理通过定义异常层次结构并强制自定义异常符合该层次结构，大量使用了继承。此外，`C#` 编译器使用继承来验证 catch 块的顺序。在下一章中，你将看到为什么继承是异常处理的核心部分。

