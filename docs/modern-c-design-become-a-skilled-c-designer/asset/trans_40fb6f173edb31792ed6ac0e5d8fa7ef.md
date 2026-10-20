

如 Listing 7-1 所示。

### Listing 7-1. 一个动态加载器工厂函数

```cpp
unique_ptr<DynamicLoader>
dynamicLoaderFactory() {
#ifdef POSIX
    return make_unique<PosixDynamicLoader>();
#elif WIN32
    return make_unique<WindowsDynamicLoader>();
#else
    return nullptr;
#endif
}
```

通过将 dynamicLoaderFactory() 函数编译到其自己的源文件中，我们可以通过将一组预处理器指令隔离到一个源文件中来实现平台无关的插件创建。然后在需要插件分配或释放的位置调用工厂函数，以返回正确类型的 DynamicLoader。通过让工厂返回一个 unique_ptr，我们无需担心内存泄漏。以下代码片段说明了 DynamicLoader 的平台无关用法：

```cpp
// Question: What platform?
auto loader = dynamicLoaderFactory();
// Answer: Who cares?
auto plugin = (loader ? loader->allocatePlugin(pluginName) : nullptr);
```

对于 pdCalc 的目的而言，我们可以用 DynamicLoader 层次结构和我们简单的工厂函数停止。我们只需要抽象一个平台相关特性（插件的分配和释放），而上面的代码已足以满足此目的。然而，我们已经走到这一步，值得再迈出一步，看看适用于需要多种不同平台相关特性的情况的平台无关性的通用实现，即使它不是我们案例研究所特别需要的。

## 7.3.3.6 用于通用平台无关代码的抽象工厂

作为软件开发人员，我们不断面临由平台依赖性引起的设计挑战。以下是 C++ 开发人员常见的平台特定编程任务的不完整列表：插件加载、进程间通信、文件系统导航（在 C++17 中标准化）、图形、线程（在 C++11 中标准化）、持久设置、二进制序列化、sizeof() 内置数据类型、计时器（在 C++11 中标准化）以及网络通信。列表上的大多数功能，如果不是全部，都可以通过 boost 或 Qt 等库中的平台无关 API 获得。对我个人而言，造成最多困扰的平台特定特性就是谦逊的目录分隔符（Posix 系统上的 / 和 Windows 系统上的 \）。

假设我们的计算器需要读取、写入和保存持久自定义设置的能力（请参阅第 8 章，了解为什么这对计算器可能是必要的）。通常，Linux 系统将设置保存在文本文件中（例如，在 Ubuntu 上，用户设置保存在主目录的 .config 目录中的文件中），而在 Windows 系统上，持久设置保存在系统注册表中。实际上，最佳解决方案是使用已经实现此抽象的现有库（例如，Qt 的 QSettings 类）。出于教学目的，我们假设没有外部库可用，并且我们将研究一种设计，该设计在我们现有的动态加载器旁边添加持久设置（或任意数量的平台相关功能）。我们的重点将放在抽象上，而不是每个平台上设置实现的细节。

简单的解决方案是搭载我们的动态加载器，并将必要的设置接口直接添加到 DynamicLoader 类中。当然，我们需要将类重命名为更通用的名称，例如 OsSpecificFunctionality，其派生类如 LinuxFunctionality 和 WindowsFunctionality。这种方法简单、快速且很快变得难以处理；它与内聚性背道而驰。对于任何规模的代码，这种技术最终会导致不可控制的臃肿，从而完全缺乏接口的可维护性。尽管项目上存在时间压力，我建议始终避免这种快速解决方案，因为它只是增加了你的技术债务，并会在未来造成比现在采用正确解决方案更长的延迟。

与其使我们现有的 DynamicLoader 类膨胀，我们反而从其设计中汲取灵感，并创建了一个单独的、类似的设置层次结构，如图 7-2 所示。同样，我们有在每个唯一平台上实例化平台特定派生类的问题。然而，与其添加一个额外的 settingsLoaderFactory() 函数来镜像现有的 dynamicLoaderFactory() 函数，我们反而寻求一个通用解决方案，该方案能够在保留平台选择单一代码点的同时实现无限的功能扩展。据预期，我们并不是第一个遇到此特定问题的程序员，并且已经存在解决方案：抽象工厂模式。

![](img/7aac03e344e518d9d0db5131f6619db9_406_0.png)

### Figure 7-2. The settings hierarchy for platform-independent persistent settings

根据 Gamma 等人[6] 的说法，抽象工厂“提供了一种创建相关或依赖对象的族的接口，而无需指定其具体类。”本质上，该模式可以分为两个步骤构建：

1. 为每个相关对象创建独立的层次结构（族），例如动态加载器层次结构和设置层次结构，通过其平台依赖性相关。
2. 创建一个层次结构，专门针对依赖关系（例如平台），为每个族提供工厂函数。

我发现上述抽象如果没有具体示例就很难理解；因此，让我们考虑我们在 pdCalc 中试图解决的问题。在浏览此示例时，请参考图 7-3 中的（过于复杂）类图。请记住，此抽象的总体目标是创建一个单一的源位置，能够提供创建任意数量的平台特定特化的平台无关机制。

![](img/7aac03e344e518d9d0db5131f6619db9_407_0.png)

![](img/7aac03e344e518d9d0db5131f6619db9_408_0.png)

### Figure 7-3. The abstract factory pattern applied to pdCalc

正如我们已经看到的，平台相关的功能可以抽象为并行、独立的层次结构。这些层次结构使平台相关的实现能够通过多态性通过平台无关的基类接口访问。对于 pdCalc，此模式转化为提供平台无关的 Settings 和 DynamicLoader 层次结构，分别抽象持久设置和动态加载。例如，我们可以通过抽象 DynamicLoader 接口多态地分配和释放插件，前提是系统根据平台实例化正确的底层派生类（PosixDynamicLoader 或 WindowsDynamicLoader）。抽象工厂的这一部分在图 7-3 中由 DynamicLoader 层次结构表示。

现在问题简化为根据当前平台实例化正确的派生类。与其提供单独的工厂函数来实例化 DynamicLoader 和 Settings 对象（一种分散的方法，需要在每个工厂中分别使用平台 #ifdefs），我们反而创建一个层次结构，该层次结构提供用于创建 DynamicLoader 和 Settings 对象的工厂函数的抽象接口。然后将此抽象工厂层次结构（图 7-3 中的 PlatformFactory 层次结构）专门化于平台，以便我们拥有工厂层次结构的平台特定派生类，这些派生类创建功能层次结构的平台特定派生类。此方案将平台依赖性集中到一个工厂函数中，该函数实例化正确的 PlatformFactory 特化。在 pdCalc 的实现中，我选择将 PlatformFactory 设为单例，并因此将 PlatformFactory 的工厂函数“隐藏”在 Instance() 函数中。

抽象工厂模式可能仍然没有太多意义，所以让我们看一些示例代码，以自上而下的方式查看抽象。最终，抽象工厂模式使我们能够在 pdCalc 中编写以下平台无关的高级代码：

```cpp
// PlatformFactory Instance returns either a PosixFactory or a
// WindowsFactory instance (based on the platform), which in turn
// creates the correct derived DynamicLoader
auto loader = PlatformFactory::Instance().createDynamicLoader();
```

```cpp
// The correctly instantiated loader provides platform specific
// dynamic loading functionality polymorphically through a platform
// independent interface
auto plugin = loader->allocatePlugin(pName);
```

