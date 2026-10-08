
大多数与单例模式相关的问题都源于其设计用于持有和控制对全局状态的访问。然而，如果你不需要控制状态何时初始化，或者不需要在单例对象本身中存储状态，可以使用其他技术，例如单状态模式（Monostate pattern）。

单状态模式允许创建类的多个实例，其中所有这些实例都使用相同的静态数据。例如，这里有一个单状态模式的简单案例：

```cpp
// monostate.h
class Monostate {
public:
    int GetAnswer() const { return sAnswer; }

private:
    static int sAnswer;
};
```

```cpp
// monostate.cpp
int Monostate::sAnswer = 42;
```

在这个示例中，你可以创建 `Monostate` 类的多个实例，但所有对 `GetAnswer()` 方法的都会返回相同的结果，因为所有实例共享同一个静态变量 `sAnswer`。你也可以通过仅在 `monostate.cpp` 中将其声明为文件作用域变量，而不是私有类变量，从而从头文件中隐藏静态变量的声明。由于静态成员不贡献于类每个实例的大小，这样做对 API 不会产生物理影响，除了从头文件中隐藏实现细节之外。单状态模式的某些优点是：

- 允许创建多个实例。
- 由于不需要 `GetInstance()` 方法，它提供了透明的用法。
- 通过使用静态变量展现了定义良好的创建和销毁机制。

正如 Robert C. Martin 所指出的，单例通过只允许创建一个实例来强制单性的**结构**，而单状态通过为所有实例共享相同的数据来强制单性的**行为**（Martin, 2002）。

提示：

如果你不需要全局数据的懒初始化，或者希望类的单一性是透明的，请考虑使用单状态代替单例。

作为一个进一步的现实示例，Second Life 源代码对 `LLWeb` 类使用了单状态模式。这个示例使用了所有成员函数都声明为静态的单状态版本。

```cpp
class LLWeb {
public:
    static void InitClass();

    /// 在用户首选的网络浏览器中加载指定的 url
    static void LoadURL(const std::string& url);

    // 在 Second Life 内部网络浏览器中加载指定的 url
    static void LoadURLInternal(const std::string& url);

    // 在操作系统的浏览器中加载指定的 url
    static void LoadURLEternal(const std::string& url);

    // 返回转义后的 url（将 "*" 转换为 "%20"）
    static std::string EscapeURL(const std::string& url);
};
```

在这种情况下，`LLWeb` 是一个管理类，为打开页面的功能提供了单一访问点。实际的网络浏览器本身在其他类中实现。`LLWeb` 类不持有任何状态，尽管当然，任何静态方法都可以访问静态变量。

这种静态方法版本的单状态的缺点是，你不能对任何静态方法进行子类化，因为静态成员函数不能是虚拟。此外，由于你不再实例化该类，因此你无法编写构造函数或析构函数来执行任何初始化或清理。这在 `LLWeb` 访问动态分配的状态而不是依赖编译器初始化的静态变量的情况下是必要的。`LLWeb` 的创建者通过引入一个 `initClass()` 静态方法绕过了这个限制，该方法要求客户端显式地初始化它。更好的设计可能是从每个公共静态方法中懒性地隐藏此调用。然而，在这种情况下，之前提到的线程安全考量将适用。

### 3.2.5 单例与单状态

作为一个进一步的现实示例，Second Life 源代码对 `LLWeb` 类使用了单状态模式。这个示例使用了所有成员函数都声明为静态的单状态版本。

## 3.3 工厂方法

工厂方法（Factory Method）是一种设计模式，允许你创建对象而无需指定要创建的 C++ 类型。本质上，工厂方法是构造函数的泛化。C++ 中的构造函数有几个局限性，如下：

- **没有返回值。**你不能从构造函数中返回结果。这意味着你不能通过返回一个 `NULL` 指针来在对象初始化期间信号错误（尽管你可以通过抛出异常来信号错误）。
- **命名限制。**构造函数很容易被识别，因为它被限制为与其所属类相同的名称。然而，这同时也限制了它的灵活性。例如，你不能拥有两个接受单个整数的构造函数。
- **静态绑定创建。**在构造对象时，你必须指定在编译时创建的类名，例如，你可能写 `Foo *f = new Foo()`，其中 `Foo` 是必须被编译器已知的特定类型。构造函数在运行时没有动态绑定的概念。
- **没有虚拟构造函数。**你不能在 C++ 中声明虚拟构造函数。正如所提到的，你必须在编译时指定要构造的对象的精确类型。编译器为该特定类型分配内存，然后调用基类的默认构造函数（除非你在初始化列表中指定了非默认构造函数）。这就是为什么你不能从构造函数中调用虚拟方法，然后调用尚未初始化的派生类。

在基础层面上，工厂方法仅仅是一个可以返回类实例的普通方法。然而，它们通常与继承结合使用，派生类可以重写工厂方法并返回该派生类的实例。使用抽象基类（ABC）实现工厂也是非常常见且有效的（DeLaura, 2001）。

在这里，在我进一步深入探讨使用工厂方法之前，让我们先回顾一下这些类。

ABC（抽象基类）是一个包含一个或多个纯虚成员函数的类。这种类不是具体的类，不能通过 `new` 操作符进行实例化。相反，它被用作基类，由派生类提供纯虚拟方法的实现。例如：

```cpp
// renderer.h
#include <string>

class IRenderer {
public:
    virtual ~IRenderer() {}
    virtual bool LoadScene(const std::string&filename, int w, int h) = 0;
    virtual void SetViewport(int w, int h) = 0;
    virtual void SetCameraPosition(double x, double y, double z) = 0;
    virtual void SetLookAt(double x, double y, double z) = 0;
    virtual void Render() = 0;
};
```

这个抽象基类可以描述一个极其简单的 3D 图形渲染器。方法上的 `=0` 意味着它们在派生类中必须被重写才能变成具体的。注意，严格来说说纯虚拟方法没有提供实现是不准确的。例如，你可以在 `renderer.cpp` 文件中为 `SetViewport` 提供默认实现，然后派生类就可以调用 `IRenderer::SetViewport()`，尽管它仍然必须显式地声明该方法。

当然，你可以在抽象基类中提供带有实现的方法：并不是所有方法都必须是虚的。在这方面，抽象基类可以模拟混入（mixins），即带有实现方法的接口。

对于任何带有一个或多个虚方法的类，你应该始终将抽象基类的析构函数声明为虚。以下代码说明了为什么这。

```cpp
class IRenderer {
    // 没有声明虚析构函数
    virtual void Render() = 0;
};
```

```cpp
class RayTracer : public IRenderer
{
    RayTracer();
    ~RayTracer();
    void Render(); // 为 ABC 方法提供实现
}
```

```cpp
int main(int, char **)
{
    IRenderer *r = new RayTracer();
    // delete 调用的是 IRenderer::~IRenderer，而不是 RayTracer::~RayTracer
    delete r;
}
```

### 3.3.2 简单工厂示例

现在我已经回顾了抽象基类，让我们用它来提供一个简单的工厂方法。我将继续之前的 `renderer.h` 示例，并开始为 `IRenderer` 的对象声明工厂。

```cpp
// rendererfactory.h
#include "renderer.h"
#include <string>
```

```cpp
class RendererFactory {
public:
    IRenderer *CreateRenderer(const std::string& type);
};
```

声明工厂方法就这样；它只是一个可以返回对象实例的普通方法。注意，此方法不能返回特定类型 `IRenderer` 的实例，因为它是抽象基类，不能实例化，它可以返回派生类。此外，你可以使用 `CreateRenderer()` 的参数来指定你想要创建的类型。

假设你已经实现了三个派生自 `IRenderer` 的具体类：`OpenGLRenderer`、`DirectXRenderer` 和 `MesaRenderer`。让我们进一步规定，你不希望使用你 API 的用户了解这些类型的存在：它们必须完全隐藏在 API 之后。根据条件，你可以这样提供工厂方法的实现：

```cpp
// rendererfactory.cpp
#include "rendererfactory.h"
#include "openglrenderer.h"
#include "directxrenderer.h"
```

```cpp
#include "mesarenderer.h"

IRenderer *RendererFactory::CreateRenderer(const std::string &type)
{
  if (type == "opengl")
    return new OpenGLRenderer();

  if (type == "directx")
    return new DirectXRenderer();

  if (type == "mesa")
    return new MesaRenderer();

  return NULL;
}
```

因此，该工厂方法可以根据客户端传递的字符串类型返回 `IRenderer` 的三个派生类中的任何一个。这允许用户在运行时决定创建哪个派生类，而不是像新的构造函数所要求的那样在编译时决定（注：此处原文可能指构造对象的方式）。这是一个巨大的优势，因为这意味着你可以根据用户输入或运行时读取的配置文件的内容创建不同的类。

此外，注意各种派生类的头文件仅包含在 `rendererfactory.cpp` 的公共头文件中。实际上，这些是私有头文件，不需要与你的 API 一起分发。因此，用户永远无法看到你不同渲染器的私有细节，他们甚至看不到用于实现这些不同渲染器的特定类型。用户仅通过字符串变量（或者如果你喜欢使用枚举）指定渲染器。

| TIP |

| :--- |

| 使用工厂方法提供强大的类构造方法并隐藏子类。 |

这个示例展示了一个完全可以的工厂方法。然而，一个潜在的缺点是它对派生类的硬编码。如果你向系统中添加一个新的渲染器，你需要编辑 `rendererfactory.cpp`。这并不麻烦，最重要的是它不会影响我们的公共 API。这意味着你不能在运行时添加对新派生类的支持。具体来说，这意味着用户不能向系统添加新的渲染器。这些问题将通过提供一个可扩展的工厂来解决。

### 3.3.3 可扩展工厂示例

为了将派生类与工厂方法解耦并允许在运行时添加新的派生类，你可以更新工厂以维护一个将名称与回调函数关联的 map。这允许工厂模式变得可扩展。为了简单起见，这里是工厂可能后的样子：

```cpp
// rendererfactory.h
#include "renderer.h"
#include <string>
#include <map>

class RendererFactory {
public:
    typedef IRenderer* (*Callback)();
    static IRenderer *CreateRenderer(const std::string& type);
    static void RegisterRenderer(const std::string& type, Callback cb);
    static void unregisterRenderer(const std::string& type);

private:
    static std::map<std::string, Callback> map;
};
```

为了完整性，`.cpp` 文件可能如下：

```cpp
// rendererfactory.cpp
#include "rendererfactory.h"
#include "openglrenderer.h"
#include "directxrenderer.h"
#include "mesarenderer.h"

std::map<std::string, RendererFactory::Callback> RendererFactory::map;

void RendererFactory::RegisterRenderer(const std::string& type, Callback cb) {
    map[type] = cb;
}

void RendererFactory::unregisterRenderer(const std::string& type) {
    map.erase(type);
}

IRenderer *RendererFactory::CreateRenderer(const std::string &type) {
    auto it = map.find(type);
    if (it != map.end()) {
        return it->second();
    }
    return NULL;
}
```

你的 API 用户现在可以向系统注册（取消注册）新的渲染器。编译器将确保用户的新渲染器符合你的 `IRenderer` 抽象接口，即它为所有纯方法都提供了实现。为了说明这一点，以下代码展示了用户如何如何定义自己的渲染器，将其注册到对象工厂，然后要求工厂创建它的实例。

```cpp
class UserRenderer : public IRenderer{
public:
    ~UserRenderer()
    bool LoadScene(const std::string &filename) { return true; };
    void SetViewport(int w, int h) {}
    void SetCameraPosition(double x, double y, double z) {}
    void SetLookAt(double x, double y, double z) {}
    void Render() { std::cout << "User Renderer" << std::endl; }
    static IRenderer* Create(int) { return new UserRenderer(); };
};

int main(int, char **argv) {
    // 注册一个新的渲染器
    RendererFactory::RegisterRenderer("user", UserRenderer::Create);

    // 创建我们新渲染器的实例
    IRenderer *r = RendererFactory::CreateRenderer("user");
    r->Render();
    return 0;
}
```

## 3.4 API 包装模式

最后，我指出，在本文提供的可扩展工厂中，渲染器回调在运行时必须对 `RegisterRenderer()` 函数可见。然而，这并不意味着你必须暴露你 API 的内置渲染器。你仍然可以通过在你的 API 初始化例程中注册它们，或者通过使用简单工厂与可扩展工厂的混合模式来隐藏它们。在这种混合模式下，工厂方法会首先将类型字符串与几个内置名称进行匹配。如果都没有匹配，它会检查由用户注册的名称。这种混合方法具有潜在的理想行为，即用户无法覆盖你的内置类。

## 3.4 API 包装模式（重申）

在另一组类之上编写一个包装接口是一项相对常见的 API 设计任务。例如，你正在处理一个庞大的遗留代码库，与其重构所有代码，你希望设计一个新的全新的 API，以隐藏底层的遗留代码（Feathers, 2004）。或者，你写了一个 C++ API，并需要为客户端暴露一个纯 C 接口。又或者，你写了一个第三方库，希望客户端能够访问它，但你不想直接向他们暴露该库。

创建包装 API 的缺点是可能会遇到性能影响，这是由于额外的间接层以及需要在包装层级存储任何额外状态的开销造成的。然而，为了暴露更高质量或更集中的 API，这种成本通常是值得的，正如前面提到的情况。

几种结构设计模式处理了在一个接口之上包装另一个接口的任务。我将在接下来的章节中描述这三种模式。它们按照包装层与原始接口之间的差异从小到大排列分别是：代理（Proxy）、适配器（Adapter）和外观（Façade）。

### 3.4.1 代理模式

代理设计模式（图 3.3）提供了一个指向另一个类的一对一转发接口：在代理类中调用 `FunctionA()` 将导致在原始类中调用 `FunctionA()`。也就是说，代理类和原始类具有相同的接口。这可以被视为一种单组件器（使用 Lakos (1996) 的术语），即代理 API 中的单个类映射到原始 API 中的单个类。

这种模式通常通过使代理类成为原始类的副本，或者更有可能是一个指向原始类的指针来实现。代理类的方法只是简单地重定向到原始对象中的同名方法。

| 客户端 | 原始对象 |

| --- | --- |
