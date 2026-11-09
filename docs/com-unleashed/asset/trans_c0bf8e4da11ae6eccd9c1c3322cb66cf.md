
## 第4章
## 持久化存储

### 本章内容

- IPersist 接口 74
- IStream 接口 78
- 创建实现 IPersistStreamInit 的 ATL 对象 83
- 使用具有持久化能力的对象 88
- 简化持久化对象的创建 90
- 简化持久化对象的使用 93

开发人员面临的挑战之一是维护 COM 对象的状态。在运行时，当 COM 对象加载时，可能希望它记住并恢复到先前的状态。在这种情况下，对象将加载持久化存储数据，以便能够在先前状态下恢复运行。当 COM 对象被销毁时，它也可能发现有必要保存其状态，以便当前应用程序或另一个应用程序能够呈现出与销毁时相同的状态。在这种情况下，对象将保存持久化数据。

持久化存储的一个很好的用例是 Visual Basic 对 ActiveX 控件的处理。在 ActiveX 控件属性表中，你可以看到 Visual Basic 在会话之间保持相同的属性值。换句话说，如果你在运行 Visual Basic 时将控件的属性设置为某些期望值，那么当你重新运行 Visual Basic 时，该控件会保留上次会话的属性设置。

本章将向你展示如何向对象加载持久化数据以及从对象保存持久化数据。我们的讨论将聚焦于 IPersistStreamInit 和 IStream 接口。然而，本章展示的技术并不是可用于持久化数据存储的唯一技术。

两个示例控件和两个使用这些控件的示例程序将说明这些技术。第一个控件保持简单，以便你能够轻松看到并理解相关内容。加载第一个示例控件的客户端应用程序也很简单。它向你展示如何在不依赖 ClassWizard 生成的类的情况下使用持久化存储技术。

第二个示例程序比第一个做得更多，因为它会响应用户的鼠标点击。不过，我借助 ClassWizard 来简化工作。因此，创建第二个示例程序所花的时间并不比第一个示例程序多。

### IPersist 接口

有几种标准持久化接口允许客户端应用程序获取并保存对象的状态。对象通过实现这些接口中的一个或多个来声明其序列化状态的能力。持久化接口还使客户端能够通过将对象的序列化数据加载回对象来克隆该对象。我已经提到过 Visual Basic 对属性持久化的使用。Microsoft 消息队列 (MSMQ) 使用持久化接口来保存对象的状态，以便在消息中传输。表4.1展示了六个标准持久化接口。

**表4.1 — 标准持久化接口**

| 接口 | 描述 |
|---|---|
| `IStorage` | IStorage 接口支持结构化存储对象的创建和管理。 |
| `IStream` | IStream 接口支持向流对象读取和写入数据。 |
| `IPersist` | IPersist 接口定义单一方法 GetClassID，该方法旨在提供可在系统中持久存储的对象的 CLSID。 |
| `IPersistStorage` | IPersistStorage 接口定义的方法使容器应用程序能够将存储对象传递给其包含的对象之一，并加载和保存该存储对象。 |
| `IPersistStream` | IPersistStream 接口提供用于保存和加载对象的方法，这些对象使用简单的串行流来满足其存储需求。 |
| `IPersistFile` | IPersistFile 接口提供的方法允许对象从磁盘文件加载或保存到磁盘文件，而不是从存储对象或流加载或保存。 |

所有持久化接口都派生自 IPersist 接口。该接口仅允许客户端获取对象的类标识符 (CLSID)。通常，客户端应用程序会将对象的类标识符与对象的状态一起存储。这样，客户端应用程序在重新实例化该类时就知道要激活哪个对象。对于无状态对象，IPersist 接口就足够了，因为客户端应用程序只需要知道要激活哪个类。然而，大多数对象除了其 CLSID 之外还需要存储数据。这些对象可以从派生自基础 IPersist 接口的多种持久化接口中进行选择。

### IPersistStorage

IPersistStorage 接口提供的方法允许容器应用程序将存储对象传递给其包含的对象之一，并加载和保存该存储对象。IPersistStorage 接口通常用于复合对象。该接口的一个常见应用是剪贴板或拖放操作。容器使用该接口初始化对象，并将其置于已加载或运行状态。接口声明如下。

```
interface IPersistStorage : IPersist
{
    HRESULT IsDirty
    (
        void
    );

    HRESULT InitNew
    (
        [in, unique] IStorage *pStg
    );

    HRESULT Load
    (
        [in, unique] IStorage *pStg
    );

    HRESULT Save
    (
        [in, unique] IStorage *pStgSave,
        [in] BOOL fSameAsLoad
    );

    HRESULT SaveCompleted
    (
        [in, unique] IStorage *pStgNew
    );

    HRESULT HandsOffStorage
    (
        void
    );
};
```

### IPersistFile

IPersistFile 接口提供的方法允许对象从磁盘文件加载或保存到磁盘文件。本章中的示例使用流对象进行加载和保存。IPersistFile 接口与我们示例中所做工作的对比如下：当你想要从单独的文件读取信息或向单独的文件写入信息时，你会实现 IPersistFile 接口。接口声明如下：

```
interface IPersistFile : IPersist
{
    HRESULT IsDirty
    (
        void
    );

    HRESULT Load
    (
        [in] LPCOLESTR pszFileName,
        [in] DWORD dwMode
    );

    HRESULT Save
    (
        [in, unique] LPCOLESTR pszFileName,
        [in] BOOL fRemember
    );

    HRESULT SaveCompleted
    (
        [in, unique] LPCOLESTR pszFileName
    );

    HRESULT GetCurFile
    (
        [out] LPOLESTR *ppszFileName
    );
};
```

### IPersistStreamInit

IPersistStreamInit 接口实际上被设计为 IPersistStream 接口的替代品。它添加了一个名为 InitNew() 的单一方法。IsDirty()、Load()、Save() 和 GetSizeMax() 派生自 IPersistStream。所有 IPersistStreamInit 方法都可以在表4.2中看到。接口声明如下：

```
interface IPersistStreamInit : IPersist
{
    HRESULT IsDirty
    (
        void
    );

    HRESULT Load
    (
        [in, unique] IStream *pStm
    );

    HRESULT Save
    (
        [in, unique] IStream *pStm,
        [in] BOOL fClearDirty
    );

    HRESULT GetSizeMax
    (
        [out] ULARGE_INTEGER *pcbSize
    );

    HRESULT InitNew
    (
        void
    );
};
```

**表4.2 — IPersistStreamInit 接口**

| 方法 | 描述 |
|---|---|
| `QueryInterface` | 继承自 IUnknown |
| `AddRef` | 继承自 IUnknown |
| `Release` | 继承自 IUnknown |
| `GetClassID` | 继承自 IPersist |
| `IsDirty` | 检查对象自上次保存以来是否发生更改 |
| `Load` | 从对象先前保存到的流中初始化对象 |
| `Save` | 将对象保存到指定流中，并指示对象是否应重置其脏标志 |
| `GetSizeMax` | 返回保存对象所需的流大小（以字节为单位） |
| `InitNew` | 将对象初始化为默认状态 |

### `IStream` 接口

IStream 接口支持向流对象读取和写入数据。流对象包含结构化存储对象中的数据。简单数据可以直接写入流，但最常见的情况是，流是嵌套在存储对象中的元素。它们类似于标准文件。

IStream 接口定义了类似于 MS-DOS 文件函数的方法。例如，每个流对象都有自己的访问权限和一个查找指针。流对象与 DOS 文件之间的主要区别在于，流不是使用文件句柄打开的，而是通过 IStream 接口指针打开的。

此接口中的方法将对象的数据呈现为可读写的连续字节序列。还有一些方法用于提交和还原以事务模式打开的流上的更改，以及用于限制对流中某个字节范围的访问的方法。

流可以长时间保持打开状态而不消耗文件系统资源。IStream::Release 方法类似于文件上的关闭函数。一旦释放，流对象就不再有效，并且不能再使用。

表4.2列出了 IStream 方法，并对每个方法作了简要说明。
