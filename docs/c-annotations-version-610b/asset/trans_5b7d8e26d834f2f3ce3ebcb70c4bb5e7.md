
为了避免这些缺点，好的做法是*防止*使用指向策略类的引用或指针来引用或指向派生类对象。这可以通过为策略类提供*非虚的受保护析构函数*来实现。非虚析构函数没有性能损失，而且由于其析构函数是受保护的，用户不能使用指向策略类的指针或引用来引用从策略类派生的类。

### 22.4.3 按策略组织结构

策略类通常定义行为，而非结构。策略类通常用于参数化从它们派生的类在某个方面的行为。然而，不同的策略可能需要不同的数据成员。这些数据成员也可以由策略类来定义。因此，策略类可以同时用于定义行为和结构。

通过提供定义良好的接口，从策略类派生的类可以利用策略类的不同结构来定义成员特化，从而发挥各自优势。例如，基于普通指针的策略类可以借助C风格的指针操作来提供其功能，而基于向量的策略类则可以直接使用vector的成员。

在这个例子中，可以设计一个通用类模板`Size`，它期望一个类似容器的策略，使用容器中常见的特性，定义策略中指定容器的数据（因此也定义了其结构）。例如：

```cpp
template <typename Data, template <typename> class Container>
struct Size: public Container<Data>
{
    size_t size()
    {                          // relies on the container's 'size()'
                               // note: can't use 'this->size()'
        return Container<Data>::size();
    }
};
```

现在可以为一个更简单的存储类定义特化，例如使用普通指针（该实现利用了`std::pair`的数据成员first和second；参见本节末尾的示例）：

```cpp
template <typename Data>
struct Size<Data, Plain>: public Plain<Data>
{
    size_t size()
    {                          // relies on pointer data members
        return this->second - this->first;
    }
};
```

根据模板作者的意图，还可以实现其他成员。

为了简化上述模板的实际使用，可以构造一个通用包装类：它使用与实际使用的存储类型（例如`std::vector`或某个普通存储类）匹配的`Size`模板来定义其结构：

```cpp
template <typename Data, template <typename> class Store>
class Wrapper: public Size<Data, Store>
{};
```

上述类现在可以如下使用（*顺便*展示一个极其基本的`Plain`类）：

```cpp
#include <iostream>
#include <vector>

template <typename Data>
struct Plain: public std::pair<Data *, Data *>
{};

int main()
{
    Wrapper<int, std::vector> wiv;
    std::cout << wiv.size() << "\n";

    Wrapper<int, Plain> wis;
    std::cout << wis.size() << "\n";
}
```

现在，`wiv`对象定义了vector数据，而`wis`对象仅定义了一个`std::pair`对象的数据成员。

## 22.5 模板别名（C++11，4.7）

除了函数模板和类模板之外，C++11还使用模板为一组类型定义别名。这称为*模板别名*。模板别名可以被特化。模板别名的名称是一个类型名。

模板别名可以用作模板模板参数的实参。这使我们能够避免使用模板模板参数时可能遇到的“意外的默认参数”。例如，定义一个指定`template <typename> class Container`的模板是可以的，但不可能将`vector`或`set`这样的容器指定为模板模板实参，因为`vector`和`set`容器还定义了第二个模板参数，用于指定它们的分配策略。

模板别名通过 using 声明来定义，为现有的（可能是部分或完全特化的）模板类型指定别名。在下面的例子中，`Vector`被定义为`vector`的别名：

```cpp
template <typename Type>
using Vector = std::vector<Type>;

Vector<int> vi;              // same as std::vector<int>
std::vector<int> vi2(vi);    // copy construction: OK
```

那么，这样做有什么意义呢？观察`vector`容器，我们发现它定义了两个而不是一个模板参数，第二个参数是分配策略`_Alloc`，默认设置为`std::allocator<_Tp>`：

```cpp
template<typename _Tp, typename _Alloc = std::allocator<_Tp> >
class vector: ...
```

现在定义一个类模板`Generic`，它定义一个模板模板参数：

```cpp
template <typename Type, template <typename> class Container>
class Generic: public Container<Type>
{
    ...
};
```

很可能，`Generic`提供了由实际用于创建`Generic`对象的容器所提供的成员，并在这些成员之上添加了一些自己的成员。然而，像`std::vector`这样的简单容器不能使用，因为`std::vector`不匹配`template <typename> class Container`参数；它需要`template <typename, typename> class Container`模板参数。

然而，`Vector`模板别名被定义为一个只含一个模板类型参数的模板，并且它使用`vector`的默认分配器。因此，将`Vector`传给`Generic`可以正常工作：

```cpp
Generic<int, Vector> giv;        // OK
Generic<int, std::vector> err;  // won’t compile: 2nd argument mismatch
```

借助一个小型模板别名，还可以在`Generic`中使用完全不同类型的容器，例如`map`：

```cpp
template <typename Type>
using MapString = std::map<Type, std::string>;

Generic<int, MapString> gim;    // uses map<int, string>
```

## 22.6 特征类

在`std`命名空间中散布着*特征类*。例如，大多数**C++**程序员都见过编译器在针对`std::string`对象执行非法操作时提到‘`std::char_traits<char>`’，比如`std::string s(1)`。

特征类用于在编译期对类型做出决策。特征类使我们能够将适当的代码应用于适当的数据类型，无论是指针、引用还是普通值，所有这些都可能与`const`结合。要使用的特定数据类型可以从使用模板时指定（或隐含）的实际类型推断出来。这完全可以自动化，不需要模板编写者做出任何决定。

特征类使我们能够开发模板`<typename Type1, typename Type2, ...>`，而无需指定大量特化来覆盖所有组合，例如值、(const)指针或(const)引用，这很快就会导致模板特化出现难以维护的指数爆炸（例如，如果每个模板参数允许这五种不同类型，那么当使用两个模板类型参数时，就已经会产生25种组合：每种组合都必须由可能不同的特化来覆盖）。

有了可用的特征类，实际类型可以在编译期被推断，允许编译器推导出实际类型是指针、成员指针还是const指针，并在实际类型是例如左值引用或右值引用类型时做出类似的推导。这反过来又使我们能够编写定义诸如`argument_type`、`first_argument_type`、`second_argument_type`和`result_type`等类型的模板，这些类型是若干通用算法（如`count_if()`）所要求的。

特征类通常不执行任何行为。也就是说，它没有构造函数，也没有可调用的成员。相反，它定义一系列类型和枚举值，这些类型和枚举值根据传递给特征类模板的实际类型而具有特定的值。编译器会从一组可用的特化中选择一个与实际的模板类型参数相匹配的特化。

定义特征模板的出发点是定义一个普通的`struct`，定义诸如`int`之类的普通值类型的特征。这为特定特化奠定了基础，这些特化会修改模板可能指定的任何其他类型的特征。

为了使问题具体化，假设我们打算创建一个特征类`BasicTraits`，告诉我们一个类型是普通值类型、指针类型、左值引用类型还是右值引用类型（所有这些类型可能是或可能不是`const`类型）。

无论实际提供的类型是什么，我们都希望能够确定“普通”类型（即没有任何修饰符、指针或引用的类型）、“指针类型”和“引用类型”，从而让我们能够
