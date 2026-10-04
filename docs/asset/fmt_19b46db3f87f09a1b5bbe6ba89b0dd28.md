
```cpp
template <typename T>    // 一个函数模板
void fun(T t)
{
    t->not_public();
}
template<typename X>    // 一个自由成员函数模板
bool operator==(A<X> const &lhs, A<X> const &rhs);
template<typename X>    // 一个类模板
class A {
    // fun() 被用作绑定到 A 的友元，
    // 为 X 实例化，无论 X 是什么
    friend void fun<A<X>>(A<X> t);
    friend bool operator==(A<X> const &lhs, A<X> const &rhs);

    int d_data = 10;
public:
    A();
private:
    void not_public();
};
template<typename X>
A<X>::A()
{
    fun(this);
}
template<typename X>
void A<X>::not_public()
{
    // 可以访问 lhs/rhs 的私有数据
}
bool operator==(A<X> const &lhs, A<X> const &rhs)
{
    return lhs.d_data == rhs.d_data;
}
```

```cpp
int main()
{
  A<int> a;
  fun(&a);
  // fun 为 A<int> 实例化。
}
```

## 22.10. 声明友元 (DECLARING FRIENDS)

### 22.10.2.1. 自由运算符作为嵌套类的友元

在类模板内部嵌套一个类时，可能希望为该嵌套类提供绑定到周围类的自由运算符（free operators）。这种情况在定义嵌套迭代器时会遇到，此时自由运算符`operator==(iterator const &lhs, iterator const &rhs)`优于成员运算符`operator==(iterator const &rhs) const`，因为后者不允许对 lhs 操作数进行提升（promotions）。

在嵌套类中将自由运算符`operator==`声明为友元是可能的，它会自动成为绑定友元。例如：

```cpp
#include <string>

template <typename Type>
struct String
{
  struct iterator
  {
    std::string::iterator d_iter;
    friend bool operator==(iterator const &lhs, iterator const &rhs)
    {
      return lhs.d_iter == rhs.d_iter;
    }
  }
  iterator begin()
  {
    return iterator();
  }
};

int main()
{
  String<int> str;
  return str.begin() == str.begin();
}
```

然而，这需要类内实现，应该避免这样做，因为它将接口和实现结合在一起降低了清晰度。

但当我们把实现移出接口之外时，会遇到`operator==`是一个函数模板的问题，它必须在类接口中声明为这种形式。编译器建议确保函数模板已经声明，并在函数名后添加`>`。

通过在

```cpp
template <typename Type>
bool operator==(Type const &lhs, Type const &rhs);
```

在`struct String`类模板之前之前声明它，然后如下实现`operator==`：

```cpp
template <typename Type>
inline bool operator==(String<Type>::iterator const &lhs,
               String<Type>::iterator const &rhs)
{
    return lhs.d_iter == rhs.d_iter;
}
```

编译器仍然报错，报告`'operator=='`的声明为非函数。

那么如何解决这个问题呢？已知有两种方法可以解决这个问题。其中一种是由 Radu Cosma 建议的（我们 2021-2022 学年 C++ 课程的助教），另一种解决方案在第 23.13.7.2 节提供。

Radu 建议使用 SFINAE 的应用：通过定义一个由嵌套类唯一定义的类型的自由运算符，并在函数实现中为该类型提供默认值，编译器会自动选择合适的重载函数。这对于声明了嵌套类的多个类以及同样适用于定义了嵌套类的类。这里是两个声明嵌套迭代器的类的示例：

```cpp
template <typename Type>
struct String
{
    struct iterator
    {
        using StringType_iterator = int;
        friend bool operator===(iterator const &lhs, iterator const &rhs);
    };
    std::string::iterator d_iter;
    iterator begin()
    {
        return iterator();
    }
};
```

```cpp
template <typename Type>
struct Container
{
    struct iterator
    {
        using ContainerType_iterator = int;
        friend bool operator===(iterator const &lhs, iterator const &rhs);
        int *d_ptr;
    };
    iterator begin()
    {
        return iterator();
    }
};
```

注意嵌套类将自由函数声明为函数模板特化。

然后，为每个嵌套类都提供一个自由运算符的实现。这些实现是提供了`Type`以及实现该运算符的嵌套类类型的函数模板：

```cpp
template <typename Type>
inline bool operator==(String<Type>::iterator const &lhs,
               String<Type>::iterator const &rhs)
{
    return lhs.d_iter == rhs.d_iter;
}
```

```cpp
template <typename Type>
inline bool operator==(Container<Type>::iterator const &lhs,
               Container<Type>::iterator const &rhs)
{
    return lhs.d_ptr == rhs.d_ptr;
}
```

主函数阐明了两个运算符的使用：

```cpp
int main()
{
    String<int> str;
    Container<int> cnt;
    str.begin() == cnt.begin();
}
```

## 22.10.3 未绑定模板作为友元 (Unbound templates as friends)

当函数模板被声明为未绑定友元时，它仅仅声明了模板的实例化。这在友元能够访问私有成员的情况下可能非常有用。函数、类和成员函数都可以是友元。以下是未绑定友元的语法约定：

- 将函数模板声明为未绑定友元：

```cpp
template <typename Type>
class Vector2:std::vector<Type>>
{
    template <typename Iterator, typename Class, typename Data>
    friend void Vector2::rows)(
,
 (, &Data);
};
```

- 将类声明为未绑定友元：

```cpp
template <typename Type>
class Vector2
{
    template <typename Iterator, typename Class, typename Data>
    friend bool operator==(
,, &rhs);
};
```

- 将成员函数声明为未绑定友元：

```cpp
template <typename Type>
class Vector2:std::vector<Type>>
{
    template <typename Iterator, typename Class, typename Data>
    friend void (2::rows)(Data);
};
```

如果函数模板定义在某个命名空间内，该命名空间也必须提及。假设`ForEach`定义在命名空间`FBB`中，其友元声明变为：

```cpp
template <typename Iterator, typename Class, typename Data>
friend FBB::ForEach(Iterator begin, Iterator end, Class &object,
    void (Class::member)(Data);
```

下面的示例展示了未绑定友元的使用。`Vector2`类存储了`Type`元素。它的`process`成员允许`ForEach`调用其`rows`成员。`rows`成员反过来允许`ForEach`调用其`columns`成员。因此，`Vector2`使用了`ForEach`的两次实例化，这对使用未绑定友元是一个清晰的提示。这里是程序：

```cpp
#include <iostream>
#include <vector>

namespace FBB {
    template <typename Iterator, typename Class, typename Data>
    void ForEach(Iterator begin, Iterator end, Class &object,
        void (Class::member)(Data)) {
        for (auto it = begin; it != end; ++it) {
            (object.*member)(*it);
        }
    }
}

template <typename Type>
class Vector2 : public std::vector<Type>
{
    using Iterator = Vector2::iterator;

    template <typename Iterator, typename Class, typename Data>
    friend FBB::ForEach(Iterator begin, Iterator end, Class &object,
        void (Class::*member)(Data);

public:
    void process();

private:
    void rows(std::vector<Type> &row);
    void columns(Type &str);
};

template <typename Type>
void Vector2::process()
{
    FBB::ForEach(this->begin(), this->end(), *this,
        &Vector2<Type>::rows);
}

template <typename Type>
void Vector2::rows(std::vector<Type> &row) 
{
    FBB::ForEach(row.begin(), row.end(), *this,
        &Vector2<Type>::columns);
}

template <typename Type>
void Vector2::columns(Type &str)
{
    std::cout << str << " ";
}

int main()
{
    Vector2<int> v{1, 2, 3, 4, 5};
    v.process();
    return 0;
}
```

## 22.10. 类的声明

```cpp
int main()
{
    Vector2<string> c;
    c.push_back(vector<string>(3, "Hello"));
    c.push_back(vector<string>(2, "World"));

    c.process();
}
/* 生成输出:

Hello Hello
World World
*/
```

- 同样地，一个完整的类模板可以被声明为友元。这允许友元成员函数的所有实例化都可以实例化声明为友元的类的类模板对象。在这种情况下，声明友元的类应该提供对该友元类的不同实例化均有用的功能（即使用不同参数的实例化）。其语法约定与声明未绑定的友元模板时使用的约定相似：

```cpp
template <typename Type>
class PtrVector
{
    template <typename Iterator, typename Class>
    friend class Wrapper; // 未绑定的友元类
}
```

该类模板的所有成员都可以使用任何实际类型作为其`Type`参数来实例化`PtrVector`。这允许`Wrapper`的实例化访问`PtrVector`的所有私有成员。

- 当类模板的某些成员需要访问另一个类模板的私有成员时（例如，另一个类模板有私有构造函数，或者第一个类模板的某些成员需要实例化第二个类模板对象），后者类模板可以仅将前者类模板中需要访问其私有成员的成员声明为友元。同样，友元类的接口可以不指定。但是，必须通知编译器该友元成员确实是一个类。因此，必须提供该类的的前向声明。在下一个示例中，`PtrVector`将`Wrapper::begin`声明为它的友元。注意类`Wrapper`的向前声明：

```cpp
template <typename Iterator>
class Wrapper;

template <typename Type>
class PtrVector
{
    template <typename Iterator> friend
    PtrVector<Type> Wrapper<Iterator>::begin(Iterator const &l);
    ...

};
```

## 22.10.4 扩展友元声明

通过扩展友元声明（这同样适用于类模板），可以将模板类型参数声明为友元。然而，模板类型参数并不一定是使用`friend`关键字有意义的类型（例如`int`）。在这些情况下，友元声明将被简单忽略。

考虑以下类模板，将`Friend`声明为友元：

```cpp
template <typename Friend>
class Class
{
    friend Friend;
    void msg();      // 私有，显示某些消息
};
```

现在，实际的`Friend`可以访问`Class`的所有成员：

```cpp
class Concrete
{
    Class<Concrete> d_class;
    Class<std::string> d_string;

public:
    void msg() {
        d_class.msg();      // OK：调用私有的 Class<Concrete>::msg()
        //d_string.msg();    // 编译失败：msg() 是私有的
    }
};
```

像`Class<int> intClass`这样的声明也是的，但这里的友元声明被简单忽略了。毕竟，没有`int`成员可以访问`Class<int>`的私有成员。

## 22.11 类模板派生

类模板也可以用于继承目的。当在类派生中使用类模板时，应当区分以下几种情况：

- 在派生普通类时，使用现有的类模板作为基类。派生类将部分是一个类模板，但当定义派生类的对象时，这在某种程度上是隐藏的。

- 在派生另一个类模板时，使用现有的类模板作为基类。在这里，类模板的特征保持清晰可见。

- 在派生类模板时，使用普通类作为基类。这种有趣的混合允许我们构建部分编译的类模板。

这些类模板派生的这些变体将在在本节及接下来的章节中详细阐述。

考虑以下基类：

```cpp
template <typename T>
class Base
{
    T const &;
  public:
    Base(T const &);
};
```

上述类是类模板可以用于派生如下：

```cpp
template <typename T>
class Derived: public Base<T>
{
    public:
    Derived(T);
};
```

类模板派生的这些变体允许我们构建派生类类。

在下一个示例中，`PtrVector`声明`Wrapper::begin`为其友元。注意类`Wrapper`的向前声明：
