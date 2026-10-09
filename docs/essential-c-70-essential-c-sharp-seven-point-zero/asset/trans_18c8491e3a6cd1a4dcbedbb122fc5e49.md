

总而言之，你应该使用类型为 `object` 的每同步上下文实例作为锁目标。

## 准则

- 避免对 `this`、`typeof()` 或字符串进行加锁。
- 请声明一个单独的、只读的、类型为 `object` 的同步变量，用作同步目标。

# 高级主题

## 避免使用 MethodImplAttribute 进行同步

在 .NET 1.0 中引入的一种同步机制是 `MethodImplAttribute`。当与 `MethodImplOptions.Synchronized` 方法结合使用时，该属性将方法标记为同步方法，以便一次只有一个线程可以执行该方法。为了实现这一点，JIT 基本上将该方法视为被 `lock(this)` 包围，或者在静态方法的情况下，对类型进行加锁。这种实现意味着，事实上，该方法和同一类上所有装饰有相同属性和枚举参数的其他方法都是同步的——而不是每个方法相对于自身进行同步。换句话说，给定同一类上装饰有该属性的两个或多个方法，一次只能执行其中一个，正在执行的那个会阻塞其他线程对该方法本身或类中具有相同装饰的其他方法的所有调用。此外，由于同步是基于 `this`（甚至更糟的是基于 `type`）进行的，它遭受了前面部分讨论过的 `lock(this)`（或者更糟的是，对于静态方法）带来的同样弊端。因此，避免使用该属性是最佳实践。

## 准则

- 避免使用 `MethodImplAttribute` 进行同步。

## 将字段声明为 volatile

在某些情况下，编译器或 CPU 可能会优化代码，使得指令不会按编码的确切顺序执行，或者某些指令被优化掉。当代码在单个线程上执行时，这类优化是无害的。然而，在多个线程的情况下，这类优化可能会产生意想不到的后果，因为优化可能会改变某个字段的读取或写入操作相对于另一个线程对同一字段的访问的执行顺序。

稳定此行为的一种方法是使用 volatile 关键字声明字段。该关键字强制所有对 volatile 字段的读取和写入在代码标识的确切位置发生，而不是在优化产生的其他位置。volatile 修饰符标识该字段容易受到硬件、操作系统或另一个线程的修改。因此，数据是“易变的”，关键字指示编译器和运行时更精确地处理它。（参见 http://bit.ly/CSharpReorderingOptimizations 以获取更多详细信息。）

总体而言，volatile 修饰符的使用很少见，且伴随复杂的并发症，很可能导致错误的使用。除非你绝对确定 volatile 的使用情况，否则优先推荐使用 lock 而不是 volatile 修饰符。

## 使用 System.Threading.Interlocked 类

迄今为止描述的互斥模式提供了处理进程（应用程序域）内同步的最小工具集。然而，使用 System.Threading.Monitor 进行同步是一个相对昂贵的操作，而处理器直接支持的替代方案针对特定的同步模式。

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

