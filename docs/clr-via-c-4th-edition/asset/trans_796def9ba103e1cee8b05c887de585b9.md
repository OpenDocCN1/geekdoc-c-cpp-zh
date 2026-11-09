
当然，如果你确实编写了持有锁的代码，那么代码不应长时间持有锁，因为这会增加线程阻塞的可能性。在本章后面的“异步同步”一节中，我将展示一种使用集合类来避免长时间持有锁的技术。

最后，对于计算密集型工作，你可以使用任务（在第27章讨论）来避免大量线程同步构造。我尤其喜欢的是，每个任务都可以关联一个或多个延续任务，当某个操作完成时，这些延续任务会通过某个线程池线程执行。这比让一个线程阻塞等待某个操作完成要好得多。对于 I/O 密集型工作，调用各种 XxxAsync 方法，使你的代码在 I/O 操作完成后继续运行；这类似于任务的 continue-with 任务。

### 著名的双重检查锁定技术

有一种著名的技术叫双重检查锁定，希望将单例对象的构造推迟到应用程序请求它时（有时称为延迟初始化）的开发者会使用这种技术。如果应用程序从未请求该对象，它就永远不会被构造，从而节省时间和内存。当多个线程同时请求该单例对象时，就会出现一个潜在问题。在这种情况下，必须使用某种形式的线程同步来确保该单例对象只被构造一次。

这种技术之所以著名，并不是因为它特别有趣或有用。它之所以著名，是因为关于它的文章很多。这种技术曾在 Java 中被大量使用，后来人们发现 Java 无法保证它在所有地方都能正常工作。描述该问题的著名文档可以在以下网页找到：www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html。

无论如何，你会很高兴知道，由于 CLR 的内存模型和 volatile 字段访问（在第29章描述），CLR 完全支持双重检查锁定技术。下面是用 C# 实现双重检查锁定技术的演示代码。

```csharp
internal sealed class Singleton {
   // s_lock is required for thread safety and having this object assumes that creating
   // the singleton object is more expensive than creating a System.Object object and that
   // creating the singleton object may not be necessary at all. Otherwise, it is more
   // efficient and easier to just create the singleton object in a class constructor
   private static readonly Object s_lock = new Object();

   // This field will refer to the one Singleton object
   private static Singleton s_value = null;

   // Private constructor prevents any code outside this class from creating an instance
   private Singleton() {
      // Code to initialize the one Singleton object goes here...
   }

   // Public, static method that returns the Singleton object (creating it if necessary)
   public static Singleton GetSingleton() {
        // If the Singleton was already created, just return it (this is fast)
        if (s_value != null) return s_value;

        Monitor.Enter(s_lock);   // Not created, let 1 thread create it
        if (s_value == null) {
            // Still not created, create it
            Singleton temp = new Singleton();

            // Save the reference in s_value (see discussion for details)
            Volatile.Write(ref s_value, temp);
        }
        Monitor.Exit(s_lock);

        // Return a reference to the one Singleton object
        return s_value;
    }
}
```

双重检查锁定技术背后的思想是，对 GetSingleton 方法的调用会快速检查 s_value 字段，以查看对象是否已经创建；如果已经创建，该方法就返回对它的引用。这里美妙之处在于，对象构造完成后不再需要线程同步；应用程序将运行得非常快。另一方面，如果第一个调用 GetSingleton 方法的线程发现对象尚未创建，它就会获取线程同步锁，以确保只有一个线程构造该单例对象。这意味着，性能损失只会在某个线程首次查询该单例对象时发生。

现在，让我解释一下为什么这种模式在 Java 中不起作用。Java 虚拟机在 GetSingleton 方法开始时将 s_value 的值读入一个 CPU 寄存器，然后在计算第二个 if 语句时只查询该寄存器，导致第二个 if 语句始终计算为 true，最终多个线程创建了 Singleton 对象。当然，这种情况只在多个线程恰好同时调用 GetSingleton 时才会发生，而在大多数应用程序中这非常不可能。这就是为什么它在 Java 中如此长时间未被发现。

在 CLR 中，调用任何锁方法都是一个完整的内存栅栏，并且你在栅栏之前进行的任何变量写入都必须在栅栏之前完成，而栅栏之后的任何变量读取都必须在其之后开始。对于 GetSingleton 方法，这意味着在调用 Monitor.Enter 之后必须重新读取 s_value 字段；它不能在此方法调用期间缓存在寄存器中。

在 GetSingleton 内部，你会看到对 Volatile.Write 的调用。下面是它正在解决的问题。假设你在第二个 if 语句内部有以下代码行。

```csharp
        s_value = new Singleton();   // This is what you'd ideally like to write
```

你会期望编译器生成这样的代码：为 Singleton 分配内存，调用构造函数来初始化字段，然后将引用赋给 s_value 字段。让一个值对其他线程可见称为发布。但编译器也可以这样做：为 Singleton 分配内存，将引用发布（赋值）到 s_value，然后调用构造函数。从单个线程的角度来看，像这样改变顺序没有影响。但是，如果在将引用发布到 s_value 之后、调用构造函数之前，另一个线程调用了 GetSingleton 方法，会怎样呢？该线程会看到 s_value 不为 null，并开始使用 Singleton 对象，但它的构造函数尚未执行完成！这可能是一个非常难以追踪的 bug，特别是因为它完全取决于时序。

对 Volatile.Write 的调用修复了这个问题。它确保 temp 中的引用只有在构造函数执行完成后才能发布到 s_value 中。解决这个问题的另一种方法是用 C# 的 volatile 关键字标记 s_value 字段。这会使对 s_value 的写入成为 volatile 写入，同样，构造函数必须先运行完成，写入才能发生。不幸的是，这也会使所有读取都成为 volatile 读取，而由于这并不需要，你只会损害性能而没有任何好处。

在本节开头，我提到双重检查锁定技术并没有那么有趣。在我看来，开发者认为它很酷，并且使用它的频率远远超过应有的程度。在大多数场景中，这种技术实际上会损害效率。下面是一个简单得多的 Singleton 类版本，其行为与前一版本相同。这个版本不使用双重检查锁定技术。

```csharp
internal sealed class Singleton {
    private static Singleton s_value = new Singleton();

    // Private constructor prevents any code outside this class from creating an instance
    private Singleton() {
        // Code to initialize the one Singleton object goes here...
    }

    // Public, static method that returns the Singleton object (creating it if necessary)
    public static Singleton GetSingleton() { return s_value; }
}
```

因为 CLR 会在代码首次尝试访问某个类型的成员时自动调用该类型的类构造函数，所以当某个线程首次查询 Singleton 的 GetSingleton 方法时，CLR 将自动调用类构造函数，从而创建该对象的一个实例。此外，CLR 已经确保对类构造函数的调用是线程安全的。我在第8章解释了所有这些内容。这种方法的一个缺点是，当类的任何成员首次被访问时，类型构造函数就会被调用。如果 Singleton 类型定义了一些其他静态成员，那么访问其中任何一个成员时都会创建 Singleton 对象。有些人通过定义嵌套类来规避这个问题。

让我向你展示第三种生成单个 Singleton 对象的方法。

```csharp
internal sealed class Singleton {
    private static Singleton s_value = null;

    // Private constructor prevents any code outside this class from creating an instance
    private Singleton() {
        // Code to initialize the one Singleton object goes here...
    }

    // Public, static method that returns the Singleton object (creating it if necessary)
    public static Singleton GetSingleton() {
        if (s_value != null) return s_value;
```
