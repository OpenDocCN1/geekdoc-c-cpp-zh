
### 反序列化对象时重写程序集和/或类型

序列化对象时，格式化器输出类型的全名以及定义该类型的程序集的全名。反序列化对象时，格式化器使用这些信息来确切知道要构造和初始化什么类型的对象。前面关于 `ISerializationSurrogate` 接口的讨论展示了一种机制，允许你接管特定类型的序列化和反序列化职责。实现 `ISerializationSurrogate` 接口的类型与特定程序集中的特定类型绑定。

然而，有时 `ISerializationSurrogate` 机制不能提供足够的灵活性。以下是一些场景，在这些场景中，将对象反序列化为与其序列化时不同的类型可能很有用：

- 开发者可能决定将某个类型的实现从一个程序集移到另一个程序集。例如，程序集的版本号发生变化，使新程序集不同于原始程序集。
- 服务器上的对象被序列化到流中，并发送到客户端。当客户端处理该流时，它可以将对象反序列化为完全不同的类型，该类型的代码知道如何远程调用服务器对象上的方法。
- 开发者创建某个类型的新版本。我们希望将任何已经序列化的对象反序列化为该类型的新版本。

`System.Runtime.Serialization.SerializationBinder` 类使将对象反序列化为不同变得非常容易。为此，首先定义自己的类型，该类型派生自抽象 `SerializationBinder` 类型。在下面的代码中，假设程序集的 1.0.0.0 版本定义了一个名为 `Ver1` 的类，并假设程序集的新版本定义了 `Ver1ToVer2SerializationBinder` 类，还定义了一个名为 `Ver2` 的类。

```csharp
internal sealed class Ver1ToVer2SerializationBinder : SerializationBinder {
    public override Type BindToType(String assemblyName, String typeName) {
        // Deserialize any Ver1 object from version 1.0.0.0 into a Ver2 object

        // Calculate the assembly name that defined the Ver1 type
        AssemblyName asmVer1 = Assembly.GetExecutingAssembly().GetName();
        asmVer1.Version = new Version(1, 0, 0, 0);

        // If deserializing the Ver1 object from v1.0.0.0, turn it into a Ver2 object
        if (assemblyName == asmVer1.ToString() && typeName == "Ver1")
            return typeof(Ver2);

        // Else, just return the same type being requested
        return Type.GetType(String.Format("{0}, {1}", typeName, assemblyName));
    }
}
```

现在，在构造格式化器之后，构造 `Ver1ToVer2SerializationBinder` 的实例，并将格式化器的 `Binder` 读写属性设置为引用该绑定器对象。设置 `Binder` 属性后，现在可以调用格式化器的 `Deserialize` 方法。在反序列化期间，格式化器会看到已设置绑定器。当每个对象即将被反序列化时，格式化器会调用绑定器的 `BindToType` 方法，并将格式化器想要反序列化的程序集名称和类型传递给它。此时，`BindToType` 决定实际应构造什么类型，并返回该类型。

**注意** `SerializationBinder` 类还使得可以在序列化对象时通过重写其 `BindToName` 方法来更改程序集/类型信息，该方法如下所示：

```csharp
public virtual void BindToName(Type serializedType,
    out string assemblyName, out string typeName)
```

在序列化期间，格式化器调用此方法，并将它想要序列化的类型传递给你。然后，你可以（通过两个 out 参数）返回你希望改为序列化的程序集和类型。如果返回 null 和 null（默认实现就是这样），则不执行任何更改。

## 第 25 章 与 WinRT 组件互操作

**本章内容：**

- **CLR 投影与 WinRT 组件类型系统规则** 640
- **WinRT 类型系统核心概念** 641
- **框架投影** 644
- **从 .NET 代码调用异步 WinRT API** 645
- **WinRT 流与 .NET 流之间的互操作** 649
- **在 CLR 与 WinRT 之间传递数据块** 651
- **在 C# 中定义 WinRT 组件** 654

Windows 8 附带一个新的类库，允许应用程序访问操作系统功能。这个类库的正式名称是 *Windows 运行时 (WinRT)*，其组件可使用 WinRT 类型系统访问。WinRT 的许多目标与公共语言运行时 (CLR) 首次引入时的目标相同，例如简化应用程序开发，并允许用不同编程语言实现的代码轻松地相互操作。具体而言，Microsoft 支持从原生 C/C++、JavaScript（使用 Microsoft 的“Chakra”JavaScript 虚拟机时）以及 C# 使用 WinRT 组件。它们不再使用类型库来描述 COM 组件的 API，而是现在使用元数据。没错，WinRT 组件使用与 ECMA 委员会标准化的相同 .NET 元数据格式 (ECMA-335) 来描述其 API。这与我整本书中一直在讨论的元数据格式相同。

元数据比类型库丰富得多，而且 CLR 已经对元数据有完整的理解。此外，CLR 从一开始就支持通过运行时可调用包装器 (RCW) 和 COM 可调用包装器 (CCW) 与 COM 组件互操作。在大多数情况下，这允许运行在 CLR 之上的语言（如 C#）与 WinRT 类型和组件无缝互操作。

在 C# 中，当你拥有对 WinRT 对象的引用时，你实际上拥有对 RCW 的引用，而该 RCW 在内部引用该 WinRT 对象。类似地，如果将 CLR 对象传递给 WinRT API，你实际上传递的是对 CCW 的引用给 WinRT API，而该 CCW 持有对你的 CLR 对象的引用。

WinRT 组件的元数据嵌入在扩展名为 .winmd 的文件中。随 Windows 提供的 WinRT 组件，其元数据位于各种 Windows.*.winmd 文件中，这些文件可以在 %WinDir%\System32\WinMetadata 目录中找到。构建应用时，你会引用 Windows SDK 安装在此处的那个 Windows.winmd 文件：

```
%ProgramFiles(x86)%\Windows Kits\8.0\References\CommonConfiguration\Neutral\Windows.winmd
```

Windows 运行时类型系统的一个主要设计目标是使开发者能够使用他们已经熟悉且熟知的技术、工具、实践和约定成功编写应用。为了实现这一点，一些 WinRT 功能被投影到各自的开发技术中。对于 .NET Framework 开发者，有两种投影：

- **CLR 投影** CLR 投影是 CLR 隐式执行的映射，通常与重新解释元数据有关。下一节重点介绍 WinRT 组件类型系统规则，以及 CLR 如何将这些规则投影给 .NET Framework 开发者。
- **框架投影** 框架投影是通过利用 Framework 类库中引入的新 API，在你的代码中显式执行的映射。当 WinRT 类型系统与 CLR 的类型系统之间的阻抗失配过大，以致 CLR 无法隐式完成时，就需要框架投影。本章稍后将讨论框架投影。

### CLR 投影与 WinRT 组件类型系统规则

WinRT 组件遵循一种类型系统，类似于 CLR 强制执行类型系统的方式。当 CLR 看到 WinRT 类型时，它通常允许通过 CLR 的常规 COM 互操作技术使用该类型。但在某些情况下，CLR 会隐藏该 WinRT 类型（通过动态将其设置为私有），然后 CLR 通过不同的类型公开该类型。在内部，CLR 会查找某些类型（通过元数据），然后将这些类型映射到 Framework 类库中的类型。有关 CLR 隐式投影到 Framework 类库类型的 WinRT 类型的完整列表，请参见
