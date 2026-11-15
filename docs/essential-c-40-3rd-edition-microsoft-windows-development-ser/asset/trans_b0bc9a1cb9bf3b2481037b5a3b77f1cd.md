

同样，代码将 _Sync 声明为私有，以便类外部的同步块无法同步同一个对象实例，从而导致代码阻塞。

如果数据是公共的，那么同步对象也可能是公共的，以便其他类可以使用同一个对象实例进行同步。这使得避免死锁变得更加困难。幸运的是，这种模式的需求很少。对于公共数据，最好将同步完全留在类之外，允许调用代码使用其自己的同步对象获取锁。

重要的是，同步对象不能是值类型。如果在值类型上使用 lock 关键字，编译器将报告错误。（在显式访问 System.Threading.Monitor 类 [而非通过 lock] 的情况下，编译时不会发生此类错误。相反，代码在调用 Monitor.Exit() 时会抛出异常，指示没有相应的 Monitor.Enter() 调用。）问题在于，当使用值类型时，运行时会对值进行副本，将其放置在堆上（发生装箱），并将装箱后的值传递给 Monitor.Enter()。同样，Monitor.Exit() 接收原始变量的装箱副本。结果是 Monitor.Enter() 和 Monitor.Exit() 接收不同的同步对象实例，因此两次调用之间没有关联。

## 为何应避免对 this、typeof(type) 和 string 进行锁定

一种常见的模式是为类中的实例数据对 this 关键字进行锁定，并为静态数据对从 typeof(type) 获得的类型实例进行锁定（例如，typeof(MyType)）。当使用 this 时，这种模式为与特定对象实例关联的所有状态提供同步目标；当使用 typeof(type) 时，则为类型的所有静态数据提供同步目标。问题在于，this（或 typeof(type)）所指向的同步目标可能会参与在不相关的代码块中创建的完全不同的同步块的同步目标。换句话说，虽然只有实例内部的代码可以使用 this 关键字进行阻塞，但创建该实例的调用者可以将该实例传递给同步锁。

结果是，同步两组完全不同数据的两个不同同步块可能会互相阻塞。虽然这种情况可能性不大，但共享同一个同步目标可能会产生意想不到的性能影响，在极端情况下甚至会导致死锁。与其对 this 或甚至 typeof(type) 进行锁定，不如定义一个私有、只读字段，只有有权访问它的类才会对其进行阻塞。

另一种应避免的锁类型是 string，原因是字符串驻留。如果同一个字符串常量出现在多个位置，那么所有位置很可能都引用同一个实例，这会使锁的范围远大于预期。

总结来说，为锁定目标使用每个同步上下文的 object 类型实例。

## 高级主题

### 避免使用 MethodImplAttribute 进行同步

.NET 1.0 引入的一种同步机制是 MethodImplAttribute。该属性与 MethodImplOptions.Synchronized 方法配合使用，用于将方法标记为同步，以便同一时间只有一个线程可以执行该方法。为了实现这一点，即时编译器基本上将该方法视为被 lock(this) 包围（对于静态方法则是对类型进行锁定）。这种实现意味着，实际上，同一个类上使用相同属性和枚举参数装饰的方法及其他所有方法都是同步的，而不仅仅是每个方法相对于自身。换句话说，对于同一个类上装饰了该属性的两个或多个方法，同一时间只能有一个方法能够执行，正在执行的方法会阻塞其他线程对其自身或类中任何其他带有相同装饰的方法的调用。此外，由于同步是在 this 上（或者更糟的是，在类型上），它会遭受与前一节讨论的 lock(this)（对于静态方法则更糟）相同的弊端。因此，最佳实践是完全避免使用该属性。

### 将字段声明为 volatile

有时，编译器和/或 CPU 可能会以这种方式优化代码，使得指令不按照编写的精确顺序发生，或者某些指令被优化掉。当代码在单个线程上执行时，此类优化是无害的。然而，在多线程情况下，此类优化可能会产生意想不到的后果，因为优化可能会改变字段读取或写入操作的执行顺序，相对于另一个线程对同一字段的访问。

稳定这一点的一种方法是使用 volatile 关键字声明字段。该关键字强制所有对 volatile 字段的读取和写入都发生在代码标识的精确位置，而不是优化产生的某个其他位置。volatile 修饰符标识该字段易受硬件、操作系统或另一个线程的修改。因此，数据是“易变”的，该关键字指示编译器和运行时更精确地处理它。

## 使用 System.Threading.Interlocked 类

迄今描述的互斥模式为在进程（应用程序域）内处理同步提供了最少的工具。然而，使用 System.Threading.Monitor 进行同步是一项相对昂贵的操作，而处理器直接支持的替代方案则针对特定的同步模式。

清单 19.5 在前一个值为 null 的情况下将 _Data 设置为新值。正如方法名所指示的，这种模式是比较/交换模式。与其在行为等效的比较和交换代码周围手动放置锁，不如使用 Interlocked.CompareExchange() 方法，它提供了一个用于同步操作的内置方法，用于对值（null）执行相同的检查，并在值相等时交换前两个参数。表 19.2 显示了 Interlocked 支持的其他同步方法。

### 清单 19.5：使用 System.Threading.Interlocked 进行同步

```
class SynchronizationUsingInterlocked
{
    private static object _Data;

    // Initialize data if not yet assigned.
    static void Initialize(object newValue)
    {
        // If _Data is null then set it to newValue.
        Interlocked.CompareExchange(
            ref _Data, newValue, null);
    }

    // ...
}
```

### 表 19.2：Interlocked 的同步相关方法

| 方法签名 | 描述 |
|---|---|
| `public static T CompareExchange<T>( T location, T value, T comparand );` | 检查 location 中的值是否等于 comparand。如果相等，则将 location 设置为 value 并返回 location 中原始存储的数据。 |
| `public static T Exchange<T>( T location, T value );` | 将 value 赋给 location 并返回先前的值。 |
| `public static int Decrement( ref int location );` | 将 location 减一。它相当于 -- 运算符，但 Decrement() 是线程安全的。 |
| `public static int Increment( ref int location );` | 将 location 加一。它相当于 ++ 运算符，但 Increment() 是线程安全的。 |
| `public static long Add( ref int location, int value );` | 将 value 添加到 location 并将结果赋给 location。它相当于 += 运算符。 |
| `public static long Read( ref long location );` | 在单个原子操作中返回一个 64 位值。 |

这些方法中的大多数都带有其他数据类型签名进行重载，例如对 long 的支持。表 19.2 提供了通用签名和描述。例如，System.Threading 命名空间直到 C# 2.0 才包含泛型方法签名，尽管早期版本包含非泛型等效项。

请注意，可以使用 Increment() 和 Decrement() 来代替清单 19.5 中同步的 ++ 和 -- 运算符，这样做可以获得更好的性能。还请注意，如果另一个线程访问了

