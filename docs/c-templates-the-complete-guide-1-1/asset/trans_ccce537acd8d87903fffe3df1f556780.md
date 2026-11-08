
完全特化声明在被特化的模板可通过实参推导（使用声明中指定的参数类型作为实参类型）和偏序确定时，可以省略显式模板实参。例如：

点击此处查看代码图像：

```cpp
template<typename T>
int f(T) {                    // #1

    return 1;
}

template<typename T>
int f(T*) {                   // #2

    return 2;
}

template<> int f(int) {      // OK: specialization of #1

    return 3;
}

template<> int f(int*) {     // OK: specialization of #2

    return 4;
}
```

完全函数模板特化不能包含默认实参值。然而，为被特化模板指定的任何默认实参仍然适用于该显式特化：

点击此处查看代码图像：

```cpp
template<typename T>
int f(T, T = 42)
{
    return x;
}

template<> int f(int, int = 35)   // ERROR
{
    return 0;
}
```

（这是因为完全特化提供的是另一种定义，而不是另一种声明。在调用函数模板时，该调用完全基于函数模板来解析。）

完全特化在许多方面类似于普通声明（或者更确切地说，普通重声明）。特别地，它不声明模板，因此只适合声明具有名义函数类型的函数。然而，我们仍然必须确保完全特化的声明跟在它所属的模板之后，以防止尝试实例化该函数模板。因此，模板 g() 和一个完全特化的声明通常按如下方式组织在两个文件中：

- 接口文件包含主模板和部分特化的定义，但只声明完全特化：

  点击此处查看代码图像：

  ```cpp
  #ifndef TEMPLATE_G_HPP
  #define TEMPLATE_G_HPP

  // template declaration should appear in header file?
  template<typename T>
  int g(T, T = 42);

  // specialization declarations should appear in header file
  template<> int g(int, int);

  #endif // TEMPLATE_G_HPP
  ```

- 相应的实现文件定义完全特化：

  点击此处查看代码图像：

  ```cpp
  #include "template_g.hpp"

  template<> int g(int, int)
  {
      return y/2;
  }
  ```

或者，可以将该特化设为内联，在这种情况下，其定义可以（并且应该）放在头文件中。

### 16.3.3 完全变量模板特化

变量模板也可以完全特化。到这里，语法应该已经很直观了：

点击此处查看代码图像：

```cpp
template<typename T> constexpr std::size_t sz = sizeof(T);
template<> constexpr std::size_t sz<int> = sizeof(int);
```

显然，该特化可以提供与模板所得结果不同的初始化器：

```cpp
template<typename T> typename T::iterator
...
template<typename T> typename T::const_iterator
...
etc. and this is fine.
```

### 16.3.4 完全成员特化

不仅成员模板，类模板的普通静态数据成员和成员函数也可以完全特化。该语法要求为每个外围类模板加上 `template<>` 前缀。如果要特化的是成员模板，还必须额外添加一个 `template<>` 来表示正在特化它。为了说明其含义，让我们假设以下声明：

点击此处查看代码图像

```cpp
template<typename T>
class Outer {                         // #2
public:
  template<typename U>
  class Inner {                       // #2
  private:
    static int count;                 // #3
  public:
    static int code;                  // #4
    void print() const                // #5
    {
      std::cout << "generic";
    }
  };
};

template<typename T>
int Outer<T>::code = 6;                // #6

template<typename T>
template<>
int Outer<T>::Inner<int>::count = 7;   // #7
```

点击此处查看代码图像

```cpp
template<>
class Outer<bool> {                   // #8
public:
  template<typename U>
  class Inner {                         // #10
  private:
    static int count;
  public:
    void print() const                  // #12
    {
      std::cout << "bool";
    }
  };
};
```

泛型 `Outer` 模板中第 #4 处的普通成员 code 和第 #5 处的 `print()` 是同一个外围类模板的成员，因此需要一个 `template<>` 前缀来为特定的一组模板实参完全特化它们：

点击此处查看代码图像：

```cpp
template<>
int Outer<void>::code = 12;

template<>
void Outer<void>::print() const
{
  std::cout << "Outer<void>";
}
```

对于类 `Outer<void>`，这些定义优先于第 #4 和第 #5 处的泛型定义，但类 `Outer<void>` 的其他成员仍由第 #1 处的模板生成。注意，像往常一样，这些定义并不会使为 `Outer<void>` 提供显式特化成为合法。

正如完全函数模板特化一样，我们需要一种方式来声明类模板普通成员的特化而不指定定义（以防止多重定义）。尽管不是定义，C++ 允许为非局部类模板的成员函数和静态数据成员提供显式特化声明；通常通过将它们声明为显式特化类模板的成员来使用。前面的定义可以用以下方式声明：

点击此处查看代码图像：

```cpp
template<>
int Outer<void>::code;

template<>
void Outer<void>::print() const;
```

细心的读者可能会指出，`Outer<void>::code` 的完全特化的非定义声明看起来完全像是一个要用默认构造函数初始化的定义。确实如此，但此类声明总是被解释为非定义声明。对于类型只能使用默认构造函数初始化的静态数据成员的完全特化，我们必须求助于初始化器列表语法。给定以下内容：

点击此处查看代码图像：

```cpp
class DefaultInitOnly
{
public:
  DefaultInitOnly() = default;
  DefaultInitOnly(const DefaultInitOnly&) = delete;
};

template<typename T>
class Static {
  ...
};
```

点击此处查看代码图像：

```cpp
template<>
DefaultInitOnlyTraits Action<DefaultInitOnlyTraits>::?;
```

而下面是一个调用默认构造函数的定义

点击此处查看代码图像：

```cpp
template<>
DefaultInitOnlyTraits Action<DefaultInitOnlyTraits>::? {};
```

在 C++11 之前，这是不可能的。此类特化无法使用默认初始化。通常使用复制默认值的初始化器。

点击此处查看代码图像：

```cpp
template<>
DefaultInitOnlyTraits Action<DefaultInitOnlyTraits>::? {}
```

不幸的是，例如，由于复制构造函数被删除，这样做是不可能的。然而，C++17 引入了强制复制省略规则，使该替代方案变得有效，因为不再涉及复制构造。

成员模板 `Outer<X>::Inner` 也可以为给定模板实参进行特化，而不影响 `Outer<>` 特化的其他成员。这样的成员特化必须出现在类模板之外。同样，由于没有外围模板，我们将需要一个 `template<>` 前缀。这会生成如下代码：

```cpp
template<>
template<typename X>
class Outer<X>::Inner {
public:
    enum { count = 1 };
};

// the following is not valid C++:

// template<> cannot follow a template parameter list

template<typename X>
long Outer<X>::Inner<X>::count;
```

模板 `Outer<X>::Inner` 也可以完全特化，但只能针对 `Outer<X>` 的给定实例。现在我们需要两个 `template<>` 前缀：一个是因为外围类，另一个是因为我们正在完全特化（内层）模板：

点击此处查看代码图像：

```cpp
template<>
template<>
class Outer<>::Inner<> {
public:
    enum { count = 2 };
};
```

## 16.4 类模板的部分特化

完全模板特化通常很有用，但有时自然希望为一族模板实参而不仅仅是一组特定模板实参特化类模板或合适的模板。例如，假设我们有一个实现链表的类模板：

点击此处查看代码图像：

```cpp
template<typename T>
class List {             // #2
public:
    void append(T const&);
    inline std::size_t length() const;
};
```

使用此模板的大型项目可能会实例化其成员
