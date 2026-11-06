
一组，使用 `extern` 模板声明。这不仅适用于显式使用的成员，也适用于隐藏成员（复制构造函数、移动构造函数、转换运算符、在类型提升期间调用的构造函数，等等）；编译器假定所有这些都已在别处实例化；

- 尽管上述源文件可以编译，但模板的实例化必须在链接器能够构建最终程序之前可用。为实现这一点，可以构建一个或多个源文件，在其中提供所有必需的实例化。

在独立程序中，人们可能会推迟定义所需成员，并等待链接器报告未解析的外部引用。然后可以利用这些信息创建一系列实例化声明，再将它们链接到程序以满足链接器。不过，这并不是一项非常简单的任务，因为声明必须严格匹配成员在类接口中的声明方式。更简单的方法是定义一个实例化源文件，在其中程序使用的所有设施实际上都在一个不会被程序调用的函数中实例化。通过将这个实例化函数添加到包含 `main` 的源文件，我们可以确保所有必需成员也被实例化。下面是一个如何做到这一点的示例：

```cpp
#include <vector>
#include <iostream>

extern void vectorUser();

int main()
{
    vectorUser();
}

// this part is never called. It is added to make sure all required
// features of declared templates will also be instantiated.

namespace
{
    void instantiator()
    {
        std::vector<int> vi;
        vi.size();
    }
}
```

- 最后，但同样重要的是：类模板的完全匹配的实例化声明（例如，对于 `std::vector<int>`）如下所示：

```cpp
template class std::vector<int>;
```

然而，将其添加到源文件会实例化整个类，即其所有成员现在都被实例化。这可能不是您想要的，因为它可能会不必要地增大最终可执行文件的大小。

- 另一方面，如果已知所需的模板成员已在别处实例化，则可以使用 `extern template` 声明来阻止当前编译单元中的成员实例化，这可能会加快编译速度。例如，

```cpp
// the compiler assumes that required members of
// vector<> have already been instantiated elsewhere
extern template class std::vector<int>;

int main()
{
    std::vector<int> vi(5);    // constructor and operator[]
    ++vi[0];                   // are NOT instantiated
}
```

## 21.2 静态数据成员

当在类模板中定义静态成员时，它们会为类模板实例化的每一种新类型分别定义。由于它们是静态成员，对于类模板实例化的每种类型，只会有一个成员。例如，在如下类中：

```cpp
template <typename Type>
class TheClass
{
    static int s_objectCounter;
};
```

对于每一种不同的 Type 指定，都会有*一个* TheClass<Type>::s_objectCounter。下面的对象定义只会导致一个静态变量被实例化，并由这两个对象共享：

```cpp
TheClass<int> theClassOne;
TheClass<int> theClassTwo;
```

在接口中提及静态成员并不意味着这些成员实际上已被定义。它们只是被*声明*，必须单独*定义*。对于类模板的静态成员也是如此。静态成员的定义通常紧跟在（即位于）模板类接口之后提供。例如，静态成员 s_objectCounter 的定义位于其类接口正下方，如下所示：

```cpp
template <typename Type>            // definition, following
int TheClass<Type>::s_objectCounter = 0;    // the interface
```

这里 s_objectCounter 是一个 int，因此独立于模板类型参数 Type。对相同 Type 多次实例化 s_objectCounter 不会造成问题，因为链接器会从最终可执行文件中删除除一个实例化之外的所有实例化（参见第 20.5 节）。

在类似列表的构造中，如果需要指向该类自身对象的指针，则在定义静态变量时必须使用模板类型参数 Type。示例：

```cpp
template <typename Type>
class TheClass
{
    static TheClass *s_objectPtr;
};

template <typename Type>
TheClass<Type> *TheClass<Type>::s_objectPtr = 0;
```

像往常一样，定义可以从变量名往回读到定义的开头：TheClass<Type> 类的 s_objectPtr 是一个指向 TheClass<Type> 对象的指针。

当定义模板类型参数类型的静态变量时，当然不应将其初始值设为 0。默认构造函数（例如，Type()）通常更合适。示例：

```cpp
template <typename Type>                    // s_type's definition
Type TheClass<Type>::s_type = Type();
```

### 21.2.1 关键字 'typename' 的扩展用法

到目前为止，关键字 typename 一直用于指示模板类型参数。然而，它也用于消除模板内代码的歧义。考虑以下函数模板：

```cpp
template <typename Type>
Type function(Type t)
{
    Type::Ambiguous *ptr;

    return t + *ptr;
}
```

当编译器处理这段代码时，它会报错，错误消息乍看之下令人费解，类似于：

```text
4: error: 'ptr' was not declared in this scope
```

这个错误消息令人费解，因为程序员的本意是声明一个指向类模板 `Type` 内定义的 `Ambiguous` 类型的指针。但是，编译器面对 `Type::Ambiguous` 时可能会以多种方式解释该语句。显然，它无法检查 `Type` 本身以揭示 `Type` 的真实性质，因为 `Type` 是模板类型。因此，`Type` 的实际定义尚不可用。

编译器面临两种可能性：`Type::Ambiguous` 要么是 `as yet mysterious` 模板 `Type` 的 *静态成员*，要么是 `Type` 的 *子类型*。由于标准规定编译器必须假定前者，因此语句

```cpp
Type::Ambiguous *ptr;
```

被解释为静态成员 `Type::Ambiguous` 与（现在未声明的）实体 `ptr` 的 *乘法*。现在错误消息的原因应该清楚了：在此上下文中，`ptr` 是未知的。

为了消除标识符引用模板类型参数的子类型时代码的歧义，必须使用关键字 `typename`。因此，上述代码改为：

```cpp
template <typename Type>
Type function(Type t)
{
    typename Type::Ambiguous *ptr;

    return t + *ptr;
}
```

类经常定义子类型。当这些子类型在模板定义中作为模板类型参数的子类型出现时，必须使用 typename 关键字将它们标识为子类型。示例：类模板 `Handler` 定义了一个 typename `Container` 作为其模板类型参数。它还定义了一个数据成员，用于存储容器 begin 成员返回的迭代器。此外，Handler 提供了一个构造函数，接受任何支持 `begin` 成员的容器。Handler 的类接口可能如下所示：

```cpp
template <typename Container>
class Handler
{
    Container::const_iterator d_it;

public:
    Handler(Container const &container)
    :
        d_it(container.begin())
    {}
};
```

设计这个类时我们有什么想法？

- typename `Container` 表示任何支持迭代器的容器。
- 容器大概支持成员 `begin`。初始化 `d_it(container.begin())` 显然依赖于模板的类型参数，因此只检查基本语法正确性。
- 同样，容器大概支持一个 *子类型* `const_iterator`，它定义在类 `Container` 中。

最后一项考虑表明需要 `typename`。如果省略它并实例化 `Handler`，编译器会产生一个奇怪的编译错误：

```cpp
#include "handler.h"
#include <vector>
using namespace std;

int main()
{
    vector<int> vi;
    Handler<vector<int> > ph(vi);
}
/*
    Reported error:

    handler.h:4: error: syntax error before `;' token
*/
```

显然，下面这一行

```cpp
Container::const_iterator d_it;
```

在类 `Handler` 中导致问题。它被编译器解释为 *静态成员* 而不是子类型。使用 `typename` 可以解决该问题：

```cpp
template <typename Container>
class Handler
{
    typename Container::const_iterator d_it;
    ...
};
```

一个有趣的例证表明编译器确实将 `X::a` 假定为类 `X` 的成员 `a`，这可以从我们尝试使用以下 `Handler` 构造函数实现编译 `main` 时得到的错误消息中看出：

```cpp
Handler(Container const &container)
:
    d_it(container.begin())
{
    size_t x = Container::ios_end;
}
/*
    Reported error:

    error: `ios_end' is not a member of type `std::vector<int,
            std::allocator<int> >'
*/
```

