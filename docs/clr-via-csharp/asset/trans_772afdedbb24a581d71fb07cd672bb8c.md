
**MarshalByValType** 不派生自 **System.MarshalByRefObject**，因此 CLR 无法定义可用于创建实例的代理类型；该对象不能跨 AppDomain 边界按引用封送。

不过，由于 **MarshalByValType** 标记了 **[Serializable]** 自定义特性，因此允许 **MethodWithReturn** 按值封送该对象。下一段将说明将一个对象按值从一个 AppDomain（源 AppDomain）封送到另一个 AppDomain（目标 AppDomain）意味着什么。有关 CLR 的序列化和反序列化机制的更多信息，请参见第 24 章“运行时序列化”。

当源 AppDomain 想要向目标 AppDomain 发送或返回对对象的引用时，CLR 会将对象的实例字段序列化为字节数组。此字节数组从源 AppDomain 复制到目标 AppDomain。然后，CLR 在目标 AppDomain 中反序列化该字节数组。这会强制 CLR 将定义正在反序列化的类型的程序集加载到目标 AppDomain（如果尚未加载）。然后，CLR 创建该类型的实例，并使用字节数组中的值初始化对象字段，使其值与原始对象中的值完全相同。换句话说，CLR 在目标 AppDomain 中创建源对象的精确副本。随后，**MethodWithReturn** 返回对此副本的引用；该对象已跨 AppDomain 边界按值封送。

> **重要** 加载程序集时，CLR 使用目标 AppDomain 的策略和配置设置（例如，AppDomain 可以具有不同的 AppBase 目录或不同的版本绑定重定向）。这些策略差异可能会阻止 CLR 定位程序集。如果无法加载程序集，将引发异常，目标将不会收到对该对象的引用。

此时，源 AppDomain 中的对象和目标 AppDomain 中的对象具有各自独立的生存期，它们的状态可以彼此独立地更改。如果源 AppDomain 中没有根使原始对象保持存活（如我的 Ch22-1-AppDomains 应用程序中那样），其内存将在下一次垃圾回收时被回收。

为了证明从 **MethodWithReturn** 返回的对象不是对代理对象的引用，我的 Ch22-1-AppDomains 应用程序调用 **System.Runtime.Remoting.RemotingServices** 的公共静态 **IsTransparentProxy** 方法，并传入从 **MethodWithReturn** 返回的引用。从输出中可以看到，**IsTransparentProxy** 返回 **false**，表明该对象是真实对象，而不是代理。

现在，我的程序使用真实对象调用 **ToString** 方法。由于 **mbvt** 变量引用真实对象，因此会调用该方法的真实实现，并且不会发生 AppDomain 转换。可以通过检查调试器的“调用堆栈”窗口来证明这一点，该窗口不会显示 [AppDomain Transition] 行。

为了进一步证明不涉及代理，我的 Ch22-1-AppDomains 应用程序卸载新的 AppDomain，然后再次尝试调用 **ToString** 方法。与演示 #1 不同，这次调用成功，因为卸载新的 AppDomain 对默认 AppDomain “拥有”的对象没有影响，其中包括按值封送的对象。

### 演示 #3：使用不可封送类型的跨 AppDomain 通信

演示 #3 的开头与演示 #1 和 #2 非常相似。正如在演示 #1 和 #2 中一样，会创建一个 AppDomain。然后，调用 **CreateInstanceAndUnwrap** 将同一程序集加载到新的 AppDomain 中，在这个新的 AppDomain 中创建 **MarshalByValType** 对象，并让 **mbrt** 变量引用指向该对象的代理。

然后，使用此代理，我调用 **MethodArgAndReturn**，它接受一个参数。同样，CLR 必须维护 AppDomain 隔离，因此它不能简单地将对该参数的引用传入新的 AppDomain。如果对象的类型派生自 **MarshalByRefObject**，CLR 将为其创建代理并按引用封送它。如果对象的类型标记为 **[Serializable]**，CLR 将把该对象（及其子对象）序列化为字节数组，将字节数组封送到新的 AppDomain，然后将字节数组反序列化为对象图，并将对象图的根传入 **MethodArgAndReturn** 方法。

在这个特定演示中，我跨 AppDomain 边界传递一个 **System.String** 对象。**System.String** 类型不是派生自 **MarshalByRefObject**，因此 CLR 无法创建代理。幸运的是，**System.String** 被标记为 **[Serializable]**，因此 CLR 可以按值封送它，从而使代码能够正常工作。请注意，对于 **String** 对象，CLR 会执行一项特殊优化。跨 AppDomain 边界封送 **String** 对象时，CLR 只是将对该 **String** 对象的引用传递过边界；它不会复制 **String** 对象。CLR 可以提供此优化，因为 **String** 对象是不可变的；因此，一个 AppDomain 中的代码不可能破坏 **String** 对象的字符。有关 **String** 不可变性的更多信息，请参见第 14 章“字符、字符串与文本处理”。⁴

在 **MethodArgAndReturn** 内部，我显示传入其中的字符串，以表明该字符串跨过了 AppDomain 边界，然后创建 **NonMarshalableType** 类型的实例，并将对该对象的引用返回给默认 AppDomain。由于 **NonMarshalableType** 不是派生自 **System.MarshalByRefObject**，也没有标记 **[Serializable]** 自定义特性，因此不允许 **MethodArgAndReturn** 按引用或按值封送该对象——该对象无法被封送

4 顺便说一下，这就是 **System.String** 类被密封的原因。如果该类未被密封，那么你可以定义自己的派生自 **String** 的类并添加自己的字段。如果这样做，CLR 就无法确保你的“字符串”类是不可变的。

我的 Ch22-1-AppDomains 应用程序只使用一个线程来完成所有工作。每当我的代码调用 **AppDomain.Unload** 时，正在卸载的 AppDomain 中都没有线程，因此 CLR 不必引发任何 **ThreadAbortException** 异常。我将在本章后面进一步讨论 **ThreadAbortException**。

顺便说一下，当线程调用 **AppDomain.Unload** 时，CLR 会等待 10 秒，让正在卸载的 AppDomain 中的线程离开该 AppDomain。如果 10 秒后调用 **AppDomain.Unload** 的线程仍未返回，它将引发 **CannotUnloadAppDomainException**，并且该 AppDomain 将来可能会也可能不会被卸载。

> **注意** 如果调用 **AppDomain.Unload** 的线程位于正在卸载的 AppDomain 中，CLR 会创建另一个线程来尝试卸载该 AppDomain。第一个线程将强制引发 **ThreadAbortException** 并展开。新线程将等待该 AppDomain 卸载，然后新线程终止。如果 AppDomain 卸载失败，新线程将处理 **CannotUnloadAppDomainException**，但由于你并未编写这个新线程所执行的代码，因此你无法捕获此异常。

### AppDomain 监视

宿主应用程序可以监视 AppDomain 消耗的资源。一些宿主会使用此信息来决定当 AppDomain 的内存或 CPU 消耗超过宿主认为合理的水平时，何时强制卸载该 AppDomain。监视还可用于比较不同算法的资源消耗，以确定哪种算法使用的资源更少。由于 AppDomain 监视会产生额外开销，宿主必须通过将 **AppDomain** 的静态 **MonitoringEnabled** 属性设置为 **true** 来显式开启监视。这会为所有 AppDomain 开启监视。一旦监视开启，就无法关闭；尝试将 **MonitoringEnabled** 属性设置为 **false** 会导致引发 **ArgumentException**。

一旦开启监视，你的代码就可以查询 AppDomain 类提供的以下四个只读属性：

- **MonitoringSurvivedProcessMemorySize**：此静态 **Int64** 属性返回当前 CLR 实例控制的所有 AppDomain 当前正在使用的字节数。该数字在最近一次垃圾回收时是准确的。
- **MonitoringTotalAllocatedMemorySize**：此实例 **Int64** 属性返回特定 AppDomain 已分配的字节数。该数字在最近一次垃圾回收时是准确的。
- **MonitoringSurvivedMemorySize**：此实例 **Int64** 属性返回特定 AppDomain 当前正在使用的字节数。该数字在最近一次垃圾回收时是准确的。
