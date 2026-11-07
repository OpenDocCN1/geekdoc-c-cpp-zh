
```cpp
HasFriend<int> hfi1(10);
cout << "After hfi1 declared: ";
counts();
HasFriend<int> hfi2(20);
cout << "After hfi2 declared: ";
counts();
HasFriend<double> hfdb(10.5);
cout << "After hfdb declared: ";
counts();
report(hfi1);
report(hfi2);
report(hfdb);

return 0;
}
```

有些编译器会对使用非模板友元发出警告。下面是程序清单 14.22 中程序的输出：

```text
No objects declared: int count: 0; double count: 0
After hfi1 declared: int count: 1; double count: 0
After hfi2 declared: int count: 2; double count: 0
After hfdb declared: int count: 2; double count: 1
HasFriend<int>: 10
HasFriend<int>: 20
HasFriend<double>: 10.5
```

## 模板类的绑定模板友元函数

你可以通过让友元函数本身成为模板来修改前面的示例。特别是，你可以为绑定模板友元做好设置，使类的每个特化都获得一个匹配的友元特化。该技术比非模板友元稍微复杂一些，涉及三个步骤。

第一步，在类定义之前声明每个模板函数：

```cpp
template <typename T> void counts();
template <typename T> void report(T &);
```

接下来，在类内部再次将这些模板声明为友元。这些语句基于类模板参数类型声明特化：

```cpp
template <typename TT>
class HasFriendT
{
...
    friend void counts<TT>();
    friend void report<>(HasFriendT<TT> &);
};
```

声明中的 `<>` 将这些标识为模板特化。对于 `report()`，`<>` 可以留空，因为后面的模板类型实参可以从函数实参推导出来：

```cpp
HasFriend<TT>
```

不过，你也可以改用以下写法：

```cpp
report<HasFriend<TT> >(HasFriend<TT> &)
```

但是，`counts()` 函数没有参数，因此必须使用模板实参语法（`<TT>`）来指明其特化。还要注意，`TT` 是 `HasFriend` 类的参数类型。

同样，理解这些声明的最好方法是想象当你声明某个特定特化的对象时它们会变成什么。例如，假设你声明这个对象：

```cpp
HasFriend<int> squack;
```

然后编译器用 `int` 替换 `TT`，并生成以下类定义：

```cpp
class HasFriend<int>
{
...
    friend void counts<int>();
    friend void report<HasFriend<int> >(HasFriend<int> &);
};
```

一个特化基于 `TT`，它变成 `int`；另一个基于 `HasFriend<TT>`，它变成 `HasFriend<int>`。因此，模板特化 `counts<int>()` 和 `report<HasFriend<int> >()` 被声明为 `HasFriend<int>` 类的友元。

程序必须满足的第三个要求是为友元提供模板定义。程序清单 14.23 说明了这三个方面。注意，程序清单 14.22 有一个 `counts()` 函数，它是所有 `HasFriend` 类的友元；而程序清单 14.23 有两个 `counts()` 函数，其中一个分别是每个已实例化类类型的友元。由于 `counts()` 函数调用没有可供编译器推导所需特化的函数参数，这些调用使用 `counts<int>()` 和 `counts<double>()` 形式来指明特化。不过，对于 `report()` 的调用，编译器可以使用实参类型来推导特化。你也可以使用 `<>` 形式达到同样的效果：

```cpp
report<HasFriend<int> >(&hf2i);  // same as report(&hf2i);
```

### 程序清单 14.23 `tmp2tmp.cpp`

```cpp
// tmp2tmp.cpp -- template friends to a template class
#include <iostream>
using std::cout;
using std::endl;

// template prototypes
template <typename T> void counts();
template <typename T> void report(T &);

// template class
template <typename TT>
class HasFriendT
{
private:
    TT item;
    static int ct;
public:
    HasFriendT(const TT & i) : item(i) {ct++;}
    ~HasFriendT() { --ct; }
    friend void counts<TT>();
    friend void report<>(HasFriendT<TT> &);
};

template <typename T>
int HasFriendT<T>::ct = 0;

// template friend functions definitions
template <typename T>
void counts()
{
    cout << "template size: " << sizeof(HasFriendT<T>) << "; ";
    cout << "template counts(): " << HasFriendT<T>::ct << endl;
}

template <typename T>
void report(HasFriendT<T> & hf)
{
    cout << hf.item << endl;
}

int main()
{
    counts<int>();
    HasFriendT<int> hfi(10);
    HasFriendT<int> hfi2(20);
    HasFriendT<double> hfdb(10.5);
    report(hfi);   // generate report(HasFriendT<int> &)
    report(hfi2);  // generate report(HasFriendT<int> &)
    report(hfdb);  // generate report(HasFriendT<double> &)
    cout << "counts<int>() output:\n";
    counts<int>();
    cout << "counts<double>() output:\n";
    counts<double>();

    return 0;
}
```

下面是程序清单 14.23 中程序的输出：

```text
template size: 4; template counts(): 0
10
20
10.5
counts<int>() output:
template size: 4; template counts(): 2
counts<double>() output:
template size: 8; template counts(): 1
```

如你所见，`counts<double>()` 报告的模板大小与 `counts<int>()` 不同，这表明现在每个 T 类型都有自己的 `counts()` 友元。

## 模板类的非绑定模板友元函数

上一节中的绑定模板友元函数是在类外部声明的模板的模板特化。int 类特化会获得 int 函数特化，依此类推。通过在类内部声明一个模板，你可以创建非绑定友元函数，其中每个函数特化都是每个类特化的友元。对于非绑定友元，友元模板类型参数与模板类类型参数不同：

```cpp
template <typename T>
class ManyFriend
{
...
    template <typename C, typename D> friend void show2(C &, D &);
};
```

程序清单 14.24 展示了一个使用非绑定友元的示例。其中，函数调用 `show2(hfi1, hfi2)` 会匹配到以下特化：

```cpp
void show2<ManyFriend<int> &, ManyFriend<int> &>
        (ManyFriend<int> & c, ManyFriend<int> & d);
```

由于它是 ManyFriend 所有特化的友元，所以该函数可以访问所有特化的 item 成员。但它只使用对 `ManyFriend<int>` 对象的访问权限。

类似地，`show2(hfdb, hfi2)` 会匹配到以下特化：

```cpp
void show2<ManyFriend<double> &, ManyFriend<int> &>
        (ManyFriend<double> & c, ManyFriend<int> & d);
```

它也是所有 ManyFriend 特化的友元，并且它使用对 `ManyFriend<int>` 对象的 item 成员以及对 `ManyFriend<double>` 对象的 item 成员的访问权限。

### 程序清单 14.24 `manyfrnd.cpp`

```cpp
// manyfrnd.cpp -- unbound template friend to a template class
#include <iostream>
using std::cout;
using std::endl;

template <typename T>
class ManyFriend
{
private:
    T item;
public:
    ManyFriend(const T & i) : item(i) {}
    template <typename C, typename D> friend void show2(C &, D &);
};

template <typename C, typename D> void show2(C & c, D & d)
{
    cout << c.item << ", " << d.item << endl;
}

int main()
{
    ManyFriend<int> hfi1(10);
    ManyFriend<int> hfi2(20);
    ManyFriend<double> hfdb(10.5);
    cout << "hfi1, hfi2: ";
    show2(hfi1, hfi2);
    cout << "hfdb, hfi2: ";
    show2(hfdb, hfi2);

    return 0;
}
```

下面是程序清单 14.24 中程序的输出：

```text
hfi1, hfi2: 10, 20
hfdb, hfi2: 10.5, 20
```

## 模板别名（C++11）

为类型创建别名可能很方便，尤其是在模板设计中。你可以使用 typedef 为模板特化创建别名：

```cpp
// define three typedef aliases
typedef std::array<double, 12> arrd;
typedef std::array<int, 12> arri;
typedef std::array<std::string, 12> arrst;
arrd gallons; // gallons is type std::array<double, 12>
arri days;    // days is type std::array<int, 12>
arrst months; // months is type std::array<std::string, 12>
```

但如果你发现自己一遍又一遍地编写类似前面 typedef 的代码，你可能会怀疑自己是否忘记了某种能简化该任务的语言特性，或者语言是否忘记提供这样的特性。在这种情况下，C++11 提供了一项以前缺失的特性——一种使用模板来提供一族别名的方法。这种方法如下所示：

```cpp
template<typename T>
    using arrtype = std::array<T,12>;   // template to create multiple aliases
```

这使得 `arrtype` 成为一个可以用作类型的模板别名，如下所示：

```cpp
arrtype<double> gallons;    // gallons is type std::array<double, 12>
arrtype<int> days;          // days is type std::array<int, 12>
arrtype<std::string> months; // months is type std::array<std::string, 12>
```

简而言之，`arrtype<T>` 表示类型 `std::array<T,12>`。

C++11 还将 `using =` 语法扩展到非模板。在这种情况下，它等同于普通的 typedef：

```cpp
typedef const char * pc1;       // typedef syntax
using pc2 = const char *;       // using = syntax
typedef const int *(*pa1)[10];  // typedef syntax
using pa2 = const int *(*)[10]; // using = syntax
```

随着你逐渐习惯它，你可能会发现新形式更易读，因为它更清楚地将类型名与类型信息分开。

C++11 对模板的另一项新增是*可变参数模板*，它允许你定义可以接受可变数量初始化器的模板类或函数。第 18 章“拜访新的 C++ 标准”探讨了这一主题。

## 总结

C++ 提供了几种复用代码的方法。第 13 章“类继承”中描述的公有继承使你能够对 *is-a* 关系建模，派生类能够复用基类的代码。私有继承和保护继承也让你可以复用基类代码，这次是对 *has-a* 关系建模。使用私有继承时，公有
