

```cpp
template<typename T1, typename T2>
class MyClass {
private:
    T1 a;
    T2 b;
    ...
};
```

完全有可能出现一个或两个模板参数被空类类型替换的情况。如果发生这种情况，`MyClass<T1, T2>` 的表示形式可能不是最优的，并且每个 `MyClass<T1, T2>` 实例都可能浪费一个字的内存。

不过，可以通过将模板参数改为基类来避免这种情况：

```cpp
template<typename T1, typename T2>
class MyClass : private T1, private T2 {};
```

然而，这种直接的替代方案也有其自身的一系列问题：

- 当 `T1` 或 `T2` 被非类类型或联合类型替换时，它无法工作。
- 当两个参数被替换为相同类型时，它也无法工作（虽然这可以通过再添加一层继承来相当容易地解决；参见第 513 页）。
- 该类可能是 `final` 的，在这种情况下尝试继承它会导致错误。

即使我们圆满解决了这些问题，一个非常严重的问题依然存在：添加基类可能会从根本上修改给定类的接口。对于我们的 `MyClass` 类来说，这似乎并不重要，因为受影响的接口元素很少，但正如我们将在本章后面看到的，继承模板参数会影响成员函数是否为虚函数。显然，这种利用 EBCO 的方法充满各种麻烦。

对于模板参数已知只会被类类型替换、且类模板中还有另一个成员可用的常见情况，可以设计出一种更实用的工具。其主要思想是利用 EBCO 将可能为空的类型参数与另一个成员“合并”。例如，与其编写

```cpp
template<typename CustomClass>
class Optimizable {
private:
    CustomClass info; // might be empty
    void* storage;
    ...
};
```

模板实现者可以使用以下方式：

```cpp
template<typename CustomClass>
class Optimizable {
private:
    BaseMemberPair<CustomClass, void*> info_and_storage;
    ...
};
```

即使不看 `BaseMemberPair` 模板的实现，显然它的使用也会使 `Optimizable` 的实现更加冗长。然而，许多模板库实现者报告说，（对于其库的使用者而言）性能的提升确实证明了所增加的复杂性是值得的。我们将在第 576 页 25.1.1 节讨论 tuple 存储时进一步探讨这种惯用法。

`BaseMemberPair` 的实现可以相当简洁：

### inherit/basememberpair.hpp

```cpp
#ifndef BASE_MEMBER_PAIR_HPP
#define BASE_MEMBER_PAIR_HPP

template<typename Base, typename Member>
class BaseMemberPair : private Base {
private:
    Member mem;
public:
    // constructor
    BaseMemberPair (Base const & b, Member const & m)
        : Base(b), mem(m) {
    }

    // access base class data via first()
    Base const& base() const {
        return static_cast<Base const&>(*this);
    }
    Base& base() {
        return static_cast<Base&>(*this);
    }

    // access member data via second()
    Member const& member() const {
        return mem;
    }
    Member& member() {
        return mem;
    }
};

#endif // BASE_MEMBER_PAIR_HPP
```

通过将派生类作为模板参数向下传递给其基类，基类无需使用虚函数即可针对派生类定制自身行为。这使得 CRTP 在提取那些只能是成员函数（例如构造函数、析构函数和下标运算符）或依赖于派生类身份的公共实现时非常有用。

CRTP 的一个简单应用是跟踪某个类类型创建了多少个对象。这很容易实现：在每个构造函数中递增一个整型静态数据成员，并在析构函数中递减它。然而，在每个类中都提供这样的代码很繁琐，而通过单个（非 CRTP）基类实现此功能会混淆不同派生类的对象计数。因此，我们可以编写以下模板：

### inherit/objectcounter.hpp

```cpp
#include <cstddef>

template<typename CountedType>
class ObjectCounter {
private:
    inline static std::size_t count = 0; // number of existing objects
protected:
    // default constructor
    ObjectCounter() {
        ++count;
    }

    // copy constructor
    ObjectCounter (ObjectCounter<CountedType> const&) {
        ++count;
    }

    // move constructor
    ObjectCounter (ObjectCounter<CountedType> &&) {
        ++count;
    }

    // destructor
    ~ObjectCounter() {
        --count;
    }

public:
    // return number of existing objects:
    static std::size_t live() {
        return count;
    }
};
```

请注意，我们使用 `inline` 以便能够在类结构内部定义并初始化 `count` 成员。在 C++17 之前，我们必须将其定义在类模板外部：

```cpp
template<typename CountedType>
class ObjectCounter {
private:
    static std::size_t count; // number of existing objects
    ...
};

// initialize counter with zero:
template<typename CountedType>
std::size_t ObjectCounter<CountedType>::count = 0;
```

如果我们想要计算某个类类型仍存活（即尚未销毁）的对象数量，只需从 `ObjectCounter` 模板派生该类即可。例如，我们可以按照以下思路定义并使用一个带计数的字符串类：

### inherit/countertest.cpp

```cpp
#include "objectcounter.hpp"
#include <iostream>

template<typename CharT>
class MyString : public ObjectCounter<MyString<CharT>> {
    ...
};

int main()
{
    MyString<char> s1, s2;
    MyString<wchar_t> ws;
    std::cout << "num of MyString<char>: "
              << MyString<char>::live() << '\n';
    std::cout << "num of MyString<wchar_t>: "
              << ws.live() << '\n';
}
```

### 21.2.1 Barton-Nackman 技巧

1994 年，John J. Barton 和 Lee R. Nackman 提出了一种模板技术，他们称之为*受限模板扩展*（参见 [BartonNackman]）。这项技术的动机部分源于这样一个事实：在当时，函数模板的重载受到严重限制¹，而且大多数编译器都不支持命名空间。

为了说明这一点，假设我们有一个类模板 `Array`，希望为其定义相等运算符 `==`。一种可能的方法是将该运算符声明为类模板的成员，但这不是好的做法，因为第一个参数（绑定到 `this` 指针）所遵循的转换规则与第二个参数不同。由于 `operator ==` 在其参数方面应当是对称的，因此最好将其声明为命名空间作用域的函数。一种自然的实现方法概要可能如下所示：

```cpp
template<typename T>
class Array {
public:
    ...
};
```

```cpp
template<typename T>
bool operator== (Array<T> const& a, Array<T> const& b)
{
    ...
}
```

然而，如果函数模板不能重载，这就带来了一个问题：在该作用域中不能声明任何其他的 `operator ==` 模板，而其他类模板很可能需要这样的模板。Barton 和 Nackman 通过在类中将该运算符定义为普通友元函数解决了这个问题：

```cpp
template<typename T>
class Array {
    static bool areEqual(Array<T> const& a, Array<T> const& b);

public:
    ...
    friend bool operator== (Array<T> const& a, Array<T> const& b) {
        return areEqual(a, b);
    }
};
```

假设这个 `Array` 版本是针对 `float` 类型实例化的。那么该友元运算符函数将作为该实例化的结果被声明，但请注意，此函数本身并不是函数模板的实例化。它是一个普通的非模板函数，作为实例化过程的副作用被注入全局作用域。由于它是非模板函数，因此在函数模板重载被添加到 C++ 语言中之前，它也可以与其他 `operator ==` 声明一起重载。Barton 和 Nackman 称之为*受限模板扩展*，因为它避免使用适用于所有类型 `T` 的模板 `operator==(T, T)`（换句话说，即不受限的扩展）。

由于 `operator== (Array<T> const&, Array<T> const&)` 是在类定义内部定义的，因此它被隐式视为内联函数，所以我们决定将其实现委托给静态成员函数 `areEqual`，而后者不需要是内联的。

自 1994 年以来，友元函数定义的名称查找规则已经发生了变化，因此 Barton-Nackman 技巧在标准 C++ 中不再那么有用。在该技巧发明之时，当类模板通过称为*友元名称注入*的过程实例化时，友元声明在其外围作用域中可见。而标准 C++ 则是通过依赖于实参的查找来查找友元函数声明（具体细节参见第 220 页 13.2.2 节）。这意味着，函数调用的参数中至少有一个必须已经将包含该友元函数的类作为关联类。如果参数是某个不相关类类型、且该类型可以转换为包含友元的类，那么将找不到该友元函数。例如：

### inherit/wrapper.cpp

```cpp
class S {
};

template<typename T>
class Wrapper {
private:
    T object;
public:
    Wrapper(T obj) : object(obj) { // implicit conversion from T to Wrapper<T>
    }
    friend void foo(Wrapper<T> const&) {
    }
};
```

