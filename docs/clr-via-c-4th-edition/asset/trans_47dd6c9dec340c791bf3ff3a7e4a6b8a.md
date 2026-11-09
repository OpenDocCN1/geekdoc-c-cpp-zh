
CreateInstanceAndUnwrap 实际上并不是 MarshalByRefType 类型的实例。CLR 通常不允许将一种类型的对象强制转换为不兼容的类型。然而，在这种情况下，CLR 确实允许这种强制转换，因为这个新类型具有与原始类型所定义的相同的实例成员。事实上，如果你使用代理对象调用 GetType，它实际上会对你撒谎，说它是一个 MarshalByRefType 对象。

不过，可以证明 CreateInstanceAndUnwrap 返回的对象实际上是对代理对象的引用。为此，我的 Ch22-1-AppDomains 应用程序调用 System.Runtime.Remoting.RemotingServices 的公共静态 IsTransparentProxy 方法，并传入 CreateInstanceAndUnwrap 返回的引用。从输出中可以看到，IsTransparentProxy 返回 true，表明该对象是一个代理。

现在，我的 Ch22-1-AppDomains 应用程序使用代理来调用 SomeMethod 方法。由于 mbrt 变量引用的是代理对象，因此会调用该方法的代理实现。代理实现使用代理对象内部的信息字段，将调用线程从默认 AppDomain 转换到新的 AppDomain。此线程现在执行的任何操作都在新 AppDomain 的安全和配置设置下运行。接下来，线程使用代理对象的 GCHandle 字段在新 AppDomain 中查找真实对象，然后使用该真实对象调用真正的 SomeMethod 方法。

有两种方法可以证明调用线程已从默认 AppDomain 转换到新的 AppDomain。首先，在 SomeMethod 方法内部，我调用 Thread.GetDomain().FriendlyName。这将返回 "AD #2"（输出可以证明这一点），因为该线程现在运行在使用 AppDomain.CreateDomain 并以 "AD #2" 作为友好名称参数创建的新 AppDomain 中。其次，如果你在调试器中单步执行代码并显示“调用堆栈”窗口，[AppDomain Transition] 行会标记线程跨越 AppDomain 边界进行转换的位置。请参见图 22-2 底部附近的“调用堆栈”窗口。

![](img/857bdf6cef9e242b53a37f88df9a1287_590_0.png)

**FIGURE 22-2** 调试器的“调用堆栈”窗口显示了 AppDomain 转换。

当真正的 `SomeMethod` 方法返回时，它会返回到代理的 `SomeMethod` 方法，后者将线程转换回默认 `AppDomain`，然后线程继续在默认 `AppDomain` 中执行代码。

> **注意** 当一个 `AppDomain` 中的线程调用另一个 `AppDomain` 中的方法时，该线程会在两个 `AppDomain` 之间转换。这意味着跨 `AppDomain` 边界的方法调用是同步执行的。然而，在任何给定时刻，一个线程只被认为处于一个 `AppDomain` 中，并且它使用该 `AppDomain` 的安全和配置设置来执行代码。如果你希望同时在多个 `AppDomains` 中执行代码，则应创建额外的线程，让它们在所需的任意 `AppDomains` 中执行所需的任意代码。

我的 `Ch22-1-AppDomains` 应用程序接下来要做的是调用 `AppDomain` 的公共静态 `Unload` 方法，强制 CLR 卸载指定的 `AppDomain`，包括加载到其中的所有程序集。系统会强制执行一次垃圾回收，以释放由正在卸载的 `AppDomain` 中的代码创建的所有对象。此时，默认 `AppDomain` 的 `mbrt` 变量仍然引用一个有效的代理对象；但是，该代理对象不再引用有效的 `AppDomain`（因为它已被卸载）。

当默认 `AppDomain` 尝试使用代理对象调用 `SomeMethod` 方法时，会调用该方法的代理实现。代理实现确定包含真实对象的 `AppDomain` 已被卸载，于是代理的 `SomeMethod` 方法会抛出 `AppDomainUnloadedException`，让调用方知道该操作无法完成。

哇！Microsoft 的 CLR 团队为确保 `AppDomain` 隔离做了大量工作，但这是重要的工作，因为这些功能被大量使用，而且开发者每天都在越来越多地使用它们。显然，通过按引用封送语义跨 `AppDomain` 边界访问对象会带来一些相关的性能开销，因此通常应尽量少用此功能。

我答应过你，会再多讲一点实例字段。派生自 `MarshalByRefObject` 的类型可以定义实例字段。但是，这些实例字段并未定义为代理类型的一部分，也不包含在代理对象内部。当你编写代码读取或写入派生自 `MarshalByRefObject` 的类型的实例字段时，JIT 编译器会生成代码，分别通过调用 `System.Object` 的 `FieldGetter` 或 `FieldSetter` 方法来使用代理对象（以查找真实的 `AppDomain`/对象）。这些方法是私有的且未记录在文档中；它们基本上就是使用反射来获取和设置字段值的方法。因此，尽管你可以访问派生自 `MarshalByRefObject` 的类型的字段，但性能特别差，因为 CLR 最终实际上会调用方法来执行字段访问。事实上，即使你访问的对象位于你自己的 `AppDomain` 中，性能也很差。^3

^3 如果 CLR 要求所有字段都是私有的（这是实现良好数据封装所推荐的），那么就不必存在 `FieldGetter` 和 `FieldSetter` 方法，并且从方法访问字段始终可以是直接访问，从而避免任何性能损失。

## 访问实例字段的性能

为了演示这种性能损失的严重性，我编写了以下代码。

```csharp
private sealed class NonMBRO : Object        { public Int32 x; }
private sealed class MBRO    : MarshalByRefObject { public Int32 x; }

private static void FieldAccessTiming() {
    const Int32 count = 100000000;
    NonMBRO nonMbro = new NonMBRO();
    MBRO mbro = new MBRO();

    Stopwatch sw = Stopwatch.StartNew();
    for (Int32 c = 0; c < count; c++) nonMbro.x++;
    Console.WriteLine("{0}", sw.Elapsed);   // 00:00:00.4073560

    sw = Stopwatch.StartNew();
    for (Int32 c = 0; c < count; c++) mbro.x++;
    Console.WriteLine("{0}", sw.Elapsed);   // 00:00:02.5388665
}
```

运行这段代码时，访问派生自 Object 的 NonMBRO 类的实例字段大约耗时 0.4 秒，而访问派生自 MarshalByRefObject 的 MBRO 类的实例字段耗时 2.54 秒。因此，访问派生自 MarshalByRefObject 的类的实例字段所需时间要长 6 倍多！

从可用性角度来看，派生自 MarshalByRefObject 的类型确实应避免定义任何静态成员。原因在于，静态成员始终在调用方 AppDomain 的上下文中访问。不会发生 AppDomain 转换，因为代理对象包含标识要转换到哪个 AppDomain 的信息，但在调用静态成员时没有代理对象。让一个类型的静态成员在一个 AppDomain 中执行，而实例成员在另一个 AppDomain 中执行，会造成非常别扭的编程模型。

由于第二个 AppDomain 中没有根，代理所引用的原始对象可能会被垃圾回收。当然，这并不理想。另一方面，如果原始对象被无限期地保留在内存中，那么代理可能已消失，而原始对象仍然存活；这同样不理想。CLR 通过使用租约管理器来解决此问题。当为对象创建代理时，CLR 会让该对象保持存活五分钟。如果五分钟后没有通过代理进行任何调用，则该对象会被停用，并在下一次垃圾回收时释放其内存。每次调用该对象后，租约管理器都会续订该对象的租约，以确保它在被停用之前再保留在内存中两分钟。如果应用程序在对象的租约过期后尝试通过代理调用该对象，CLR 会抛出 System.Runtime.Remoting.RemotingException。

可以通过重写 MarshalByRefObject 的虚方法 InitializeLifetimeService 来覆盖默认的五分钟和两分钟租约时间。有关更多信息，请参阅 .NET Framework SDK 文档中标题为“生命周期租约”的章节。
