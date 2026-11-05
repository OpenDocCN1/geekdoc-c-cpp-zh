
**try** 语句的 **try** 块在 **try** 语句可达时可达。

**try** 语句的 **catch** 块在 **try** 语句可达时可达。

**try** 语句的 **finally** 块在 **try** 语句可达时可达。

**try** 语句的结束点在以下两个条件都为真时可达：

- **try** 块的结束点可达，或至少一个 **catch** 块的结束点可达。
- 如果存在 **finally** 块，则 **finally** 块的结束点可达。

## 8.11 checked 和 unchecked 语句

**checked** 和 **unchecked** 语句用于控制整数类型算术运算和转换的 *overflow* 检查上下文。

```
checked-statement:
    checked block

unchecked-statement:
    unchecked block
```

**checked** 语句导致 *block* 中的所有表达式都在 **checked** 上下文中求值。**unchecked** 语句导致 *block* 中的所有表达式都在 **unchecked** 上下文中求值。

**checked** 和 **unchecked** 语句与 **checked** 和 **unchecked** 运算符 (§7.6.12) 完全等价，只是它们操作的是块而不是表达式。

## 8.12 lock 语句

**lock** 语句为给定对象获取互斥锁，执行一条语句，然后释放锁。

```
lock-statement:
    lock ( expression ) embedded-statement
```

**lock** 语句的表达式必须表示已知为 *reference-type* 的类型的值。**lock** 语句的表达式永远不会执行隐式装箱转换 (§6.1.7)，因此表达式表示值类型的值是编译时错误。

形式为的 lock 语句

```
lock (x) ...
```

其中 x 是 reference-type 的表达式，精确等价于

```
bool __lockWasTaken = false;
try {
    System.Threading.Monitor.Enter(x, __lockWasTaken);
    ...
}
finally {
    if (__lockWasTaken) System.Threading.Monitor.Exit(x);
}
```

只是 x 只被求值一次。

> **BILL WAGNER** lock() 语句提供了额外的编译器检查，以防止尝试锁定值类型。

在持有互斥锁期间，同一执行线程中执行的代码也可以获取和释放锁。然而，在其他线程中执行的代码在锁被释放之前会被阻止获取锁。

为了同步对静态数据的访问而锁定 System.Type 对象是不推荐的。其他代码可能锁定在同一类型上，这可能导致死锁。更好的方法是，通过锁定私有静态对象来同步对静态数据的访问。例如：

```
class Cache
{
    private static readonly object synchronizationObject = new object();
    public static void Add(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }

    public static void Remove(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }
}
```

> **JOSEPH ALBAHARI** 在编写供公众使用的库时，一个好的策略是使静态函数从一开始就是线程安全的（通常通过在函数内部实现锁定，如本例所示）。对于使用者来说，在调用静态方法或属性周围加锁要困难得多（甚至不可能），因为他们不知道函数是从哪些其他位置调用的。

## 8.13 using 语句

using 语句获取一个或多个资源，执行一条语句，然后释放该资源。

> **ERIC LIPPERT** 规范在此明确指出，using 语句的要点是确保 *resource* 的获取和及时释放。通常，这将包括来自操作系统的某些非托管资源，例如文件句柄。尽快停止使用资源是礼貌的；当你使用完它时，其他程序可能想要读取该文件。我不建议使用 using 语句来强制执行程序不变量。例如，有时人们会看到这样的代码：
>
> ```csharp
> using(new TemporarilyStopReportingErrors()) AttemptSomething();
> ```
>
> 这里 TemporarilyStopReportingErrors 是一个类型，其构造函数作为副作用关闭错误报告，而其释放方法将其重新打开。我认为这种（不幸地广泛存在）的做法是对 using 语句的滥用；程序副作用不是资源，在构造函数和释放器中引起全局副作用似乎是个坏主意。我会改用 try-finally 结构编写此代码。

```
using-statement:
    using ( resource-acquisition ) embedded-statement

resource-acquisition:
    local-variable-declaration
    expression
```

*resource* 是一个实现 System.IDisposable 的类或结构体，其中包含一个名为 Dispose 的单个无参数方法。使用资源的代码可以调用 Dispose 来表示资源不再需要。如果未调用 Dispose，则由于垃圾回收，最终会自动释放。

> **JOSEPH ALBAHARI** 调用 Dispose 以任何方式都不影响垃圾回收：对象在（且仅在）没有其他对象引用它时才有资格进行自动垃圾回收。同样，垃圾回收也不影响释放：除非你编写了一个显式进行此调用的终结器（析构函数），否则垃圾收集器不会调用 Dispose。
>
> Dispose 方法中最常执行的两个活动是释放非托管资源以及对其他被引用或“拥有”的对象调用 Dispose。也可以在终结器内部释放非托管资源，尽管这种操作意味着要等待不确定的时间让垃圾收集器触发。这就是为什么存在 IDisposable。

如果 *resource-acquisition* 的形式是 *local-variable-declaration*，则 *local-variable-declaration* 的类型必须是 dynamic 或可以隐式转换为 `System.IDisposable` 的类型。如果 *resource-acquisition* 的形式是 *expression*，则该表达式必须可以隐式转换为 `System.IDisposable`。

在 *resource-acquisition* 中声明的局部变量是只读的，并且必须包含初始值设定项。如果嵌入语句尝试修改这些局部变量（通过赋值或 ++ 和 -- 运算符）、获取它们的地址或将它们作为 ref 或 out 参数传递，则会发生编译时错误。

using 语句被翻译为三个部分：获取、使用和释放。资源的使用被隐式包含在包含 finally 子句的 try 语句中。此 finally 子句释放资源。如果获取到 null 资源，则不会调用 Dispose，也不会抛出异常。如果资源的类型为 dynamic，则在获取期间通过隐式动态转换 (§6.1.8) 动态转换为 IDisposable，以确保在进行使用和释放之前转换成功。

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

在任何展开中，资源变量在嵌入语句中都是只读的，而 d 变量在嵌入语句中不可访问且对嵌入语句不可见。

> **PETER SESTOFT** 感谢上述规则，using 语句也可以（被）用于以这种风格声明只读局部变量：
>
> ```csharp
> using (MyClass v = ...)
> using (MyStruct s = ...) {
>     ...
> }
> ```
>
> 事实上，这是在 C# 中声明不可变局部变量的唯一方法，但它很丑陋且奇怪。而且，它仅适用于实现 IDisposable 接口的类型 MyClass 和 MyStruct，而不适用于 int 和 string 等。例如，从语言设计的角度来看，也许令人困惑的是，与 struct 类型的只读字段 (§10.5.2 和 §7.6.4) 不同，struct 类型 MyStruct 的不可变资源变量 s 被视为变量，而不是值。因此，方法调用 s.SetX() 作用于存储在 s 中的结构体，而不是它的副本。总的来说，这种行为表明在 C# 中声明不可变局部变量和参数的机制是存在的，但遗憾的是并不以可用的形式存在。
