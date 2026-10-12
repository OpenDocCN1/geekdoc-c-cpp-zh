
## 选择锁对象

无论是显式使用 `lock` 关键字还是 `Monitor` 类，程序员仔细选择锁对象都是至关重要的。

在之前的示例中，同步变量 `_Sync` 被声明为私有的且只读的。将其声明为只读是为了确保在 `Monitor.Enter()` 和 `Monitor.Exit()` 的调用之间值不会改变。这允许在进入和退出同步块之间建立关联。

类似地，代码将 `_Sync` 声明为私有，以便类外部的任何同步块都不能同步相同的对象实例，从而导致代码阻塞。

如果数据是公有的，同步对象可以是公有的，以便其他类可以使用相同的对象实例进行同步。然而，这使得避免死锁变得更加困难。幸运的是，这种模式的需求很少。对于公有数据，最好完全将同步留在类外，允许调用代码使用其自己的同步对象获取锁。

同步对象不能是值类型这一点很重要。如果对值类型使用 `lock` 关键字，编译器将报告错误。（在显式访问 `System.Threading.Monitor` 类的情况下 [而非通过 `lock`]，编译时不会发生此类错误。相反，代码将在调用 `Monitor.Exit()` 时抛出异常，表明没有对应的 `Monitor.Enter()` 调用。）问题在于使用值类型时，运行时创建值的副本，将其放置到堆中（发生装箱），并将装箱后的值传递给 `Monitor.Enter()`。类似地，`Monitor.Exit()` 接收原始变量的装箱副本。结果是 `Monitor.Enter()` 和 `Monitor.Exit()` 接收不同的同步对象实例，因此两次调用之间不存在关联。

## 为什么应避免对 this、typeof(type) 和 string 进行锁定

一种看似合理的模式是对类中的实例数据锁定 `this` 关键字，对静态数据锁定从 `typeof(type)` 获得的类型实例（例如，`typeof(MyType)`）。当使用 `this` 时，这种模式为与特定对象实例关联的所有状态提供同步目标；当使用 `typeof(type)` 时，则为类型的静态数据提供同步目标。问题是 `this`（或 `typeof(type)`）指向的同步目标可能会参与在无关代码块中创建的完全不同同步块的同步目标。换句话说，虽然只有实例内部的代码可以使用 `this` 关键字进行阻塞，但创建该实例的调用者可以将该实例传递给同步锁。

结果是，同步两个完全不同数据集的两个不同同步块可能会相互阻塞。虽然这种情况可能不太可能发生，但共享相同的同步目标可能会产生非预期的性能影响，在极端情况下甚至可能导致死锁。与对 `this` 甚至 `typeof(type)` 进行锁定相比，最好定义一个私有、只读的字段，除了拥有访问权限的类之外，没有其他人会在其上阻塞。

另一种应避免的锁类型是 `string`，因为字符串驻留的原因。如果相同的 `string` 常量出现在多个位置，这些位置很可能都引用同一个实例，从而使锁的范围比预期的要广泛得多。

总而言之，你应该使用类型为 `object` 的每同步上下文实例作为锁目标。

## 准则

- 避免对 `this`、`typeof()` 或字符串进行加锁。
- 请声明一个单独的、只读的、类型为 `object` 的同步变量，用作同步目标。

## 高级主题

## 避免使用 MethodImplAttribute 进行同步

在 .NET 1.0 中引入的一种同步机制是 `MethodImplAttribute`。当与 `MethodImplOptions.Synchronized` 方法结合使用时，该属性将方法标记为同步方法，以便一次只有一个线程可以执行该方法。为了实现这一点，JIT 基本上将该方法视为被 `lock(this)` 包围，或者在静态方法的情况下，对类型进行加锁。这种实现意味着，事实上，该方法和同一类上所有装饰有相同属性和枚举参数的其他方法都是同步的——而不是每个方法相对于自身进行同步。换句话说，给定同一类上装饰有该属性的两个或多个方法，一次只能执行其中一个，正在执行的那个会阻塞其他线程对该方法本身或类中具有相同装饰的其他方法的所有调用。此外，由于同步是基于 `this`（甚至更糟的是基于 `type`）进行的，它遭受了前面部分讨论过的 `lock(this)`（或者更糟的是，对于静态方法）带来的同样弊端。因此，避免使用该属性是最佳实践。

## 准则

- 避免使用 `MethodImplAttribute` 进行同步。

## 将字段声明为 volatile

在某些情况下，编译器或 CPU 可能会优化代码，使得指令不会按编码的确切顺序执行，或者某些指令被优化掉。当代码在单个线程上执行时，这类优化是无害的。然而，在多个线程的情况下，这类优化可能会产生意想不到的后果，因为优化可能会改变某个字段的读取或写入操作相对于另一个线程对同一字段的访问的执行顺序。

稳定此行为的一种方法是使用 `volatile` 关键字声明字段。该关键字强制所有对 `volatile` 字段的读取和写入在代码标识的确切位置发生，而不是在优化产生的其他位置。`volatile` 修饰符标识该字段容易受到硬件、操作系统或另一个线程的修改。因此，数据是“易变的”，关键字指示编译器和运行时更精确地处理它。（参见 http://bit.ly/CSharpReorderingOptimizations 以获取更多详细信息。）

总体而言，`volatile` 修饰符的使用很少见，且伴随复杂的并发症，很可能导致错误的使用。除非你绝对确定 `volatile` 的使用情况，否则优先推荐使用 `lock` 而不是 `volatile` 修饰符。

## 使用 System.Threading.Interlocked 类

迄今为止描述的互斥模式提供了处理进程（应用程序域）内同步的最小工具集。然而，使用 `System.Threading.Monitor` 进行同步是一个相对昂贵的操作，而处理器直接支持的替代方案针对特定的同步模式。

代码清单 20.6 将 `_Data` 设置为新值，只要前面的值为 null。如方法名所示，此模式是比较/交换模式。不需要手动对行为等效的比较和交换代码加锁，`Interlocked.CompareExchange()` 方法提供了一种内置的同步操作方法，执行相同的值（null）检查，如果值等于第二个参数，则更新第一个参数。表 20.2 显示了 `Interlocked` 支持的其他同步方法。

## 代码清单 20.6：使用 System.Threading.Interlocked 进行同步

```csharp
public class SynchronizationUsingInterlocked
{
    private static object _Data;
    // Initialize data if not yet assigned
    static void Initialize(object newValue)
    {
        // If _Data is null, then set it to newValue
        Interlocked.CompareExchange(
            ref _Data, newValue, null);
    }
    // ...
}
```

## 表 20.2：Interlocked 的同步相关方法

| 方法签名 | 描述 |
| :--- | :--- |
| `public static T CompareExchange<T>(ref T location, T value, T comparand)` | 检查 `location` 中 `comparand` 的值。如果值相等，则将 `location` 设置为 `value` 并返回存储在 `location` 中的原始数据。 |
| `public static T Exchange<T>(ref T location, T value)` | 将 `location` 赋值为 `value` 并返回先前的值。 |
| `public static int Decrement(ref int location)` | 将 `location` 递减 1。它等效于前缀 `--` 运算符，除了 `Decrement()` 是线程安全的。 |
| `public static int Increment(ref int location)` | 将 `location` 递增 1。它等效于前缀 `++` 运算符，除了 `Increment()` 是线程安全的。 |
| `public static int Add(ref int location, int value)` | 将 `value` 加到 `location` 并将结果赋值给 `location`。它等效于 `+=` 运算符。 |
| `public static long Read(ref long location)` | 在单个原子操作内返回 64 位值。 |

这些方法中的大部分都具有额外的数据类型签名重载，例如对 `long` 的支持。表 20.2 提供了一般签名和描述。

请注意，你可以使用 `Increment()` 和 `Decrement()` 来替代代码清单 20.5 中同步的 `++` 和 `--` 运算符，这样做会产生更好的性能。另外请注意，如果另一个线程使用非 Interlocked 方法访问 `_Count`，这两个访问将不会正确同步。

## 多线程的事件通知

开发人员经常忽略同步的一个领域是触发事件。发布事件的不安全线程代码类似于代码清单 20.7。

### 代码清单 20.7：触发事件通知

```csharp
// Not thread-safe
if (OnTemperatureChanged != null)
{
    // Call subscribers
    OnTemperatureChanged(
        this, new TemperatureEventArgs(value));
}
```

只要此方法与事件订阅者之间没有竞态条件，这段代码就是有效的。然而，代码不是原子的，因此多个线程可能会引入竞态条件。有可能在检查 `OnTemperatureChange` 是否为 `null` 和实际触发事件之间，`OnTemperatureChange` 可能被设置为 `null`，从而抛出 `NullReferenceException`。换句话说，如果多个线程可能同时访问委托，则有必要对委托的分配和触发进行同步。

C# 6.0 对此困境的解决方案很简单。只需使用空条件运算符即可：

```csharp
OnTemperature?.Invoke(
    this, new TemperatureEventArgs(value));
```

空条件运算符是专门设计为原子的，因此该委托调用实际上是原子的。关键，显然，是记住利用空条件运算符。

虽然需要更多的代码，但在 C# 6.0 之前线程安全的委托调用也不特别困难。这种方法有效是因为添加和移除监听者的运算符是线程安全的且是静态的（运算符重载是通过静态方法完成的）。为了更正代码清单 20.7 并使其线程安全，请分配一个副本，检查该副本是否为 null，并触发该副本（参见代码清单 20.8）。

### 代码清单 20.8：线程安全的事件通知

```csharp
// ...
TemperatureChangedHandler localOnChange =
    OnTemperatureChanged;
if (localOnChange != null)
{
    // Call subscribers
    localOnChange(
        this, new TemperatureEventArgs(value));
}
// ...
```

鉴于委托是引用类型，也许令人惊讶的是，分配一个局部变量然后使用局部变量触发就足以使空检查线程安全。由于 `localOnChange` 指向 `OnTemperatureChange` 指向的相同位置，你可能会认为 `OnTemperatureChange` 中的任何变化都会反映在 `localOnChange` 中。

然而，事实并非如此：任何对 `OnTemperatureChange += <listener>` 的调用都不会向 `OnTemperatureChange` 添加一个新的委托，而是将其赋值为一个完全新的多播委托，而对 `localOnChange` 也指向的原始多播委托没有任何影响。这使得代码线程安全，因为只有单个线程会访问 `localOnChange` 实例，而如果添加或移除监听者，`OnTemperatureChange` 将是一个完全新的实例。

## 同步设计最佳实践

伴随着多线程编程的复杂性，也带来了处理这些复杂性的若干最佳实践。

## 避免死锁

随着同步的引入，死锁的可能性也随之而来。死锁发生在两个或多个线程相互等待对方释放

同步锁。例如，假设线程 1 请求 `_Sync1` 的锁，然后在释放 `_Sync1` 的锁之前又请求了 `_Sync2` 的锁。与此同时，线程 2 请求了 `_Sync2` 的锁，然后在释放 `_Sync2` 的锁之前请求了 `_Sync1` 的锁。这为死锁的发生埋下了伏笔。如果线程 1 和线程 2 都成功获取了各自的初始锁（分别为 `_Sync1` 和 `_Sync2`），然后再去获取第二把锁时，死锁实际上就会发生。

要发生死锁，必须同时满足以下四个基本条件：

- *互斥条件（Mutual exclusion）：* 一个线程（线程 A）独占某个资源，使得其他任何线程（线程 B）都无法获取相同的资源。
- *持有并等待（Hold and wait）：* 一个已经持有互斥资源的线程（线程 A）正在等待获取由另一个线程（线程 B）持有的资源。
- *不可剥夺（No preemption）：* 线程（线程 A）持有的资源不能被强制移除（线程 A 需要主动释放其锁定的资源）。
- *循环等待（Circular wait condition）：* 两个或更多线程形成一个循环链，它们锁定了相同的两个或更多资源，并且每个线程都在等待链中下一个线程持有的资源。

移除上述任何一个条件都可以防止死锁。

一种容易导致死锁的场景是：当两个或更多线程请求对相同的两个或更多同步目标（资源）的独占所有权，并且这些锁的请求顺序不同。当开发人员小心确保多次获取锁的操作始终按相同顺序进行时，可以避免这种情况。导致死锁的另一个原因是锁不是**可重入的（reentrant）**。如果一个线程的锁能够阻塞该线程本身——即当它重新请求同一把锁时——那么该锁就不是可重入的。例如，如果线程 A 获取了锁，然后重新请求同一把锁，但因为锁已被其自身拥有而处于阻塞状态，则该锁不可重入，额外的请求将导致死锁。

由 `lock` 关键字（基于底层的 `Monitor` 类）生成的代码是可重入的。但是，正如我们将在“更多同步类型”一节中所见，某些锁类型是不可重入的。

## 何时提供同步

正如前文所述，所有静态数据都应该是线程安全的。因此，需要同步机制来包围可变的静态数据。通常，程序员应声明私有静态变量，然后提供公有方法用于修改数据。如果可能涉及多线程访问，此类方法应在内部处理同步。

相反，实例状态通常不被期望包含同步机制。同步可能会显著降低性能，并增加锁竞争或死锁的可能性。除了那些明确设计为支持多线程访问的类之外，跨多个线程共享对象的程序员被期望自行处理共享数据的同步。

## 避免不必要的锁定

在不损害数据完整性的前提下，程序员应尽可能避免不必要的同步。例如，你应在线程之间使用不可变类型，这样就不需要同步（这种方法在 F# 等功能性编程语言中已被证明极具价值）。同样，你也应避免对线程安全操作（如读写小于原生（指针大小）整数值）进行锁定，因为这类操作本身就是自动原子的。

## 指导原则

- **切勿（DO NOT）** 以不同的顺序请求对相同的两个或更多同步目标的独占所有权。
- **应当（DO）** 确保并发持有多个锁的代码总是按相同顺序获取它们。
- **应当（DO）** 在公共 API 中封装可变静态数据，并包含同步逻辑。
- **避免（AVOID）** 对不大于原生（指针大小）整数的值的简单读取或写入进行同步，因为这类操作是自动原子的。

## 更多同步类型

除了 `System.Threading.Monitor` 和 `System.Threading.Interlocked` 之外，还有几种同步技术可供使用。

### 使用 System.Threading.Mutex

`System.Threading.Mutex` 在概念上类似于 `System.Threading.Monitor` 类（但不支持 `Pulse()` 方法），不同之处在于 `lock` 关键字并不使用 `Mutex`，并且 `Mutex` 可以被命名，从而支持跨多个进程的同步。使用 `Mutex` 类，你可以同步对文件或其他跨进程资源的访问。由于 `Mutex` 是一种跨进程资源，.NET 2.0 添加了支持，允许通过 `System.Security.AccessControl.MutextSecurity` 对象设置访问控制。`Mutex` 类的一个用途是限制应用程序只能同时运行一次，如清单 20.9 所示。

#### 清单 20.9：创建单实例应用程序

```
using System;
using System.Threading;
using System.Reflection;
public class Program
{
    public static void Main()
    {
        // Indicates whether this is the first
        // application instance
        bool firstApplicationInstance;
        // Obtain the mutex name from the full
        // assembly name
        string mutexName =
            Assembly.GetEntryAssembly().FullName;
        using(Mutex mutex = new Mutex(false, mutexName,
