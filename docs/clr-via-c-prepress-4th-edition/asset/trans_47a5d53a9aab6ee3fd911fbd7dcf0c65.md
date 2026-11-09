
开发人员每天都会……显然，通过使用按引用封送语义跨 AppDomain 边界访问对象会带来一些性能成本，因此通常希望将这一特性的使用降到最低。

我答应过你会再多谈一些实例字段。派生自 MarshalByRefObject 的类型可以定义实例字段。然而，这些实例字段并不被定义为代理类型的一部分，也不包含在代理对象内部。当你编写读取或写入派生自 MarshalByRefObject 的类型的实例字段的代码时，JIT 编译器会分别通过调用 System.Object 的 FieldGetter 或 FieldSetter 方法来生成使用代理对象（以找到真正的 AppDomain/对象）的代码。这些方法是私有的且未记录；它们基本上就是使用反射来获取和设置字段值的方法。因此，尽管你可以访问派生自 MarshalByRefObject 的类型的字段，但性能特别差，因为 CLR 实际上最终会调用方法来执行字段访问。事实上，即使你访问的对象位于你自己的 AppDomain 中，性能也很差。<sup>30</sup>

30 如果 CLR 要求所有字段都是私有的（这是良好数据封装所推荐的做法），那么 FieldGetter 和 FieldSetter 方法就不必存在，从方法中访问字段也始终可以直接进行，从而避免任何性能损失。

## 访问实例字段的性能

为了演示这种性能损失的严重程度，我编写了以下代码：

```csharp
private sealed class NonMBRO : Object            { public Int32 x; }
private sealed class MBRO     : MarshalByRefObject { public Int32 x; }

private static void FieldTiming()
{
    const Int32 count = 100000000;
    NonMBRO nonmbro = new NonMBRO();
    MBRO mbro = new MBRO();

    Stopwatch sw = Stopwatch.StartNew();
    for (Int32 c = 0; c < count; c++) nonmbro.x++;
    Console.WriteLine("{0}", sw.Elapsed);       // 00:00:00.4073560

    sw = Stopwatch.StartNew();
    for (Int32 c = 0; c < count; c++) mbro.x++;
    Console.WriteLine("{0}", sw.Elapsed);       // 00:00:02.5388665
}
```

当我运行这段代码时，访问派生自 Object 的 NonMBRO 类的实例字段耗时约 0.4 秒，而访问派生自 MarshalByRefObject 的 MBRO 类的实例字段耗时 2.54 秒。因此，访问派生自 MarshalByRefObject 的类的实例字段所需时间超过约 6 倍！

新的 AppDomain。如果对象的类型派生自 MarshalByRefObject，CLR 会为它创建一个代理，并按引用封送它。如果对象的类型标记为 [Serializable]，CLR 会将该对象（及其子对象）序列化为字节数组，将字节数组封送到新的 AppDomain 中，然后将字节数组反序列化为对象图，并将对象图的根传入 MethodArgAndReturn 方法。

在这个特定演示中，我跨 AppDomain 边界传递一个 System.String 对象。System.String 类型不是派生自 MarshalByRefObject，因此 CLR 无法创建代理。幸运的是，System.String 标记为 [Serializable]，因此 CLR 可以按值封送它，这使代码能够工作。请注意，对于 String 对象，CLR 会执行一项特殊优化。跨 AppDomain 边界封送 String 对象时，CLR 只是将对该 String 对象的引用传递过边界；它不会复制该 String 对象。CLR 能够提供这项优化，是因为 String 对象是不可变的；因此，一个 AppDomain 中的代码不可能破坏 String 对象的字符。有关 String 不可变性的更多信息，请参见第 14 章“字符、字符串与文本处理”。

在 MethodArgAndReturn 内部，我显示传入其中的字符串，以表明该字符串跨过了 AppDomain 边界，然后我创建 NonMarshalableType 类型的实例，并将对该对象的引用返回给默认 AppDomain。由于 NonMarshalableType 不是派生自 System.MarshalByRefObject，也没有标记 [Serializable] 自定义特性，因此不允许 MethodArgAndReturn 按引用或按值封送该对象——该对象根本无法跨 AppDomain 边界封送！为了报告这一点，MethodArgAndReturn 在默认 AppDomain 中抛出 SerializationException。由于我的程序没有捕获这个异常，程序就直接终止了。

## AppDomain 卸载

AppDomain 的一大特性是你可以卸载它们。卸载 AppDomain 会使 CLR 卸载该 AppDomain 中的所有程序集，并且 CLR 还会释放该 AppDomain 的加载器堆。要卸载 AppDomain，可调用 AppDomain 的 Unload 静态方法（如 Ch22-1-AppDomains 应用程序所做的那样）。此调用会使 CLR 执行大量操作来正常卸载指定的 AppDomain：

1. CLR 挂起进程中所有曾经执行过托管代码的线程。

2. CLR 检查所有线程的堆栈，以确定哪些线程当前正在被卸载的 AppDomain 中执行代码，或者哪些线程可能稍后返回到正在被卸载的 AppDomain 中的代码。CLR 强制任何堆栈上包含正在卸载的 AppDomain 的线程抛出 `ThreadAbortException`（恢复该线程的执行）。这会导致这些线程展开，并在退出时执行任何 `finally` 块，以便清理代码得以执行。如果没有代码捕获 `ThreadAbortException`，它最终会变成 CLR 会吞掉的未处理异常；线程死亡，但允许进程继续运行。这很不寻常，因为对于所有其他未处理异常，CLR 都会终止进程。

   **重要** CLR 不会立即中止当前正在 `finally` 块、catch 块、类构造函数、关键执行区域或非托管代码中执行代码的线程。如果 CLR 允许这样做，那么清理代码、错误恢复代码、类型初始化代码、关键代码或 CLR 一无所知的任意代码将无法完成，导致应用程序行为不可预测，并可能带来安全漏洞。正在中止的线程可以完成执行这些代码块，然后在该代码块结束时，CLR 强制该线程抛出 `ThreadAbortException`。

3. 在步骤 #2 中发现的所有线程都已离开该 AppDomain 后，CLR 随后遍历堆，并在每个代理对象中设置一个标志，这些代理对象曾引用由被卸载的 AppDomain 创建的对象。这些代理对象现在知道它们所引用的真实对象已经不存在了。如果现在有任何代码在无效的代理对象上调用方法，该方法将抛出 `AppDomainUnloadedException`。

4. CLR 强制进行垃圾回收，回收由现已卸载的 AppDomain 创建的任何对象所使用的内存。这些对象的 `Finalize` 方法会被调用，使这些对象有机会正确地清理自身。

5. CLR 恢复所有剩余的线程。调用 `AppDomain.Unload` 的线程现在将继续运行；对 `AppDomain.Unload` 的调用是同步发生的。

我的 Ch22-1-AppDomains 应用程序只使用一个线程完成所有工作。每当我的代码调用 `AppDomain.Unload` 时，被卸载的 AppDomain 中都没有线程，因此 CLR 不必抛出任何 `ThreadAbortException` 异常。本章后面我会更详细地讨论 `ThreadAbortException`。

顺便说一下，当线程调用 `AppDomain.Unload` 时，CLR 会等待 10 秒，让正在卸载的 AppDomain 中的线程离开它。如果 10 秒后，调用 `AppDomain.Unload` 的线程仍未返回，它将抛出 `CannotUnloadAppDomainException`，并且该 AppDomain 将来可能会也可能不会被卸载。

**注意** 如果调用 `AppDomain.Unload` 的线程位于正在卸载的 AppDomain 中，CLR 会创建另一个线程来尝试卸载该 AppDomain。第一个线程将强制抛出 `ThreadAbortException` 并展开。新线程将等待该 AppDomain 卸载，然后新线程终止。如果 AppDomain 卸载失败，新线程将处理 `CannotUnloadAppDomainException`，但既然你没有编写这个新线程
