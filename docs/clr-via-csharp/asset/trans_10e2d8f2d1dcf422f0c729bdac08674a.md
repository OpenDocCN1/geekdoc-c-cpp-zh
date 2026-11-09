

- **AppDomain 可以卸载** CLR 不支持从 AppDomain 中卸载单个程序集的能力。不过，你可以让 CLR 卸载某个 AppDomain，这也会导致该 AppDomain 中当前包含的所有程序集一并被卸载。
- **AppDomain 可以单独实施安全控制** 创建时，可以为 AppDomain 应用一个权限集，该权限集决定授予在该 AppDomain 中运行的程序集的最大权限。这允许宿主加载某些代码，并确保这些代码无法破坏或读取宿主自身使用的重要数据结构。
- **AppDomain 可以单独配置** 创建时，可以为 AppDomain 关联一组配置设置。这些设置主要影响 CLR 如何将程序集加载到 AppDomain 中。配置设置涉及搜索路径、版本绑定重定向、卷影复制和加载器优化。

> **重要** Windows 的一个出色特性是，它在自己的进程地址空间中运行每个应用程序。这确保一个应用程序中的代码无法访问另一个应用程序正在使用的代码或数据。进程隔离可防止安全漏洞、数据损坏和其他不可预测行为的发生，从而使 Windows 及其上运行的应用程序保持稳健。遗憾的是，在 Windows 中创建进程的代价非常高。Win32 **CreateProcess** 函数非常慢，而且 Windows 需要大量内存来虚拟化进程的地址空间。
>
> 不过，如果一个应用程序完全由可验证安全且不调用非托管代码的托管代码组成，那么在单个 Windows 进程中运行多个托管应用程序就不会有问题。而 AppDomain 提供了对这些应用程序进行安全控制、配置和终止所需的隔离。

图 22-1 展示了一个单独的 Windows 进程，其中运行着一个 CLR COM 服务器。此 CLR 当前管理两个 AppDomain（尽管单个 Windows 进程中可运行的 AppDomain 数量并没有硬编码限制）。每个 AppDomain 都有自己的加载器堆，每个加载器堆都维护着自该 AppDomain 创建以来已访问过哪些类型的记录。这些类型对象已在第 4 章“类型基础”中讨论过；加载器堆中的每个类型对象都有一个方法表，如果某个方法至少被执行过一次，则方法表中的每个条目都指向 JIT 编译的本机代码。

![](img/3c46ff5b170881db4209d365b1f7a808_613_0.png)

**图 22-1** 承载 CLR 和两个 AppDomain 的单个 Windows 进程

此外，每个 AppDomain 中都加载了一些程序集。AppDomain #1（默认 AppDomain）有三个程序集：MyApp.exe、TypeLib.dll 和 System.dll。AppDomain #2 中加载了两个程序集：Wintellect.dll 和 System.dll。

你会注意到，System.dll 程序集已加载到两个 AppDomain 中。如果两个 AppDomain 都使用 System.dll 中的同一个类型，那么两个 AppDomain 都会在每个加载器堆中为同一类型分配一个类型对象；类型对象的内存并不会由所有 AppDomain 共享。此外，当某个 AppDomain 中的代码调用某个类型定义的方法时，该方法的中间语言 (IL) 代码会被 JIT 编译，生成的本机代码会与每个 AppDomain 关联；该方法代码不会由调用它的所有 AppDomain 共享。

不共享类型对象或本机代码的内存是浪费的。不过，AppDomain 的全部目的就是提供隔离；CLR 需要能够卸载某个 AppDomain 并释放其所有资源，同时不会对其他任何 AppDomain 造成不利影响。复制 CLR 数据结构可确保这一点可以实现。它还可确保由多个 AppDomain 使用的类型为每个 AppDomain 都有一组静态字段。

有些程序集预期会被多个 AppDomain 使用。最好的例子是 MSCorLib.dll。此程序集包含 System.Object、System.Int32 以及对 .NET Framework 如此不可或缺的所有其他类型。此程序集在 CLR 初始化时会自动加载，并且所有 AppDomain 都共享此程序集中的类型。为减少资源使用量，MSCorLib.dll 以域中性方式加载；也就是说，CLR 为以域中性方式加载的程序集维护一个特殊的加载器堆。此加载器堆中的所有类型对象以及这些类型方法的所有本机代码都由该进程中的所有 AppDomain 共享。遗憾的是，共享这些资源带来的好处是有代价的：以域中性方式加载的程序集永远无法卸载。回收它们所用资源的唯一方法是终止 Windows 进程，让 Windows 回收这些资源。

### 跨 AppDomain 边界访问对象

一个 AppDomain 中的代码可以与另一个 AppDomain 中包含的类型和对象通信。不过，只有通过定义良好的机制才允许访问这些类型和对象。下面的 Ch22-1-AppDomains 示例应用程序演示了如何创建新的 AppDomain、将程序集加载到其中，并构造该程序集中定义的一个类型的实例。代码展示了在构造按引用封送的类型、按值封送的类型以及完全无法封送的类型时的不同行为。代码还展示了当创建这些对象的 AppDomain 被卸载时，这些以不同方式封送的对象的行为。Ch22-1-AppDomains 示例应用程序中的代码非常少，但我添加了很多注释。在代码清单之后，我会逐步讲解代码，解释 CLR 在做什么。

```csharp
private static void Marshalling() {
    // Get a reference to the AppDomain that calling thread is executing in
    AppDomain adCallingThreadDomain = Thread.GetDomain();

    // Every AppDomain is assigned a friendly string name (helpful for debugging)
    // Get this AppDomain's friendly string name and display it
    String callingDomainName = adCallingThreadDomain.FriendlyName;
    Console.WriteLine("Default AppDomain's friendly name={0}", callingDomainName);

    // Get & display the assembly in our AppDomain that contains the 'Main' method
    String exeAssembly = Assembly.GetEntryAssembly().FullName;
    Console.WriteLine("Main assembly={0}", exeAssembly);

    // Define a local variable that can refer to an AppDomain
    AppDomain ad2 = null;

    // *** DEMO 1: Cross-AppDomain Communication using Marshal-by-Reference ***
    Console.WriteLine("{0}Demo #1", Environment.NewLine);

    // Create new AppDomain (security & configuration match current AppDomain)
    ad2 = AppDomain.CreateDomain("AD #2", null, null);
    MarshalByRefType mbrt = null;

    // Load our assembly into the new AppDomain, construct an object, marshal
    // it back to our AD (we really get a reference to a proxy)
    mbrt = (MarshalByRefType)
        ad2.CreateInstanceAndUnwrap(exeAssembly, "MarshalByRefType");

    Console.WriteLine("Type={0}", mbrt.GetType());  // The CLR lies about the type

    // Prove that we got a reference to a proxy object
    Console.WriteLine("Is proxy={0}", RemotingServices.IsTransparentProxy(mbrt));

    // This looks like we're calling a method on MarshalByRefType but, we're not.
    // We're calling a method on the proxy type. The proxy transitions the thread
    // to the AppDomain owning the object and calls this method on the real object.
    mbrt.SomeMethod();

    // Unload the new AppDomain
    AppDomain.Unload(ad2);
    // mbrt refers to a valid proxy object; the proxy object refers to an invalid AppDomain

    try {
        // We're calling a method on the proxy type. The AD is invalid, exception is thrown
        mbrt.SomeMethod();
        Console.WriteLine("Successful call.");
    }
    catch (AppDomainUnloadedException) {
        Console.WriteLine("Failed call.");
    }



    // *** DEMO 2: Cross-AppDomain Communication using Marshal-by-Value ***
    Console.WriteLine("{0}Demo #2", Environment.NewLine);

    // Create new AppDomain (security & configuration match current AppDomain)
    ad2 = AppDomain.CreateDomain("AD #2", null, null);

    // Load our assembly into the new AppDomain, construct an object, marshal
    // it back to our AD (we really get a reference to a proxy)
    mbrt = (MarshalByRefType)
        ad2.CreateInstanceAndUnwrap(exeAssembly, "MarshalByRefType");

    // The object's method returns a COPY of the returned object;
    // the object is marshaled by value (not by reference).
    MarshalByValType mbvt = mbrt.MethodWithReturn();

    // Prove that we did NOT get a reference to a proxy object
    Console.WriteLine("Is proxy={0}", RemotingServices.IsTransparentProxy(mbvt));

    // This looks like we're calling a method on MarshalByValType and we are.
    Console.WriteLine("Returned object created " + mbvt.ToString());

    // Unload the new AppDomain
    AppDomain.Unload(ad2);
    // mbvt refers to a valid object; unloading the AppDomain has no impact.

    try {
```

