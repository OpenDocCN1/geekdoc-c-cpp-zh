

```csharp
// Create a Timer object that knows to call our TimerCallback
// method once every 2000 milliseconds.
Timer t = new Timer(TimerCallback, null, 0, 2000);

// Wait for the user to hit <Enter>
Console.ReadLine();
}

private static void TimerCallback(Object t)
{
    // Display the date/time when this method got called.
    Console.WriteLine("In TimerCallback: " + DateTime.Now);

    // Force a garbage collection to occur for this demo.
    GC.Collect();
}
}
```

从命令提示符编译这段代码，不要使用任何特殊的编译器开关。当你运行生成的可执行文件时，你会发现 TimerCallback 方法只被调用了一次！

从上面的代码来看，你可能认为 TimerCallback 方法每 2,000 毫秒就会被调用一次。毕竟，创建了一个 Timer 对象，变量 t 引用了这个对象。只要 timer 对象存在，timer 就应该持续触发。但你会在 TimerCallback 方法中注意到，我通过调用 GC.Collect() 强制进行了一次垃圾回收。

当回收开始时，它首先假定堆中的所有对象都是不可达的（垃圾）；这包括 Timer 对象。然后，收集器检查应用程序的根，发现 Main 在初次赋值后就不再使用 t 变量。因此，应用程序没有变量引用 Timer 对象，垃圾回收就会回收它的内存；这会停止 timer，也解释了为什么 TimerCallback 方法只被调用一次。

假设你正在使用调试器逐句执行 Main，而恰好在 t 被赋予新 Timer 对象的地址之后发生了一次垃圾回收。然后，假设你尝试使用调试器的“快速监视”窗口查看 t 所引用的对象。你认为会发生什么？调试器无法显示该对象，因为它刚刚被垃圾回收了。大多数开发人员会认为这种行为非常出乎意料且不可取，因此 Microsoft 想出了一个解决方案。

当你使用 C# 编译器的 /debug 开关编译程序集时，编译器会将一个 System.Diagnostics.DebuggableAttribute（其 DebuggingModes 的 DisableOptimizations 标志被设置）应用到结果程序集中。在运行时，JIT 编译器编译方法时看到这个标志被设置，就会人为地将所有根的生命周期延长到方法末尾。以我的示例为例，JIT 编译器会欺骗自己，认为 Main 中的 t 变量必须存活到方法结束。因此，如果发生垃圾回收，垃圾回收器现在会认为 t 仍然是一个根，而 t 所引用的 Timer 对象将继续保持可达。Timer 对象将在回收中幸存下来，TimerCallback 方法将不断被调用，直到 Console.ReadLine 返回且 Main 退出。

要看到这一点，只需在命令提示符下重新编译程序，但这次指定 C# 编译器的 /debug 开关。当你运行生成的可执行文件时，你会看到 TimerCallback 方法被重复调用了！注意，C# 编译器的 /optimize+ 编译器开关会重新启用优化，因此进行此实验时不应指定该编译器开关。

JIT 编译器这样做是为了帮助你进行 JIT 调试。你现在可以正常启动应用程序（不附带调试器），如果该方法被调用，JIT 编译器会人为地将变量的生命周期延长到方法末尾。之后，如果你决定将调试器附加到进程，可以在先前编译的方法中设置断点并检查根变量。

所以现在你知道如何构建一个在调试构建中工作但在发布构建中不正确的程序了！既然没有开发者希望程序只有在调试时才能工作，我们肯定可以对程序采取一些措施，使它在任何构建类型下都能一直正常工作。

你可以尝试将 Main 方法修改为这样：

```csharp
public static void Main() {
    // Create a Timer object that knows to call our TimerCallback
    // method once every 2000 milliseconds.
    Timer t = new Timer(TimerCallback, null, 0, 2000);

    // Wait for the user to hit <Enter>
    Console.ReadLine();

    // Refer to t after ReadLine (this gets optimized away)
    t = null;
}
```

然而，如果你编译这段代码（不使用 /debug+ 开关）并运行生成的可执行文件，你会看到 TimerCallback 方法仍然只被调用一次。这里的问题在于 JIT 编译器是一个优化编译器，将局部变量或参数变量设置为 null 与根本不引用该变量是一样的。换句话说，JIT 编译器将 t = null; 这一行完全优化掉了，因此程序仍然无法按我们期望的方式工作。修改 Main 方法的正确方法如下：

```csharp
public static void Main() {
    // Create a Timer object that knows to call our TimerCallback
    // method once every 2000 milliseconds.
    Timer t = new Timer(TimerCallback, null, 0, 2000);

    // Wait for the user to hit <Enter>
    Console.ReadLine();

    // Refer to t after ReadLine (t will survive GCs until Dispose returns)
    t.Dispose();
}
```

现在，如果你编译这段代码（不使用 /debug+ 开关）并运行生成的可执行文件，

与对象 B 相邻。在垃圾回收中幸存下来的对象（对象 A、B 和 D）被认为是第 1 代。第 1 代中的对象已经被垃圾回收器检查过一次。堆现在的样子如图 21-5 所示。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_510_0.png)

**图 21-5** 在一次回收之后，第 0 代的幸存者被提升到第 1 代；第 0 代已为空。

一次垃圾回收之后，第 0 代不包含任何对象。与往常一样，新对象将被分配到第 0 代。图 21-6 显示了应用程序正在运行并分配对象 F 到 K。此外，在应用程序运行期间，对象 B、H 和 J 变得不可达，应在某个时候回收它们的内存。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_510_1.png)

**图 21-6** 新对象被分配到第 0 代；第 1 代存在一些垃圾。

现在假设尝试分配对象 L 会使第 0 代超出其预算。由于第 0 代已达到预算，必须启动一次垃圾回收。启动垃圾回收时，垃圾回收器必须决定要检查哪些代。之前我提到，当 CLR 初始化时，它会为第 0 代选择预算。同样，它也会为第 1 代选择预算。

启动垃圾回收时，垃圾回收器还会查看第 1 代占用了多少内存。在这种情况下，第 1 代占用的内存远低于其预算，因此垃圾回收器只检查第 0 代中的对象。请再次考虑分代式垃圾回收器所做的假设。第一个假设是，新创建的对象具有较短的生存期。因此，第 0 代中很可能有大量垃圾，回收第 0 代将会回收大量内存。垃圾回收器会直接忽略第 1 代中的对象，这可以加快垃圾回收过程。

显然，忽略第 1 代中的对象提高了垃圾回收器的性能。然而，垃圾回收器提升性能的更大原因在于它不需要遍历托管堆中的每个对象。如果某个根或对象引用了旧代中的对象，垃圾回收器可以忽略这些较旧对象的任何内部引用，从而减少构建可达对象图所需的时间。当然，旧对象的某个字段也可能引用新对象。为了确保这些旧对象已更新的字段被检查，垃圾回收器使用了 JIT 编译器内部的一种机制：当对象的引用字段发生变化时，会设置一个位。这种支持让垃圾回收器知道自上次回收以来哪些旧对象（如果有）被写入过。只有那些字段发生过变化的旧对象需要被检查，以确定它们是否引用

