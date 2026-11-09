
正如你所记得的，本章开头的 Stateful 对象示例在通过调用 `SetComplete()` 启用提前停用后，在调用之间丢失了状态。如你所见，`IObjectControl` 就是解决你那个运行不良的 Stateful 对象的方法。现在，你有一种方法可以支持提前停用和即时激活，同时不会丢失状态。`Activate()` 调用使你能够检索客户端交互所需的任何状态，而 `Deactivate()` 调用使你能够存储后续客户端调用所需的任何对象状态。你可能会说，类的构造函数和析构函数还不够。有两个具体原因。首先，某些操作（例如访问对象的上下文）只有在对象完全构造之后才能进行。这些方法通过在构造之后、销毁之前执行，规避了这个问题。第二个也是最重要的原因是，如果对象支持池化，那么它可以被重用，而不是被销毁并重新创建。

从 `CanBePooled()` 返回 true 会告知 COM+ 你的对象支持池化。这使 COM+ 能够维护一个对象池，从而可以快速分派对象来服务客户端请求，而无需承担对象构造和销毁的开销。MTS 2.0 及更早版本实际上并不池化对象，但它们仍然会调用 `IObjectControl`，就好像是为了将来兼容性而这样做。COM+ 实际上实现了对象池化。如果你关注最佳可伸缩性，就应该尝试测试支持提前停用、即时激活和池化的组件。只有精心的设计和测试，才能为给定组件找到最佳解决方案。

如果没有上下文信息带来的好处，`Activate()` 调用就不会有多大用处。突然被激活，并不能帮助你了解是谁在调用，以及为了执行所请求的任务可能需要恢复什么状态。因此，大多数组件设计将 `Activate()` 方法作为一个入口，用来从 COM+ 检索上下文信息（使用 `GetObjectContext()`），并从可能存储上下文特定状态信息的任何位置检索这些信息。

## 使用 ATL 构建 COM+ 组件

ATL 使构建支持 COM+ 的组件变得容易。从这里开始，所有 COM+ 示例都是使用 Visual C++ 6 及其相关 ATL 元素开发的。让我们构建一个基本的 ATL DLL，你可以用它来完成后续的几个示例。尽管构建一个支持 COM+ 的 ATL 组件并不复杂，但 ATL COM 应用程序向导会为你处理其中的少量细节。Visual C++ 6 可以创建 MTS 组件，而不能创建 COM+ 组件。因此，我们将采取的步骤会创建一个 MTS 组件。不过，它将在 COM+ 环境中运行。

首先，在一个 MTS 组件中重建 Stateful DLL 及其 Sum 类。随着本章的深入，你将修复先前实验中暴露的每个问题。要创建 MTS 组件项目，只需从 Visual C++ 主菜单中选择“文件”>“新建”，然后选择 ATL COM 应用程序向导。为项目指定名称和目录；然后在第一个向导对话框中，选中 MTS 支持复选框。MTS 组件始终是 DLL，这使 MTS 能够提供完整的运行时环境。如果沿用上一示例中使用的项目名和类名，就无需创建新的 COM+ 应用程序或修改客户端应用程序。

与为普通 ATL DLL 项目生成的文件相比，DSP 文件是唯一被修改的文件。MTS 组件链接到 MTS 支持库 mtx.lib 和 mtxguid.lib。还值得注意的是，VC 6 引入了一项新的性能特性，使你的生成项目能够将某些 DLL 标记为延迟（即时）加载。这可以将内存中应用程序映像的大小保持在最低限度，并加快程序的初始加载时间。ATL 通过使用 /delayload 链接器开关，以这种方式链接到 mtxex.dll（MTS 执行程序）。使用 /delayload 开关需要辅助函数来动态加载 DLL。你可以自行编写，也可以像 ATL 那样链接 delayimp.lib 中预提供的例程。

接下来，通过右键单击“类视图”窗格中的项目图标并选择“新建 ATL 对象”，向项目中添加新的 ATL 对象。选择 MS Transaction Server 组件类型，然后选择“下一步”。为类指定名称（例如 Sum），然后单击 ATL 对象向导属性对话框中的 MTS 选项卡，以配置 MTS 特定设置。

选中对 IObjectControl 的支持后，ATL 向导会为所有 IObjectControl 方法添加接口支持和起始代码。选中 Can Be Pooled 后，ATL 会生成一个返回 true 的 CanBePooled() 方法。

创建该类后，你会注意到 ATL 添加了一个智能指针特性，用于引用 MTS 的 IObjectContext 接口。ATL 会添加代码，在 Activate() 方法中初始化该指针，并在 Deactivate() 方法中释放它。生成的代码应类似于以下内容：

```cpp
HRESULT CSum::Activate()
{
    HRESULT hr = GetObjectContext(&m_spObjectContext);
    if (SUCCEEDED(hr))
        return S_OK;
    return hr;
}

BOOL CSum::CanBePooled()
{
    return TRUE;
}

void CSum::Deactivate()
{
    m_spObjectContext.Release();
}
```

添加上一示例中的 ISum::Add() 和 ISum::Accumulate() 方法。在新类中，你可以将原先大段的 SetComplete() 代码块替换为通过对象上下文智能指针进行的一次简单 SetComplete() 调用。Activate() 和 Deactivate() 方法确保所有其他方法都能自由访问你的 MTS 上下文对象。

```cpp
STDMETHODIMP CSum::Accumulate(int iValue, int *piTotal)
{
    if (NULL == piTotal)
        return E_INVALIDARG;

    m_iTotal += iValue;
    *piTotal = m_iTotal;

    // Tell MTS that our work is complete
    m_spObjectContext->SetComplete();

    // Return success
    return S_OK;
}
```

测试新的 COM+ 组件时，应当会表现出你之前体验过的相同功能和问题。

尽管目前调用之间仍然会丢失状态，但该对象现在已具备多种保存和检索 m_iTotal 状态的方法。Activate() 方法为对象提供了一种在需要状态之前恢复状态的方式，而 IObjectContext 提供的上下文信息使你能够识别是哪个客户端在调用。同样，Deactivate() 方法可用于在对象销毁之前保存对象状态。或者，就像你的情况一样，可以存储总额，并且仅在需要时检索，以提高性能。新的多用户 COM+ 对象还需要确保所有用户都能访问该总额。使用 MTS 共享属性管理器可以轻松解决此任务。

## 共享属性管理器

在多个对象和激活之间保存半持久对象状态的需求非常普遍。事实上，这种需求如此普遍，以至于 MTS 专门为此提供了一个称为共享属性管理器（SPM）的资源分配器。

每个 MTS 服务器进程中至多实例化一次共享属性管理器，从而让该进程内的所有对象都能访问其控制下的共享状态。SPM 提供并发管理，以确保共享状态元素不会因同一时间来自多个对象的写入和读取而遭到破坏。共享属性通过命名组进行管理，从而降低名称冲突的可能性。单体应用程序在需要共享状态时通常使用全局变量。SPM 解决了与全局变量相关的两个最大问题：访问控制和全局命名空间污染。有关 SPM 的更多信息，请参见第 15 章。

## SPM 的不足

在设计使用 SPM 的组件时，务必牢记几点。最值得注意的是，SPM 在每个服务器进程中只实例化一次。这意味着，存储在 SPM 中的任何属性都可供该服务器进程内的所有组件使用，而该进程之外的组件无法使用。因此，使用 SPM 在组件之间共享属性通常是个坏主意。如果管理员将某个组件重新部署到另一个服务器进程（应用程序）中，这些共享属性将无法再共享，并且每个服务器进程都会维护自己的一组属性数据。允许客户端连接到运行在不同计算机上的同一类对象的负载均衡场景，也会带来同样的问题。当需要应用程序范围的共享状态时，单独的数据库是最可行的解决方案。

## SPM 接口

使用 SPM 的组件需要包含 mtxspm.h 头文件。该头文件定义了三个接口，用于提供对共享属性管理器资源的访问：

- `ISharedPropertyGroupManager`
- `ISharedPropertyGroup`
- `ISharedProperty`

ISharedPropertyGroupManager 接口提供对 SPM 顶层行为的访问，包括创建、检索和枚举命名属性组。要清除 SPM 中任何现有组或属性，唯一的方法是关闭运行 SPM 的服务器进程。ISharedPropertyGroup 接口提供了一些方法，使你能够按名称或位置在引用的组中创建和检索属性。ISharedProperty 接口允许以变体形式设置和检索属性值。

## 向组件添加 SPM 功能

现在可以使用 SPM 更新现有的 COM+ 组件。此前，Stateful 组件在一个特性中维护对象状态。这种方法存在几个问题。首先，无法在你的分布式多用户应用程序中可能执行的各种对象之间共享此信息。这取决于设计，可能有利也可能有害；但在此示例中，假设你希望所有用户都能向累计总额中累加，即汇总当天所有销售人员的全部销售额。
