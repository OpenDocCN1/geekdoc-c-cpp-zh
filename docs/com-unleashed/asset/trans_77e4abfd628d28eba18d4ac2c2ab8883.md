
```cpp
{
    .
    .
    .

    // use object on MyServer
    pb->Release();
}
}
```

然而，如果客户端代码被改写为使用 `CoCreateInstance()` 或 `CoCreateInstanceEx()`，则无法正常工作。

```cpp
HRESULT hr;

COSERVERINFO csi = { 0, OLESTR("MyCLBS"), 0, 0 };
MULTI_QI mqi = { &IID_IUnknown, 0, 0 };

IBalanced *pb = 0;
hr = CoCreateInstanceEx(CLSID_Balanced, 0,
        CLSCTX_REMOTE_SERVER, &csi, 1, &mqi);
if (SUCCEEDED(hr))
{
    (pb = reinterpret_cast<IBalanced*>(mqi.pItf))->
        AddRef();
    mqi.pItf->Release();
    .
    .
    .

    // use object on MyServer

    pb->Release();
}
```

不幸的是，当前实现的 `CoCreateInstance()` 和 `CoCreateInstanceEx()` 不支持返回对某个对象的对象引用，而该对象位于调用 `CoCreateInstance()` 或 `CoCreateInstanceEx()` 所指向的服务器之外的另一台服务器上。换句话说，如果用户机器上的客户端以远程服务器名称 MyCLBS 调用 `CoCreateInstance()` 或 `CoCreateInstanceEx()`，而运行在 MyCLBS 上的类对象试图返回一个接口指针，指向它在 MyServer 上创建的对象，那么客户端的调用总是失败，并返回 `RPC_E_INVALID_OXID`，即“找不到指定的对象导出程序”。

OXID 是对象所在套间相对于机器的标识符。当一个接口指针在上下文之间进行封送传输时，它由一个名为 OBJREF 的低层数据类型表示，该类型与上下文无关，可以在线路上传递。大多数对象在接口指针于上下文之间传递时，依赖标准的 COM 封送机制来完成正确的操作。当它们的接口指针被封送时，生成的标准 OBJREF 会包含它们的 OXID。当一个 OBJREF 在目标上下文中被反封送时，接收机器会通过回调 OXID 所在的机器（该机器的地址也编码在标准 OBJREF 中）将 OXID 转换为一组 RPC 字符串绑定。这些字符串绑定可用于构建一个 RPC 绑定句柄，以对原始机器上 OXID 所属的进程进行远程调用。

`CoCreateInstance()` 和 `CoCreateInstanceEx()` 的服务器端（这是一个跨上下文调用）会进行检查，以确保它返回的 OBJREF 中的 OXID 在其执行所在的机器上是有效的。（这也是客户端最初调用时所针对的机器。）如果 OXID 不在该机器上，`CoCreateInstance()` 和 `CoCreateInstanceEx()` 就会报告 OXID 无效，因此返回 `RPC_E_INVALID_OXID`。尽管这种实现方式无疑有其充分的理由，但从 COM 的哲学来看，这感觉并不正确，因为所有的对象引用都应当是平等的。既然类对象在其自身机器上从另一个上下文返回一个对象引用是合法的（这正是 MTS、ATL 和 Visual Basic 中实现轮询、单线程和单元线程池的方式），那么它也应该能够从另一台机器上的上下文返回一个对象引用。但它做不到，而且这一事实在短期内不会改变。

当客户端使用 `CoGetClassObject()` 时，这不会成为问题，因为该方法返回的是客户端所调用机器上的对象。不幸的是，绝大多数 COM 客户端是通过 `CoCreateInstance()` 和 `CoCreateInstanceEx()` 编写的，或者是使用 Visual Basic 中新增的 Java 和脚本语言编写的。因此，`CoGetClassObject()` 可以工作这一事实在很大程度上无关紧要。

## 创建信封

`CoCreateInstance()` 需要知道所返回对象引用的 OXID。可以通过将对象引用放入另一个对象中，并转而返回对该对象的引用来隐藏这一信息。以下是 IEnvelope 的接口：

```idl
[
  uuid(5E7F74C0-E165-11D2-B72C-00A0CC212296), object
]
interface IEnvelope : IUnknown
{
  [propput] HRESULT Letter([in] IUnknown *punk);
};
```

我修改了特殊类对象的 `CreateInstance` 实现，将其想要返回的对象隐藏在一个本地创建的信封中。

如果信封使用标准封送，`CoCreateInstance()` 会成功，因为信封位于客户端所调用机器上的一个上下文中。然而，客户端最终会得到错误类型的对象引用，并且这些对象运行在错误的机器上——在本例中就是 CLBS。当然，客户端想要的是对运行在最终目标服务器 MyServer 上的底层对象的引用。这可以通过自定义封送来实现。

远程处理层在尝试封送接口指针时，首先会通过调用 `QueryInterface` 并请求 `IMarshal` 来检查对象是否实现了自定义封送。如果对象实现了这个接口，远程处理层就会将编写其上下文无关的 OBJREF 的任务委托给它。信封可以进行自定义封送，并将其负载中携带的、位于 MyServer 上的远程对象的标准 OBJREF 作为内容。

如果信封使用自定义封送，`CoCreateInstance()` 仍然会成功，因为它只检查标准封送 OBJREF 的 OXID。客户端最终仍然会得到错误类型的对象，不过现在它们运行在客户端的进程内部。这个问题可以通过一些巧妙的手法来解决。

当对象进行自定义封送时，远程处理层会要求它提供一个 CLSID，该 CLSID 标识一个能够解释其将写入自定义 OBJREF 中负载的类。当自定义 OBJREF 在目标上下文中被接收时，会实例化这个类的一个实例，并让其解释数据并返回一个对象引用。虽然通常情况下，解释自定义负载的对象会返回对自身的引用（这在实现按值封送时很典型），但这不是必需的要求。

执行反封送的对象可以返回对任意对象的引用，而这就是关键所在。如果信封进行自定义封送，那么当它在客户端进程中反封送时，它可以简单地通过反封送其隐藏在负载中的标准 OBJREF，然后返回对由此产生的、真实远程对象的代理的引用，从而将自身剥离掉。这就是为什么前面展示的 IEnvelope 接口使用只写属性的原因。不需要 propget 方法，因为信封会自己打开自己。

信封在 `GetUnmarshalClass` 中返回自己的 CLSID，以指示该类的另一个实例将解释其自定义负载。在 `GetMarshalSizeMax()` 和 `MarshalInterface()` 中，信封使用封送 API 将标准封送委托给信（letter），因此它将把标准 OBJREF 作为自定义封送数据写入。在 `UnmarshalInterface()` 中（当信封从 `CoCreateInstance()`（或 `CoCreateInstanceEx()`）返回时，会在客户端进程中调用此方法），信封会对其负载进行反封送，并返回对结果对象的引用。在这种情况下，代理引用的是真实远程对象，无论它运行在哪里。

要让信封技巧生效，需要在 CLBS 机器和每台客户端机器上注册信封类。这是一个额外的负担，但相对于让 `CoCreateInstance()` 和 `CoCreateInstanceEx()` 能够与转发类对象协同工作而言，这是非常便宜的代价。

实际上，还有一项额外的成本。自定义封送接口 `IMarshal` 包含 `ReleaseMarshalData()` 方法，如果远程处理架构在接收方的上下文中无法对自定义负载进行反封送，就会调用该方法。这个方法调用为自定义封送对象提供了一个清理任何现存服务器端资源的机会。例如，如果某个对象使用套接字进行自定义封送以传输数据，这个方法将给该对象一个关闭其在 `MarshalInterface()` 中建立的套接字的机会。

不幸的是，对于按值封送的对象（如信封），这个方法不会被调用，因为对象的服务器端副本已经被销毁了。对于大多数按值封送的对象来说，这没什么大不了的，因为它们不携带对象引用。但是信封确实携带了一个对象引用，如果它无法反封送，那么这个引用就会泄漏。幸运的是，COM+ 垃圾回收器会在六分钟内介入并清理这些泄漏的引用，所以这应该不是问题。

### 算法

在拥有一个代理服务器托管转发类对象并实现了信封机制之后，实现负载均衡所需的基本框架就完成了。所缺少的只是一个选择远程机器的算法。敏锐的观察者会注意到，我目前所有的代码总是将创建请求转发到 MyServer。有很多方法可以选择将工作发送到哪台服务器，包括（但不限于）随机、轮询、CPU 负载、方法调用时间以及网络访问成本。如此广泛的选择范围表明，负载均衡算法非常适合实现为可插拔组件。

对于我自己的可插拔算法，我定义了以下接口：

```idl
[
    uuid(741F3750-E3B1-11d2-8117-00E09801FDBE), object
]
interface ILoadBalancingAlg : IUnknown
{
    HRESULT CreateInstance([in] REFCLSID rclsid,
        [in] REFIID riid, [out, iid_is(riid)] void **ppv);
}
```

假设存在一个预先创建好的、实现了该接口的实例，那么转发类对象的 `CreateInstance` 方法可以被重写。

