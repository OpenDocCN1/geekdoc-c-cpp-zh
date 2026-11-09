
当对某个包关闭安全性时，IsCallerInRole() 始终返回 TRUE。因此，在使用 IsCallerInRole() 之前，必须检查安全性是否可用。清单 15.2 展示了如何在方法级别测试安全性。

## 清单 15.2 在方法级别测试安全性

```cpp
HRESULT MyObj::SecuredMethod()
{
    IObjectContext *pContext=NULL;
    HRESULT hr = GetObjectContext(&pContext);
    if (SUCCEEDED(hr))
    {
        if (!pContext->IsInTransaction())
            return E_ACCESSDENIED;
        BSTR bstrAdmin = SysAllocString(L"Admins");
        BOOL bInRole=FALSE;
        if (!pContext->IsCallerInRole(bstrAdmin,&bInRole))
        {
            SysFreeString(bstrAdmin);
            return E_ACCESSDENIED;
        }
        pContext->Release();
        return S_OK;
    }
    // Add your security code here
    return S_OK;
}
```

## 直接调用方与原始调用方

当 MTS 外部的客户端与 MTS 内部的对象通信时，MTS 执行基于角色的安全性检查。当 MTS 内部的一个对象对另一个 MTS 对象进行方法调用时，MTS 不检查安全性。考虑一个示例：客户端有权访问 objectA 中的 method1，但无权访问 objectB 中的 method1。如果客户端调用 objectA 中的 method1，而 objectA 有权访问 objectB 中的 method1，并可能调用它。由于 MTS 不检查 MTS 对象调用其他 MTS 对象时的安全性，因此客户端不会被阻止执行这种调用序列。这可能会带来安全问题。

不过，MTS 确实提供了若干 API 来帮助你确定客户端的身份。MTS 区分原始调用方（访问调用链中第一个 COM 对象的客户端）和直接调用方（发起方法调用的调用方）。你可以使用 ISecurityProperty 接口中的方法获取原始调用方和直接调用方的安全标识符。此接口有五个方法：GetDirectCreatorSID、GetOriginalCreatorSID、GetDirectCallerSID、GetOriginalCallerSID 和 ReleaseSID。要获取此接口，请在上下文对象上调用 QueryInterface。

清单 15.3 演示如何使用 ISecurityProperty 接口。

## 清单 15.3 ISecurityProperty 接口

```cpp
IObjectContext* pContext = NULL;
ISecurityProperty* pISecProp = NULL;
PSID psid = NULL;
HRESULT hr = S_OK;
// Get the object context
hr = GetObjectContext(&pContext);
if (SUCCEEDED(hr))
{
    // Get a reference to the ISecurityProperty interface
    hr = pContext->QueryInterface( IID_ISecurityProperty,
        (void**)&pISecProp);
    // Obtain the creator's security ID
    hr = pISecProp->GetDirectCreatorSID(&psid);
    // Add your security code here
    // Release the security ID
    pISecProp->ReleaseSID(psid);
    // Release the interface
    pISecProp->Release();

    // Release the context
    pContext->Release();
}
```

## 负载均衡

本节讨论负载均衡，并建议一种以编程方式执行负载均衡的技术。第 20 章“负载均衡与池化”将通过一个示例应用程序深入介绍具体细节。负载均衡背后的基本目标是提高服务器性能。性能可以通过多种方式衡量，但就本讨论而言，它意味着两件事：更多用户和更快响应。

负载均衡有两种类型：动态和静态。动态负载均衡是指操作系统能够根据性能统计数据选择最适合运行客户端所请求组件的服务器。静态负载均衡是指程序根据固定数量决定应由哪台服务器处理请求（例如，如果有超过 50 个用户发出请求，则使用服务器 B）。

由于 MTS 和 Windows NT Server 4 无法执行动态负载均衡，因此执行负载均衡的最简单方法是让分布式应用程序更具可伸缩性：让多台服务器导出同一个包，然后让客户端决定要在哪台服务器上运行。更复杂且健壮的技术可能涉及创建一个负载均衡包。

![](img/112c2326f49d26b8d59aa054e14c5747_420_0.png)

使用这种技术时，每个客户端都与负载均衡包通信。负载均衡包的职责是根据某种算法或轮询方式创建中间层组件的实例。

Microsoft 提供了若干有助于负载均衡的产品，包括 Microsoft Cluster Server (MSCS)。MSCS 允许多台 Windows NT Enterprise Server 计算机作为一个单一单元运行。虽然对 MSCS 的完整讨论超出了本章范围，但你可以访问 Microsoft 网站 www.microsoft.com/Windows/server/Technical/management/ClusterArch.asp 查找有关此产品的更多信息。

## 创建基于 MTS 的应用程序

基于事务的应用程序的关键目标之一是尽可能快地执行事务。事务发生时，数据库系统会对数据加锁，以防止其他应用程序查看中间数据。

锁定会妨碍并发性，从而不利于可伸缩性。为了提高可伸缩性，必须设计对象，使其不会在实际事务中花费太多时间。本质上，最好通过粒度更细的方法调用来实现这一点。第 20 章详细讨论了粒度，第 16 章“COM+ 作为组件管理器”讨论了事务优化。

有两个方面决定事务的持续时间。一个涉及 MTS 中的拦截机制，具体来说是 JIT。另一个涉及 MTS 中的超时功能，该功能会在指定时间后自动中止事务。要理解这两个因素，必须首先理解事务在 MTS 中如何运作。

回顾一下，活动是具有相同并发要求的一组对象。在 MTS 2 中，当基础客户端创建 MTS 对象时，MTS 会创建一个新活动，并将该对象实例放入其中。这个对象反过来可以使用 IObjectContext 接口中的 CreateInstance() 函数邀请其他对象成为该活动的一部分（回顾一下，你从 GetObjectContext() API 获取 IObjectContext）。

另外，请记住，只有属于同一活动的对象才能对事务投票。事务具有单一入口点，并在标记为 Requires a Transaction 或 Requires a New Transaction 的对象被激活时开始。

你可能还记得，对象在客户端进行第一次方法调用时被激活。因此，对象首先在客户端请求创建该对象时被创建，但直到第一次方法调用时才被激活。对象所投的票存储在上下文包装器中。因此，投票在对象被激活时开始，在对象被停用时结束。

当事务根被销毁时，MTS 将提交或中止事务。更准确地说，如果一个对象需要成为该事务的一部分，它必须从第一个对象内部创建，并且必须被邀请到同一活动中。由于 MTS 2 是在 COM 发布之后构建的，因此活动中的对象无法使用标准 COM API 在同一活动中创建 MTS 组件。如果你使用 `CoGetClassObject()` 或 `CoCreateInstance()`，该对象将属于一个单独的活动。要创建属于同一活动的对象，请使用 `IObjectContext` 接口中的 `CreateInstance()` 方法。

以下示例展示了如何将对象 `CLSID_FriendObject` 邀请到同一活动中。

```cpp
IObjectContext *pContext;
HRESULT hr = GetObjectContext(&pContext);
if (SUCCEEDED(hr))
{
    IFriendObject *pFriendObject;
    pContext->CreateInstance(CLSID_FriendObject,
        __uuidof(pFriendObject),
        (void **)&pFriendObject);
}
```

当对象的上下文包装器消失后，投票就无法更改。上下文包装器会在通常称为“满意”标志的东西上跟踪投票状态。投“是”表示对象“满意”，投“否”表示对象“不满意”。如果上下文包装器在“不满意”状态下被销毁，事务将注定失败。投票可能有两种方式。一种方式是进行临时投票；另一种方式是进行最终投票。通过临时投票，对象表示它可以改变主意。（“我不满意，但也许如果你再进行一次方法调用，我可能会被说服而变得满意。”）通过永久式投票，对象表示：“我不满意（或满意），任何人都无法改变我的想法。”对象通过调用 `IObjectContext` 接口中的两个方法之一来控制满意状态：`EnableCommit()` 和 `DisableCommit()`。`EnableCommit()` 将“满意”标志的状态设置为满意，而 `DisableCommit()` 将状态设置为不满意。以下代码展示了如何调用这些方法：

```cpp
IObjectContext *pContext;
HRESULT hr = GetObjectContext(&pContext);
if (SUCCEEDED(hr))
{
    pContext->EnableCommit();
    pContext->Release();
}
```

`EnableCommit()` 和 `DisableCommit()` 进行的是临时投票——它们不影响上下文包装器的生命周期；它们只影响满意位的状态。如果对象被销毁，上下文包装器也随之销毁，此时最后一次投票将成为最终投票。
