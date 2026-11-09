
- 指向接受 PermissionSet 的 CreateDomain 方法重载版本的 PermissionSet 对象引用。
- **一个 System.AppDomainSetup，用于标识 CLR 应为新 AppDomain 使用的配置设置。** 同样，我在此处传入 null，以便新 AppDomain 继承创建它的 AppDomain 的相同配置设置。如果希望该 AppDomain 具有特殊配置，请构造一个 AppDomainSetup 对象，将其各个属性设置为你期望的值（例如配置文件的名称），然后将得到的 AppDomainSetup 对象引用传给 CreateDomain 方法。

在内部，CreateDomain 方法会在进程中创建一个新的 AppDomain。这个 AppDomain 将被分配指定的友好名称、安全性和配置设置。新 AppDomain 将拥有自己的加载器堆，该堆将为空，因为当前没有程序集加载到新 AppDomain 中。创建 AppDomain 时，CLR 不会在这个 AppDomain 中创建任何线程；除非你显式让某个线程调用该 AppDomain 中的代码，否则不会有代码在该 AppDomain 中运行。

现在，要在新 AppDomain 中创建对象的实例，我们必须先将一个程序集加载到新 AppDomain 中，然后构造该程序集中定义的某个类型的实例。这正是调用 AppDomain 的公共实例方法 CreateInstanceAndUnwrap 所做的事情。调用 CreateInstanceAndUnwrap 时，我传入两个参数：一个 String 标识我要加载到新 AppDomain 中的程序集（由 ad2 变量引用），另一个 String 标识我要构造其实例的类型的名称。在内部，CreateInstanceAndUnwrap 会使调用线程从当前 AppDomain 转换到新 AppDomain。此时，线程（位于 CreateInstanceAndUnwrap 调用内部）将指定的程序集加载到新 AppDomain 中，然后扫描该程序集的类型定义元数据表，查找指定的类型（"MarshalByRefType"）。找到该类型后，线程调用 MarshalByRefType 的无参数构造函数。然后，线程转换回默认 AppDomain，以便 CreateInstanceAndUnwrap 可以返回对新 MarshalByRefType 对象的引用。

**注意** 存在 CreateInstanceAndUnwrap 的重载版本，允许你在调用类型的构造函数时传入参数。

虽然这听起来很好，但有一个问题：CLR 不能允许位于一个 AppDomain 中的变量（根）引用在另一个 AppDomain 中创建的对象。如果 CreateInstanceAndUnwrap 只是返回该对象的引用，隔离就会被破坏，而隔离正是 AppDomain 的全部目的！因此，就在 CreateInstanceAndUnwrap 返回对象引用之前，它会执行一些额外的逻辑。

你会注意到，MarshalByRefType 类型派生自一个非常特殊的基类：System.MarshalByRefObject。当 CreateInstanceAndUnwrap 发现它正在封送一个类型派生自 MarshalByRefObject 的对象时，CLR 将按引用跨 AppDomain 边界封送该对象。下面说明按引用将一个对象从一个 AppDomain（源 AppDomain，即对象实际创建所在的 AppDomain）封送到另一个 AppDomain（目标 AppDomain，即调用 CreateInstanceAndUnwrap 所在的 AppDomain）意味着什么。

当源 AppDomain 想要向目标 AppDomain 发送或返回某个对象的引用时，CLR 会在目标 AppDomain 的加载器堆中定义一个代理类型。这个代理类型使用原始类型的元数据定义，因此它看起来与原始类型完全相同；它具有所有相同的实例成员（属性、事件和方法）。实例字段不属于该类型的一部分，但稍后我会更详细地讨论这一点。这个新类型确实在其内部定义了一些实例字段，但这些字段与原始数据类型的字段并不相同。相反，这些字段指示哪个 AppDomain “拥有”真实对象，以及如何在拥有该对象的 AppDomain 中找到真实对象。（在内部，代理对象使用一个引用真实对象的 GCHandle 实例。GCHandle 类型将在第 21 章“自动内存管理（垃圾回收）”中讨论。）

一旦在目标 AppDomain 中定义了这个类型，CreateInstanceAndUnwrap 就会创建该代理类型的一个实例，初始化其字段以标识源 AppDomain 和真实对象，并将该代理对象的引用返回给目标 AppDomain。在我的 Ch22-1-AppDomains 应用程序中，mbrt 变量将被设置为引用这个代理。注意，从 CreateInstanceAndUnwrap 返回的对象实际上并不是 MarshalByRefType 类型的实例。CLR 通常不允许你将一个类型的对象强制转换为不兼容的类型。然而，在这种情况下，CLR 确实允许这种强制转换，因为这个新类型具有与原始类型所定义的相同的实例成员。事实上，如果你使用代理对象调用 GetType，它实际上会对你撒谎，说它是一个 MarshalByRefType 对象。

不过，可以证明从 CreateInstanceAndUnwrap 返回的对象实际上是对代理对象的引用。为此，我的 Ch22-1-AppDomains 应用程序调用 System.Runtime.Remoting.RemotingServices 的公共静态方法 IsTransparentProxy，并传入从 CreateInstanceAndUnwrap 返回的引用。从输出中可以看到，IsTransparentProxy 返回 true，表明该对象是一个代理。

现在，我的 Ch22-1-AppDomains 应用程序使用该代理调用 SomeMethod 方法。由于 mbrt 变量引用的是代理对象，因此会调用该代理对此方法的实现。代理的实现使用代理对象内部的信息字段，将调用线程从默认 AppDomain 转换到新 AppDomain。此线程现在执行的任何操作都在新 AppDomain 的安全性和配置设置下运行。然后，线程使用代理对象的 GCHandle 字段在新 AppDomain 中找到真实对象，再使用真实对象调用真正的 SomeMethod。

有两种方法可以证明调用线程已从默认 AppDomain 转换到新 AppDomain。首先，在 SomeMethod 方法内部，我调用 Thread.GetDomain().FriendlyName。由于线程现在运行在使用 AppDomain.CreateDomain 创建、并以 “AD #2” 作为友好名称参数的新 AppDomain 中，因此这将返回 “AD #2”（如输出所示）。其次，如果你在调试器中单步执行代码并显示“调用堆栈”窗口，[AppDomain Transition] 行会标记线程跨越 AppDomain 边界的位置。请参见图 22-2 底部的“调用堆栈”窗口。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_562_0.png)

**图 22-2** 调试器的“调用堆栈”窗口显示 AppDomain 转换。

当真正的 SomeMethod 方法返回时，它会返回到代理的 SomeMethod 方法，后者将线程转换回默认 AppDomain，然后线程继续在默认 AppDomain 中执行代码。

**注意** 当一个 AppDomain 中的线程调用另一个 AppDomain 中的方法时，该线程会在两个 AppDomain 之间转换。这意味着跨 AppDomain 边界的方法调用是同步执行的。然而，在任何给定时间，一个线程都被认为只处于一个 AppDomain 中，并使用该 AppDomain 的安全性和配置设置执行代码。如果你希望同时在多个 AppDomain 中执行代码，则应创建额外的线程，并让它们在所需的任何 AppDomain 中执行所需的任何代码。

我的 Ch22-1-AppDomains 应用程序接下来要做的是调用 AppDomain 的公共静态方法 Unload，以强制 CLR 卸载指定的 AppDomain，包括已加载到其中的所有程序集。系统会强制进行垃圾回收，以释放由正在卸载的 AppDomain 中的代码创建的任何对象。此时，默认 AppDomain 的 mbrt 变量仍然引用一个有效的代理对象；然而，该代理对象不再引用有效的 AppDomain（因为它已被卸载）。

当默认 AppDomain 尝试使用该代理对象调用 SomeMethod 方法时，会调用代理对此方法的实现。代理的实现确定包含真实对象的 AppDomain 已被卸载，于是代理的 SomeMethod 方法抛出 AppDomainUnloadedException，以告知调用方该操作无法完成。

哇！Microsoft 的 CLR 团队为确保 AppDomain 隔离做了大量工作，但这是重要的工作，因为这些特性被大量使用，并且正被越来越多的
