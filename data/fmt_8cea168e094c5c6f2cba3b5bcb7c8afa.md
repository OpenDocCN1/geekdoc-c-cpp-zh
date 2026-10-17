
`cout` << " " << `ni` << " " << `nb` << `endl`;

`cout` << "Done.\n";

`return` 0;

}

```

列表 14.21 中程序的运行示例如下：

Enter double pairs, such as 4.5 (0 to end):
50 22
25 33
60 12
0 0
60 12
25 33
50 22
Done.

你可以将模板对与普通参数混合。例如，`Crab` 的声明可以这样开头：

```cpp
template <template <typename T> class Thing, typename U, typename V>
class Crab
{
private:
    Thing<U> s1;
    Thing<V> s2;
    ..
};
```

现在，存储在成员 `s1` 和 `s2` 中的类型是泛型类型，而不是硬编码类型。这需要将程序中 `nebula` 的声明更改为：

```cpp
Crab<Stack, int, double> nebula; // T=Stack, U=int, V=double
```

## 模板类与友元

模板类也可以友元。你可以将友元分为三类：

- 非模板友元
- 绑定模板友元，意味着友元的类型由模板实例化确定
- 解绑定模板友元，意味着模板的所有实例化

让我们看看它们的示例。

### 模板类的非模板友元

让我们为模板类声明一个普通函数作为友元：

```cpp
template <typename T>
class HasFriend {
public:
    ..
    friend void counts(); // 模板
};
```

这种声明使得 `counts()` 函数是所有模板实例的友元。

### 模板类

假设你想为模板类提供一个友元。可以有这样的声明吗？

```cpp
friend void report(HasFriend); // 可以吗？
```

答案是否定的。因为没有 `HasFriend` 这种类型，只有 `HasFriend<int>` 这样的实例化。因此，你需要为特定的实例化提供友元，例如：

```cpp
template <typename T>
class HasFriend
{
    ...
};
```

你需要 产生特定的 `int` 类型：

```cpp
HasFriend<int>;
```

```cpp
HasFriend<int> hfil(10);
cout << "After hfil declared: ";
counts();
HasFriend<int> hfi2(20);
cout << "After hfi2 declared: ";
counts();
HasFriend<double> hfdb(10.5);
cout << "After hfdb declared: ";
counts();
reports(hfil);
reports(hfi2);
reports(hfdb);
return 0;
```

某些编译器会对比使用非模板友元函数发出警告。以下是列表 14.22 中程序的输出：

```
No objects declared: int count: 0; double count: 0
After hfil declared: int count: 1; double count: 0
After hfi2 declared: int count: 2; double count: 0
After hfdb declared: int count: 2; double count: 1
HasFriend<int>: 10
HasFriend<int>: 20
HasFriend<double>: 10.5
```

### 将友元函数绑定到模板类

你可以通过让友元函数本身成为模板来修改上一个示例。具体来说，你可以为模板友元进行设置，使得类的每个特化版本都能获得匹配的友元特化版本。这种技术比非模板友元稍微复杂一些，涉及三个步骤。

第一步，在类定义之前声明每个模板函数：

```cpp
template <typename T> void counts();
template <typename T> void report(T &);
```

接下来，在类内部内部再次将这些模板声明为友元。这些语句根据类模板参数类型声明了特化版本：

```cpp
template <typename TT>
class HasFriendT
{
    friend void counts<TT>();
    friend void report(HasFriendT<TT> &);
};
```

声明中的 `<>` 标识这些为模板特化。在 `report()` 的情况下，`<>` 可以为空，因为后续的模板类型参数可以从函数参数推推出来：

```cpp
HasFriendT<TT>
```

然而，你也可以使用这种写法：

```cpp
report<HasFriendT<TT>> (HasFriendT<TT> &)
```

`counts()` 函数没有参数，因此你必须使用模板参数语法（`<TT>`）来指示其特化。注意，`TT` 是 `HasFriendT` 类的参数。

再次，理解这些声明最好的方法是想象当你声明一个特定特化的对象时，它们会变成什么样。例如，假设你声明了这个对象：

```cpp
HasFriendT<int> squash;
```

然后编译器用 `int` 替换 `TT`，并生成了如下类定义：

```cpp
class HasFriendT<int>
{
...
    friend void counts<int>();
    friend void report<>(HasFriendT<int> &);
};
```

其中一个特化是基于 `TT` 的（变为 `int`），另一个是基于 `HasFriendT<TT>` 的（变为 `HasFriendT<int>`）。因此，模板特化 `counts<int>()` 和 `report<HasFriendT<int>>()` 被声明为 `HasFriendT<int>` own友元。

程序必须的第三个要求是为友元提供模板定义。列表 14.23 说明了这三个方面。注意，列表 14.22 有一个对所有 `HasFriend` 类都是友元的 `count()`，而列表 14.23 有两个 `count()`，其中一个是每个实例化类的友元。由于 `count()` 函数没有可以供编译器推断出所需特化版本的参数，因此这些调用使用了 `count<int>()` 和 `count<double>()` 形式来指示特化。然而，对于 `report()` 的调用，编译器可以使用 `<>` 相同的效果：

```cpp
report<HasFriendT<int>> (hfi2); // 等同于 report(hfi2)
```

列表 14.23 tmp2.cpp

```cpp
// tmp2.cpp -- 模板类的模板友元
#include <iostream>
using std::cout;
using std::endl;
// 模板原型
template <typename T> void counts();
template <typename T> void report(T &);
// 模板类
template <typename TT>
class HasFriendT {
private:
    TT item;
    static int ct;
public:
    HasFriendT(const TT & i) : item(i) {ct++;}
    ~HasFriendT() {ct--;}
    friend void counts<TT>();
    friend void report(HasFriendT<TT> &);
};
template <typename T>
int HasFriendT<T>::ct = 0;
// 模板友元函数定义
template <typename T>
void counts() {
    cout << "template size: " << sizeof(HasFriendT<T>) << " ";
    cout << "template counts(): " << HasFriendT<T>::ct << endl;
}
template <typename T>
void report(T &T) {
    cout << T.item << endl;
}
int main() {
    counts<int>();
    HasFriendT<int> hf1(10);
    HasFriendT<int> hf2(20);
    HasFriendT<double> hfdb(10.5);
    report(hf1); // 生成 report (HasFriendT<int> &)
    report(hf2); // 生成 report (HasFriendT<int> &)
    report(hfdb); // 生成 report (HasFriendT<double> &)
}
```

## 总结

基类的公有和保护成员将成为派生类的私有成员。

通过保护性继承，基类的公有和保护成员将成为派生类的保护成员。因此，在任何情况下，基类的公共接口都会变成派生类的内部接口。这有时被描述为继承实现而非接口，因为派生对象可以显式地访问基类接口。因此，你不能将派生对象视为基类对象。正因如此，在没有显式类型转换的情况下，基类指针或引用不允许指向派生对象。

你也可以通过开发一个成员本身是对象的类来重用代码。这种方法称为包含、分层或组合，它建模了“拥有”（has）关系，因此通常是优选。然而，私有继承和保护继承的能力略不同。例如，继承允许派生类访问基类的保护成员。它还允许派生类完善继承自基类的虚函数。由于包含不是继承的形式，当你通过包含重用代码时，这些功能都不可用。另一方面，如果你需要给定类的多个对象，则包含更为合适。例如，一个状态类可以包含任何 `Country` 数组。

多重继承（MI）允许你在类设计中为多个类重用代码。私有或保护的多重继承可能会引起名称冲突和多重继承基类的问题。你可以使用类限定符来解决名称歧义，并使用虚基类来避免多重继承基类。然而，使用虚基类为构造函数的初始化列表和解决歧义引入了新的规则。

类模板允许你生成通用的类设计，其中一个类型（通常是成员类型）由类型参数表示。一个典型的模板如下：

```cpp
template <class T>
class Ic {
    T v;
public:
    Ic(const T& val) : v(val) { }
};
```

在这里，`T` 是类型参数，它作为稍后指定的实际类型的占位符。（该参数可以具有任何有效的 C++ 命名，但 `T` 和 `Type` 是常见选择。）你也可以在此语境下使用 `typename` 代替 `class`：

```cpp
template <typename T> // 等同于 template <class T>
class Rev { ... };
```

当声明类对象并指定特定类型时，会生成类定义（实例化）。例如，以下声明会导致编译器生成一个类声明，其中模板中类型参数 `τ` 的每次出现都被替换为类声明中的实际类型 `short`：

```cpp
class Ic<short> sic; // 隐式实例化
```

在这种情况下，类名是 `Ic<short>` 而不是 `Ic`。`Ic<short>` 被模板的*特化*。特别是隐式实例化。

当你使用关键字 `template` 类的特定特化时，会发生显式实例化：

```cpp
template Ic<int>; // 显式实例化
```

在这种情况下，编译器使用通用模板生成一个隐式特化 `Ic<int>`，即使尚未请求该类的任何对象。

你可以提供显式特化，即覆盖模板定义的特化类声明。你只需要从 `template<>` 开始定义该类，然后使用模板类名，后跟包含你想要特化的类型的角括号。例如，你可以如下为字符指针提供一个特化的 `Ic` 类：

```cpp
template <> Ic<char*>;
{
    char * str;
public:
    Ic(const char * s) : str(s) { }
}
```

然后，如下形式的声明将使用特化定义 `chic` 而不是使用通用模板：

```cpp
class Ic<char*> chic;
```

模板可以指定多个泛型类型，还可以有非类型参数：

```cpp
template <class T, class TT, int n>
class Pals {...};
```

以下声明将使用 `double` 作为 `T`，`string` 作为 `TT`，`6` 作为 `n` 生成隐式实例化：

```cpp
Pals<double, string, 6> mix;
```

类模板还可以具有作为模板的参数：

```cpp
template <typename T> class CL, typename U, int z
class Trophy {...};
```

在这里，`z` 代表一个 `int` 值，`U` 代表类型的名称，`CL` 代表使用 `template <typename T>` 声明的类模板。

类模板可以部分特化：

```cpp
template <class T> Pals<T, T, 10> {...};
template <class T, class TT> Pals<T, TT, 100> {...};
template <class T, int n> Pals <T, T*, n> {...};
```

这里的第一个创建了一个两个类型都相同且 `n` 值为 6 的特化。同样，第二个创建了 `n` 等于 100 的特化，第三个创建了第二类型为第一种类型指针的特化。

模板类可以是其他类、结构体和模板的成员。

所有这些方法的目的都是允许程序员重用经过测试的代码，而无需手动复制。这简化了编程任务并使程序更加可靠。

# 章节复习

- 1. 对于以下每组类，指出对于类 B 而言公有继承还是私有继承更合适：

| A | B |
| :--- | :--- |
| class Bear | class PolarBear |
| class Kitchen | class Home |
| class Person | class Programmer |
| class Person | class HorseAnd |
| class Automobile | class Driver |

- 2. 假设你有以下定义：

```cpp
class Frabous {
private:
  char fab[20];
public:
  Frabous(const char * s = "C++") : fab(s) { }
  virtual void tell();
};
class Gloam {
private:
  int glip;
public:
  Gloam(int g = 0, const char * s = "C++");
  void tell(int & f);
};
```

给定 Gloam 的 `tell()` 方法应显示 `glip`，提供这些方法的定义。

- 3. 假设你有：

```cpp
Stack sw;
```

写出将生成的类声明。

- 4. 使用本章模板定义以下：

- 一个字符串数组

- 一个 double 栈

- 一个 Worker 对象的数组

- 5. 描述虚类和非虚类的区别。

# 编程练习

- 1. Wine 类有一个字符串对象（见第 4 章）用于存储名称，以及一个包含 `varray<int>`（本章讨论）的 `Pair` 对象。每个 Pair 的第一个成员持有年份，第二个成员持有相应年份的瓶数。例如，第一个变长数组对象可能持有 1988、1992 和 1996 年，而第二个数组对象可能持有 24、48 和 144 瓶。Wine 有一个存储年份数量的 `int` 成员可能会很方便。一些别名可能简化代码：

```cpp
typedef std::var<int> ArrayInt;
typedef Pair<ArrayInt, int> PairArray;
```

因此，`PairArray` 类型代表 `Pair<varray<int>, int>`。使用包含实现 Wine 类。该类应有一个默认构造函数和至少以下构造函数：

```cpp
// 初始化标签为 1，数量为 y，
// 年份为 yr[]，瓶数为 bot[]
Wine(const char * 1, int yr[], const int bot[]);
// 初始化标签为 1，数量为 y，
// 创建长度为 y 的数组
Wine(const char * 1, int yr);
```

Wine 类应该有一个 `GetBottles()` 方法，给定具有 y 年份的 Wine 对象，提示用户输入相应的年份和瓶数。`Label()` 方法返回名称的引用。`sum()` 方法应返回 Pair 对象中第二个 `varray<int>` 对象的瓶数总和。

程序应提示用户输入葡萄酒名称、数量以及每个数组元素的年份和瓶数信息。程序应使用这些数据构造一个 Wine 对象并显示存储在对象的信息。为了指导，这里有一个示例程序：

```cpp
// pel4-1.cpp -- 使用包含关系的 Wine 类
#include <iostream>
#include "wine.h"

int main ( void )
{
    using std::cin;
    using std::cout;
    using std::endl;

    cout << "
```

# 第14 章 在 C++ 中重用代码
