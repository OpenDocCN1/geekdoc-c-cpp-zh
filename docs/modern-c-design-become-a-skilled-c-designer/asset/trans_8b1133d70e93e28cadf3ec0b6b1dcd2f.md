
// ...
loader->deallocatePlugin(plugin);

// 同样的原则适用于设置 ...
auto settings =
PlatformFactory::Instance().createSettings();
settings->readSettingsFromDisk();
// ...
settings->commitSettingsToDisk();

深入来看，我们首先要检查的是 PlatformFactory 的 Instance() 函数，它会根据平台返回 PosixFactory 或 WindowsFactory。

```
PlatformFactory&
PlatformFactory::Instance()
{
#ifdef POSIX

static PosixFactory instance;
#elif WIN32
static WindowsFactory instance;
#endif
return instance;
```

}
上面的函数做了一个微妙但聪明的处理，这是一个值得了解的技巧。
从客户端的角度来看，
PlatformFactory 看起来像一个普通的单例类。调用 Instance() 函数，会返回一个 PlatformFactory 引用。客户端随后像使用任何其他单例类一样使用该 PlatformFactory 的公共接口。然而，由于 Instance() 成员函数返回的是一个引用，我们可以多态地使用该实例。由于 PosixFactory 和 WindowsFactory 都派生自 PlatformFactory，因此实例化的 instance 变量是与平台匹配的特化版本，由实现中的 #ifdef 定义。我们巧妙地将实现细节，即抽象工厂模式的机制，从类的使用者那里隐藏起来。除非客户端注意到 PlatformFactory 中的工厂函数是纯虚的，否则他可能意识不到自己在使用一个面向对象的层次结构。当然，目标并不是为了在某种险恶的阴谋中隐藏任何东西来混淆

实现。相反，这种信息隐藏被用来减轻 PlatformFactory 客户端的复杂性负担。我们接下来检查 PosixFactory 和 WindowsFactory 类中 createDynamicLoader() 函数的简单实现（注意函数的协变返回类型）：

```
unique_ptr<DynamicLoader>
PosixFactory::createDynamicLoader()
{
return make_unique<PosixDynamicLoader>
();
}
```

```
unique_ptr<DynamicLoader>
WindowsFactory::createDynamicLoader()
{
return
make_unique<WindowsDynamicLoader>();
}
```

上面，我们只是用一个类层次结构替换了动态

加载器工厂函数（参见列表 7-1），用多态性替换了平台 #ifdefs。仅有一小部分功能依赖于平台，用抽象工厂替换工厂函数显然是过度设计。然而，对于我们的示例，我们有独立的 DynamicLoader 和 Settings 族都依赖于相同的平台条件（原则上，我们可以有任意数量的此类层次结构），而抽象工厂模式允许我们将平台依赖集中在一个位置（在这里，是 PlatformFactory 的 Instance() 函数中），而不是将其分散到多个独立的工厂函数中。从维护的角度来看，其价值主张与更倾向于使用多态而不是 switch 语句类似。

难题的最后几部分是 DynamicLoader 和 Settings 层次结构的实现。幸运的是，这些实现与第 7.3.3 节概述的思路完全相同，我不必在此重复它们。确实使用抽象工厂模式并不会给平台相关函数的实现增加任何固有的复杂性。该模式只是在通过单一工厂层次结构而不是一系列工厂函数实例化这些类时增加了一些机制。

在 pdCalc 仓库的源代码中，不存在 Settings 层次结构（或其在 PlatformFactory 中的相关 readSettingsFromDisk() 和 commitSettingsToDisk() 函数）的实现，因为按编写方式，pdCalc 并不需要持久化设置抽象。Settings 层次结构只是作为一个合理的示例人为制造出来，以具体展示抽象工厂模式的机制和相关性。话虽如此，我确实选择在 pdCalc 的代码中仅为 DynamicLoader 包含一个完整的抽象平台工厂实现，以说明抽象工厂模式的实际实现，即使更简单的单个工厂函数本可以胜任，并且更适合生产代码。

## 7.4 问题 3：改造 pdCalc

我们现在转向最后一个插件问题，即改造已开发的类和接口以适应动态添加计算器功能。这个问题不是关于插件管理。相反，我们在这里解决的问题是扩展 pdCalc 的模块接口以接受插件功能。本质上，在第 7.2 节定义了如何在插件中发现命令和按钮的情况下，本节描述了如何将这些新发现的命令整合到 pdCalc 中。

让我们首先创建一个接口以实现新发现的插件命令的注入。回忆一下第 4 章中核心命令在应用程序启动时如何加载到 CommandRepository 中。首先，主应用程序调用 RegisterCoreCommands() 函数。其次，在此函数内部，CommandRepository 类的 registerCommand() 函数

对每个核心命令调用一次，将命令的名称和命令原型注册到 CommandRepository。在第 7.2 节中，我们开发了一个接口用于从插件导出命令名称和命令原型。显然，要注册这些插件命令，我们只需要扩展命令分发器模块的接口以包含 registerCommand() 函数。然而，这种接口扩展提出了一个有趣的问题。在 C++ 中，没有正式的模块定义，将模块接口扩展意味着什么？

## 模块接口

到目前为止，我们还没有严格定义实现或描述模块的机制。我们只是松散地声明某些类属于某些模块（例如，CommandRepository 属于命令分发器模块）。但这到底意味着什么？目前的 C++ 语言并没有实现模块概念。因此，模块本质上是一个元语言概念，而

语言本身在强制执行模块接口方面几乎没有帮助。我们确实有几种基本选择来定义模块及其接口。首先，将所有不直接属于接口的类封装在一个源文件中，并且只在一个头文件中公开有限的模块接口。其次，将每个模块构建为单独的 DLL 并使用 DLL 符号导出机制选择性地导出接口函数。第三，通过文档和注释中的声明隐式定义模块边界。让我们探讨每一种选项。

## 源代码隐藏

让我们首先讨论 C 程序员一直可用的封装模型：将非公共接口类和函数隐藏在源文件中，并且不在头文件中公开其接口。这是 C++ 提供的唯一真正隐藏符号的机制（记住，访问修饰符，如 private，不能用于类本身，就像在

选项中那样）。采用此选项当然超出了 C++ 语言本身的范围。DLL 隐藏基于操作系统的库格式并通过编译器指令实现。本质上，程序员用特殊的编译器指令装饰类或函数以指示函数是否要从 DLL 导出或导入。编译器随后创建仅公开导出适当标记符号的 DLL，而链接到 DLL 的代码必须指定其打算导入哪些符号。由于同一个头文件在编译 DLL 时必须标记为导出，而在编译使用 DLL 的代码时必须标记为导入，因此实现通常是通过使用编译器/OS 特定的预处理器指令来完成的。例如，在 Windows 中，将采用以下代码（或类似变体）：

// Declspec .h
#ifdef BUILDING_DLL

#define DECL... #else
