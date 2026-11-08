
数组结果本身是为使用初始化列表提供上下文的唯一方式；实际值会被忽略。在C++11及以后，我们可以使用折叠表达式（在第22.6节，第307页讨论）来消除对这个多余变量的需要：

点击此处查看代码图像

variant/variantdestroy1.hpp

```cpp
template<typename... Types>
void Variant<Types...>::destroy()
{
    // call destroy() on each VariantChoice base class
    (VariantChoice<Types, Types...>::destroy(), ...);

    // indicate that the variant does not store a value
    this->setDiscriminator(0);
}
```

### 26.4.3 赋值

赋值建立在初始化和销毁的基础上，如下面的赋值运算符所示：

点击此处查看代码图像

variant/variantchoiceassign.hpp

```cpp
template<typename T, typename... Types>
auto VariantChoice<T, Types...>::operator= (T const& val)
{
    if (getDerived().getDiscriminator() == Discriminator) {
        // assign new value of same type
        *getDerived().template getBufferAs<T>() = val;
    }
    else {
        // assign new value of different type
        getDerived().destroy();              // try destroy
        new (getDerived().getBuffer()) T { val };
        getDerived().setDiscriminator(Discriminator);
    }
    return getDerived();
}

template<typename T, typename... Types>
auto VariantChoice<T, Types...>::operator= (T&& val)
{
    if (getDerived().getDiscriminator() == Discriminator) {
        // assign new value of same type
        *getDerived().template getBufferAs<T>() = std::move(val);
    }
    else {
        // assign new value of different type
        getDerived().destroy();              // try destroy
        new (getDerived().getBuffer()) T { std::move(val) };
        getDerived().setDiscriminator(Discriminator);
    }
    return getDerived();
}
```

与从某个已存储的值类型进行初始化一样，每个VariantChoice都可以提供一个赋值运算符，将值从其存储的值类型复制（或移动）到variant的存储区中。这些赋值运算符由Variant通过以下using声明继承：

点击此处查看代码图像

variant/variantchoiceassign.hpp

```cpp
using VariantChoice<Types, Types...>::operator=;
```

被修改后，赋值运算符将视情况把类型`T`的值交换赋值或移动赋值到缓冲区中。判别器不会改变。

如果variant没有存储类型`T`的值，赋值需要两步过程：使用`variant::destroy()`销毁当前值，然后使用`variant::place()`初始化一个类型`T`的新值，并适当地设置判别器。

使用placement new进行这种两步赋值有三个常见问题，每一个都必须考虑：

- 自赋值
- 异常
- `std::launder()`

### 自赋值

由于如下表达式，variant `v`可能发生自赋值：

```cpp
v = v;
```

采用上面实现的两步过程，已存储的值会在被复制之前销毁，可能导致内存损坏。幸运的是，自赋值总是意味着判别器匹配，因此这样的代码会调用`T`的赋值运算符，而不是这个两步过程。

### 异常

如果现有值的销毁完成，但新值的初始化抛出异常，variant处于什么状态？在我们的实现中，`variant::destroy()`将判别器值重置为`-1`。在异常情况下，判别器会被设置为适合新备选项的值。当新值初始化期间发生异常时，判别器会保持指示variant不存储值。在我们的设计中，这是产生无值variant的唯一方式。

下面的程序演示了如何通过尝试交换一个拷贝构造函数会抛出的类型的值，来触发一个没有存储值的variant：

点击此处查看代码图像

variant/variantassign.cpp

```cpp
#include "variant.hpp"
#include <exception>
#include <string>

class CopyableNonCopyable : public std::exception
{
};

class NonCopyable
{
public:
    NonCopyable() {
    }

    NonCopyable(NonCopyable const&) {
        throw CopyableNonCopyable();
    }

    NonCopyable& operator=(NonCopyable const&) = default;
};

Variant<int, NonCopyable> v(17);

try {
    NonCopyable nc;
    v = nc;
}
catch (CopyableNonCopyable) {
    std::cout << "Copy assignment of NonCopyable failed.\n";
    if (!v) {
        std::cout << "Variant has no value." << '\n';
    }
}
```

该程序的输出是：

Copy assignment of NonCopyable failed.
Variant has no value.

访问没有值的variant，无论是通过抛出异常的`get()`，还是通过下一节描述的访问者`Monostate`，都会抛出`EmptyVariant`异常，以便程序从这种异常情况中恢复。`empty()`成员函数检查variant是否处于这种空状态。

点击此处查看代码图像

variant/variant_empty.cpp

```cpp
template<class VariantType>
bool Variant<VariantType>::empty() const {
    return this->getDiscriminator() == 0;
}
```

我们两步赋值的第三个问题是一个微妙的问题，C++标准化委员会直到C++17标准化过程结束时才意识到它。我们接下来简要解释。

### std::launder

C++编译器通常旨在生成高性能代码，而提高生成代码性能的主要机制也许就是避免反复将数据从内存复制到寄存器。为此，编译器必须做出一些假设，其中一个假设是某些类型的数据在其生命周期内不可变。这包括const数据、引用（引用可以初始化，但之后不能修改），以及多态对象中存储的一些簿记数据，这些数据用于分派虚函数、定位虚基类以及处理类型化转换和动态转换。

上面两步赋值过程的问题在于，它本质上结束了一个对象的生命周期，并在同一位置开始另一个对象的生命周期，而编译器可能无法识别这一点。因此，编译器可能认为它从`Variant`对象先前状态获得的值仍然有效，而实际上使用placement `new`进行初始化已经使其失效。如果不加缓解，结果将是：使用具有不可变数据成员的类型的`Variant`的程序，在为现代性能进行编译时，可能偶尔产生无效结果。这类错误通常很难追踪（部分因为它们很少发生，部分因为它们在源代码中并不真正可见）。

从C++17开始，这个问题的解决方案是通过`std::launder()`访问新对象，它只是返回其参数，但会使编译器认识到结果地址指向的对象可能与编译器对传给`std::launder()`的参数的假设不同。然而，请注意，`std::launder()`只清洗它返回的地址，而不是传给它的参数。`std::launder()`使编译器认识到，在传给它的地址上实际存在一个指示类型的对象。有一些方法可以做得稍好一些（例如添加一个额外的指针成员来引用新对象，并在每次使用placement new赋值新值时使用“清洗过的”地址），但它们会使代码复杂化，难以维护。我们的方法简单且正确，只要我们接受一点性能损失。

`std::launder()`的情况并不完全令人满意：它非常可用，却难以察觉（例如，我们直到本书即将付印前才注意到它），而且不太声明式。了解它很有用，但使用起来很容易。因此，委员会的一些成员要求做更多工作以找到更令人满意的解决方案。[Launder]应构成对该问题更详细的描述。

## 26.5 访问者
