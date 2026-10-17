
然而，STL 提供了几个专门为继承设计的类。其中最明显的是 `std::exception`。它是所有 STL 异常的基类，包括 `bad_alloc`、`bad_cast`、`bad_exception`、`bad_type`、`lock_error`、`logic_error` 和 `runtime_error`。你可以非常简单地定义派自 `std::exception` 的自定义异常：

```cpp
class DivByZeroException : public std::exception {
public:
    const char *what() const {
        return "Division by zero attempted";
    }
};
```

STL 中另一个支持通过继承扩展的部分是 `ostream` 库。这是一个非常强大、设计良好且可扩展的 API，它提供了流抽象。流可以被视为一序列等待处理的字节流，例如 `cin` 输入流和 `cout` 输出流。你可以通过派生特定的流类或 `istream` 基类来编写自定义流类。例如，你可以创建自定义流类来向 Web 服务器发送和从中接收 HTTP 数据。

此外还有 `iambuf` 库，它使得处理 STL 流和流缓冲区（stream buffers）变得更加容易。该库附带了一系列实用的过滤器，包括正则表达式过滤和数据压缩方案（如 `gzip`、`zip` 和 `bzip2`）。

### 12.2.4 继承与枚举

有时，用户可能想要扩展你在某个基类中定义的枚举，以便为他们在派生类中添加的新功能增加更多的枚举器值。这在 C++ 中可以如下所示轻松实现：

```cpp
class Base {
public:
    enum SHAPE {
        CIRCLE,
        SQUARE,
        TRIANGLE,
        SHAPE_END = TRIANGLE
    };
};
```

```cpp
class Derived : public Base {
public:
    enum SHAPE {
        OVAL = SHAPE_END + 1,
        RECTANGLE,
        HEXAGON
    };
};
```

这里是一个展示如何使用这种扩展枚举的示例：

```cpp
std::cout << "CIRCLE" << Derived::CIRCLE << std::endl;
std::cout << "SQUARE" << Derived::SQUARE << std::endl;
std::cout << "TRIANGLE" << Derived::TRIANGLE << std::endl;
std::cout << "OVAL" << Derived::OVAL << std::endl;
std::cout << "RECTANGLE" << Derived::RECTANGLE << std::endl;
std::cout << "HEXAGON" << Derived::HEXAGON << std::endl;
```

这种工作能够健壮运行的关键在于，`Base` 类定义了 `SHAPE_END`，使得 `Derived` 类可以从 `Base::SHAPE` 定义的最后一个值之后添加新值。因此，当你预计一个会被子类化的类中定义枚举时，这是一种良好的做法。如果不这样做，你的客户端可能会选择一个任意大的整数开始为它们的枚举器编号，例如 `OVAL=100`，虽然这种方案并不优雅。

| 提示 |
| :--- |
| 对于基类中的枚举，请为枚举值添加一个枚举器，例如 `<enum-name>_END`。 |

### 12.2.5 访问者模式（Visitor Pattern）

在第 3 章中介绍过各种泛型设计模式。然而，我将访问者模式的讨论推迟到了现在，因为它专门针对 API 的可扩展性。访问者模式的核心目标是允许客户端遍历数据结构中的所有对象，并对其中的每个对象执行泛型操作。这种模式本质上是模拟向现有类添加新虚函数的方法。它为客户端扩展你的 API 功能提供了一个实用的模式。例如，访问者模式可以用于让提供一组方法，对场景图层次结构中的每个节点进行操作，或者遍历编程语言解析器的派生树并输出人类可读的程序树。

让我们开发一个访问者示例来说说明这种模式的工作原理。我将使用一个描述 3D 场景的场景图层次结构示例，例如 Open Inventor、OpenSceneGraph 或虚拟现实建模语言（VRML）所使用的。为了保持示例简单，我们的场景图将包含三种不同的节点类型：`Shape`、`Transform` 和 `Light`。图 12.4 显示了使用这些节点类型的示例层次结构。

首先定义抽象访问者接口。客户端可以创建此接口的具体子类，以便为场景图添加自定义操作。它本质上为场景图中的每种节点类型声明了一个 `Visit()` 方法。

![](img/170b148e5ba8f4b05aa8234f929ebba6_374_0.png)

图 12.4 显示节点类型的示例场景层次结构。

```cpp
// nodevisitor.h
#include <string>
class ShapeNode;
class TransformNode;
class LightNode;
class INodeVisitor
{
public:
    virtual ~INodeVisitor() {}
    virtual void Visit(ShapeNode& node) = 0;
    virtual void Visit(TransformNode& node) = 0;
    virtual void Visit(LightNode& node) = 0;
};
```

```cpp
// scenraph.h
class BaseNode {
public:
    explicit BaseNode(const std::string& name) : mName(name) {}
    virtual ~BaseNode() {}
    virtual void Accept(INodeVisitor& visitor) = 0;
protected:
    std::string mName;
};
class ShapeNode : public BaseNode {
public:
    explicit ShapeNode(const std::string& name) : BaseNode(name) {}
    void Accept(INodeVisitor& visitor) override;
    int GetPolygonCount() const;
};
class TransformNode : public BaseNode {
public:
    explicit TransformNode(const std::string& name) : BaseNode(name) {}
    void Accept(INodeVisitor& visitor) override;
};
class LightNode : public BaseNode {
public:
    explicit LightNode(const std::string& name) : BaseNode(name) {}
    void Accept(INodeVisitor& visitor) override;
};
class SceneGraph {
public:
    SceneGraph();
    void Traverse(INodeVisitor& visitor);
private:
    class Impl;
    Impl *impl;
};
```

![](img/170b148e5ba8f4b05aa8234f929ebba6_376_0.png)

图 12.5 访问者模式的 UML 图。

```cpp
// scenraph.cpp
void ShapeNode::Accept(INodeVisitor& visitor)
{
    visitor.Visit(*this);
}
void TransformNode::Accept(INodeVisitor& visitor)
{
    visitor.Visit(*this);
}
void LightNode::Accept(INodeVisitor& visitor)
{
    visitor.Visit(*this);
}
```

## 12.2 通过继承进行扩展

`MyVisitor` visitor:
```cpp
enegraph.Traverse : << << visitor.mNumShapes << std::endl;
std::cout << "Shapes: " << visitor.mNumShapes << std::endl;
std::cout << "Polygons: " << visitor.mNumPolygons << std::endl;
std::cout << "Transforms: " << visitor.mNumTransforms << std::endl;
std::cout << "Lights: " << visitor.mNumLights << std::endl;
```

此示例展示了访问者模式（Visitor pattern）的许多优点，为客户端提供了扩展的灵活性，客户端可以轻松地将自己的方法插入到类层次结构中。其他优点还包括将执行单一协调操作的代码聚合在一起。例如，所有实现节点计数功能的代码都包含在单个 `MyVisitor` 类中，而控制各种节点和多形数量的状态（`mNumShapes`, `mNumPolygons`, `mNumTransforms`, `mNumLights`）被隔离在 `MyVisitor` 类中，而不是直接存储在 `SceneGraph` 对象中，从而增加了该对象的大小。

然而，访问者模式也有一些明显的缺点。能够向一组类添加新方法的灵活性，代价是让添加新类变得困难得多。请注意，在 `visitor.h` 中，访问者必须了解每个可以被访问的类，因此需要了解我们所有的节点类型。因此，向我们的场景图中添加新的节点类型将需要更新访问者接口。结果，访问者模式最适用于层级结构稳定的情况（Alexandres, 2001）。

为了解决这个问题，让我们考虑向场景图添加一种类型名为 `CameraNode` 的新节点类型。一种简单的方法是在 `IVisitor` 接口中添加一个接受 `CameraNode` 引的 `Visit()` 纯虚方法。然而，从 API 向后兼容性的角度来看，向接口添加纯虚方法是一个坏做法，因为它会破坏所有现有的客户端代码。解决这个问题有几种替代方案。

- 1. 尽早考虑，你可以将 `INodeVisitor` 的第一个版本替换为针对 `BaseNode` 的 `Visit()` 纯虚方法。这将启用一个捕获方法，当遇到没有显式 `Visit()` 方法的节点类型时将调用该方法（必须修改 `BaseNode::Accept()` 使其不再是纯虚方法）。这样做的结果是，用户必须在这个捕获方法内部使用 `dynamic_cast` 调用来确定传递了哪种节点类型。采用这种解决方案将把访问者接口更改为：

```cpp
// visitor.h
class ShapeNode;
class TransformNode;
class LightNode;
class BaseNode;
{
class INodeVisitor
public:
```

```cpp
virtual void Visit(ShapeNode &node) = 0;
virtual void Visit(TransformNode &node) = 0;
virtual void Visit(LightNode &node) = 0;
virtual void Visit(BaseNode &node) = 0; // catch-all
```

- 2. 更好的解决方案是为新类型添加 `Visit()` 虚方法，而不是纯虚方法。也就是说，为新方法提供一个空实现，以便现有代码能够继续编译，同时允许用户在适当的地方为新节点类型实现类型安全的 `Visit()` 方法。这会将 `INodeVisitor` 接口更改为：

```cpp
//nodevisitor.h
class ShapeNode;
class TransformNode;
class LightNode;
class CameraNode;
class INodeVisitor {
public:
    virtual void Visit(ShapeNode &node) = 0;
    virtual void Visit(TransformNode &node) = 0;
    virtual void Visit(LightNode &node) = 0;
    virtual void Visit(CameraNode &node);
};
```

### 12.2.6 禁止子类化

关于继承扩展的最后一点，我将讨论你希望禁止用户从你提供的类中派生派生类的情况。在 Java 中，你可以将一个类声明为 `final` 以防止他人继承它，但 C++ 没有类似的概念。
正如所提到的，如果你声明一个类具有非虚析构函数，这应该是一个向优秀的程序员发送的信号，提醒他们应该重考虑是否继承该类。如果你希望有一种物理机制来防止用户对你的类进行子类化，最的方法将其所有构造函数设为私有。任何派生此类的尝试都会产生编译错误，因为派生类的构造函数无法调用你类的构造函数。你可以提供一个工厂方法来让用户创建对象的实例。

```cpp
class NonBase {
public:
    static NonBase* Create() { return new NonBase(); }
private:
    NonBase();
};
```

## 12.3 通过模板进行扩展

```cpp
class Derived : public NonBase {};
Derived d; // 编译错误!
```

这种方法的缺点是无法在栈上创建 `NonBase` 的实例。你的客户端必须使用 `NonBase::Create()` 静态函数来分配 `NonBase` 实例。如果这不可接受，还有另一种解决方案。你可以依靠虚继承来确保没有具体类可以继承自 `NonBase`，如下（Cline et al., 1998）。

```cpp
class NonBase;
```

```cpp
class NonBaseFinal
private:
  NonBaseFinal()
  friend class NonBase;
}
class NonBase :virtual public NonBaseFinal
public:
...
class Derived : public NonBase {};
Derived d; // 编译错误!
```

## 12.3 通过模板进行扩展

C++ 经常被称为多范式语言，因为它支持不同的编程风格，如过程化、面向对象和泛型。继承是使用面向对象概念扩展类的主要方式。然而，当使用模板编程时，扩展接口的默认方法是用具体类型对模板进行特化。

例如，STL 提供了各种类，如 `std::vector` 和 `std::set`。你可以使用这些类来创建包含任意数据类型的数据结构，例如 `std::vector<MyCustomClass *>`，STL 的创建者在设计库时并无法得知这些类型。

同样，Boost 提供了创建引用计数指针的能力，这种指针可以持有任何指针，而无需诉助于 `void*`。这是一个强大且通用的设施，可以由客户端自定义以创建任何对象的类型安全指针，例如 `boost::shared_ptr<MyCustomClass>`。

模板为你提供了一种极佳的方法编写适用于许多不同类型的代码，包括客户端在自己的代码中定义的类型。接下来的几节将介绍基于策略的模板（policy-based templates）的概念，以帮助你最大化类的类的灵活性。

### 12.3.1 基于策略的模板

Alexandrescu 在他的书中推广了基于策略的模板的使用（Alexandrescu,2001）。该术语指的是由较小的类（称为策略类 policy classes）构建复杂行为的方法，其中每个策略类定义了整个组件的接口。这一概念是使用接受多个模板参数（通常是模板参数）的类模板实现的，用符合接口的类进行实例化。

```cpp
template <typename T,
template <class> OwnershipPolicy = RefCounted,
class ConversionPolicy = DisallowConversion,
template <class> CheckingPolicy = AssertCheck,
template <class> StoragePolicy = DefaultSPStorage
>
class SmartPtr;
```
