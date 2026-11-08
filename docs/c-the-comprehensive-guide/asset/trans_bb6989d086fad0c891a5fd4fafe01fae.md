
在这里，你看到的是 `setData()` 针对 `MyContainer<std::string>` 的一个特化；当你实例化 `MyContainer<std::string>` 对象时，就会使用并生成这个特化，`main()` 中简要展示了这一点。一般情形仍然保留，并适用于所有尚未获得特化的形式类型参数。因此，对于 `string`，输出带有方括号——如特化中所编程的那样——而对于 `int`，输出不带方括号——如一般情形中所编程的那样。

`std::copyable` 是 C++20 概念。没有概念时，你写 `typename`。

## 23.5.3 从类模板创建对象

现在我将更详细地说明如何从类模板创建实例。与函数模板调用一样，类模板只有在首次使用时才会用相应类型进行实例化。在本书中，你已经多次使用过实例化类模板，例如 `vector<int>`。除了类名之外，你还必须在尖括号内为形式数据类型指定类型，编译器应据此生成一个类。

下面的清单展示了最小示例类 `MyContainer<T>` 的几个经典应用示例。

```cpp
// https://godbolt.org/z/9vP3o68bW
#include <iostream>
#include <string>
#include <concepts>    // copyable, C++20

template <std::copyable T>
class MyContainer {
    T data_;
public:
    void setData(const T& d) { data_ = d; }
    T getData() const { return data_; }
};

class IntValue {
    int val_;
public:
    explicit IntValue(int val=0) : val_(val) {}
    int getInt() const { return val_; }
};

int main() {
    // C-array with three MyContainer<double> instances
    MyContainer<double> dcont[3];
    dcont[0].setData(123.123);
    dcont[1].setData(234.234);
    std::cout << dcont[0].getData() << std::endl;
    std::cout << dcont[1].getData() << std::endl;
    // custom data type as formal parameter
    IntValue ival{100'000};
    MyContainer<IntValue> scont;
    scont.setData(ival);
    std::cout << scont.getData().getInt() << std::endl;
    // string as formal parameter
    std::string str{"Text"};
    MyContainer<std::string> strCont;
    strCont.setData(str);
    std::cout << strCont.getData() << std::endl;
}
```

**清单 23.32** 这就是从模板类创建实例的方式。

当声明 `MyContainer<double> dcont[3]` 时，编译器会为 `MyContainer<double>` 生成一个类，然后为 C 数组创建该类的三个实例。编译器将类模板的形式数据类型 `T` 替换为具体的 `double` 类型。通过 `dcont[...].setData(...)`，我为其中一些容器实例设置值并将它们输出。

这同样适用于自定义类，正如我用 `MyContainer<IntValue>` scont 实例化所演示的那样。在这里，编译器将为 `MyContainer<IntValue>` 生成一个类。编译器将形式数据类型 `T` 替换为 `IntValue` 类。

在最后一个实例化 `MyContainer<std::string> strCont` 中，编译器生成了该类的另一种形式。在这里，它用 `std::string` 替换了形式数据类型。

> **双重错误检查**
> 
> 一般来说，实例化模板的另一个优点是编译器必须两次检查错误：一次是在解析模板定义时，另一次是在用具体类型实例化模板时。

### 类模板实参推导（CTAD）

自 C++17 起，编译器可以根据构造函数实参本身的类型推导模板类的参数类型（通过类模板实参推导 [CTAD]，又称模板参数推导）。直到并包括 C++14，你始终必须显式列出类型参数。你已经见过函数模板的这种做法，具体见[第 23.1.2 节](#)。在下面的清单中，现在作为模板的是类。

```cpp
// https://godbolt.org/z/YaEW5aTra
#include <string>
#include <vector>
#include <set>
#include <tuple>
#include <memory> // shared_ptr
template <typename T>
class MyStuff {
    T data_;
public:
    MyStuff() : data_{} {}                 // default constructor
    MyStuff(const T& d) : data_{d} {}      // copy constructor
    T getStuff() const { return data_; }
};
class IntValue {
    int val_;
public:
    explicit IntValue(int val=0) : val_{val} {}
    int getInt() const { return val_; }
};
int main() {
    MyStuff intStuff(12);                  // becomes MyStuff<int>
    std::vector vs{1,2,3,4};              // becomes vector<int>
    MyStuff valStuff{ IntValue{33} };      // becomes MyStuff<IntValue>
    std::tuple tpl{ 23, 'a' };             // becomes tuple<int,char>
    std::set twoThree (vs.begin()+1, vs.end()-1); // becomes set<int>
    //The compiler cannot deduce:
    MyStuff<double> dblStuff;              // no constructor argument
    std::vector<char> vcs(10);             // size 10, but of what type?
    std::shared_ptr<int> ptr(new int{88}); // no rule for int*
}
```

**清单 23.33** 从构造函数实参推导模板参数。

如你所见，有些情况下编译器无法推导模板类的类型——例如，当你使用默认构造函数（没有实参）时，就像 dblStuff 那样；或者对于编译器无法推导类型的构造函数，就像 vcs 那样。

对于某些模板类，编译器无法或不愿猜测：对于 ptr，它本可以从构造函数的实参类型 int* 推导出 shared_ptr<int> 的 int，但它不会自动这样做。

> **推导指引**
> 
> 编译器足够智能，可以从 `int` 类型的构造函数实参推断出模板参数也应为 `int`。然而，如果你查看示例中的 `twoThree`，你会看到传入的是*迭代器*，而不是 `int` 值。编译器如何知道不要构造 `<set<iterator>>` 呢？

```cpp
template<class IT>
  set(IT, IT)
  -> set<typename std::iterator_traits<IT>::value_type>;
```

这意味着：“如果两个构造函数实参类型相同，就检查两者是否存在 `iterator_traits<IT>::value_type`；如果存在，那么它就是 set 的类型。”

即使在编译器能够推断的情况下，在模板类中省略实参也并不总是好事。有时最好显式命名。因此，只有在能让代码*更好*而不只是*更短*时，才使用这个新特性。

此外，只有非常现代的编译器才支持此特性。直到并包括 C++14，编译器都无法使用构造函数实参来推导模板类型，因此这仅限于函数模板。因此，标准库中的许多类型都定义了 make_helper 函数来解决这个问题。结合 auto，你还能获得简洁的代码。

```cpp
auto tpl = std::make_tuple( 5, 'x' );
auto ptr = std::make_shared( 5 );
```

**清单 23.34** 长期以来，你一直可以使用 make_helper 函数和 auto。

### 本书中的模板实参推导

在本书中，我将更倾向于新形式，因为我相信有了这项创新，C++ 会更好、更易理解、更易使用。如果你的编译器尚不支持模板实参推导，请改用 auto 和函数，或显式指定。

## 23.5.4 具有多个形式数据类型的类模板

与函数模板一样，类模板本质上可以使用任意数量的附加形式数据类型。你只需在类模板定义的尖括号内列出这些形式数据类型，用逗号分隔，并使用 typename（或 class）关键字。在下面的示例中，你会看到 `std::pair` 的一个原始版本，它本身就是一个具有多个形式数据类型的类模板：

```cpp
// https://godbolt.org/z/dMTnbT1v4
#include <iostream>
#include <concepts>    // copyable, C++20

template<std::copyable T, std::copyable U>
class MyPair {
    T data01_;
    U data02_;
public:
    MyPair(const T& t, const U& u) : data01_{t}, data02_{u} {}
    void print(std::ostream& os) const {
        os << data01_ << " " << data02_ << std::endl;
    }
};

int main() {
    std::string month{"January"};
    int temp = -5;
    MyPair<std::string, int> temperature(month, temp);
    temperature.print(std::cout);
}
```

使用 MyPair<T, U> 类模板，你可以创建一个能够管理两个（几乎）任意类型的类。在示例中，我使用 MyPair<std::string, int> temperature 创建了一个具有具体 std::string 和 int 类型的实例。对于 MyPair<std::string, int>，编译器实例化模板并生成类。然后编译器从这个类创建 temperature 实例。除了 C++20 的 copyable 概念，你也可以使用 typename。

这里还有另一个提示，适用于你不想实例化包含多个形式数据类型的类模板的情况。一个例子是 MyPair<double, double>，其中编译器将 T 替换为 double，将 U 替换为 double。这个提示是：如果你想用 MyPair<double> 生成该类的实例，只需如下调整模板头：

```cpp
// https://godbolt.org/z/jbafeEdoW
#include <iostream>
#include <concepts>    // copyable, C++20

template<std::copyable T, std::copyable U=T>
class MyPair {
    T data01_;
    U data02_;
public:
    MyPair(const T& t, const U& u) : data01_{t}, data02_{u} {}
    void print(std::ostream& os) const {
        os << data01_ << " " << data02_ << std::endl;
    }
```
