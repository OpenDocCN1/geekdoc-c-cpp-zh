
是 baseDMA 类的友元。下一个问题在于，友元不是成员函数，因此不能用作用域解析运算符来指明要使用哪个函数。这个问题的解决办法是使用类型转换，以便原型匹配能够选中正确的函数。因此，代码把类型为 `const hasDMA &` 的参数强制转换为类型为 `const baseDMA &` 的实参：

```cpp
std::ostream & operator<<(std::ostream & os, const hasDMA & hs)
{
// use type cast to match operator<<(ostream & , const baseDMA &)
os << (const baseDMA &) hs;
os << "Style: " << hs.style << endl;
return os;
}
```

程序清单 13.16 在一个简短程序中测试了 baseDMA、lacksDMA 和 hasDMA 类。

## 程序清单 13.16 `usedma.cpp`

```cpp
// usedma.cpp -- inheritance, friends, and DMA
// compile with dma.cpp
#include <iostream>
#include "dma.h"
int main()
{
    using std::cout;
    using std::endl;

    baseDMA shirt("Portabelly", 8);
    lacksDMA balloon("red", "Blimpo", 4);
    hasDMA map("Mercator", "Buffalo Keys", 5);
    cout << "Displaying baseDMA object:\n";
    cout << shirt << endl;
    cout << "Displaying lacksDMA object:\n";
    cout << balloon << endl;
    cout << "Displaying hasDMA object:\n";
    cout << map << endl;
    lacksDMA balloon2(balloon);
    cout << "Result of lacksDMA copy:\n";
    cout << balloon2 << endl;
    hasDMA map2;
    map2 = map;
    cout << "Result of hasDMA assignment:\n";
    cout << map2 << endl;
    return 0;
}
```

下面是程序清单 13.14、13.15 和 13.16 中程序的输出：

```
Displaying baseDMA object:
Label: Portabelly
Rating: 8

Displaying lacksDMA object:
Label: Blimpo
Rating: 4
Color: red

Displaying hasDMA object:
Label: Buffalo Keys
Rating: 5
Style: Mercator

Result of lacksDMA copy:
Label: Blimpo
Rating: 4
Color: red

Result of hasDMA assignment:
Label: Buffalo Keys
Rating: 5
Style: Mercator
```

## 类设计回顾

C++ 可以应用于各种各样的编程问题，而你不能把类设计简化成某种按数字填色式的固定套路。不过，有些指导原则经常适用，现在正是通过回顾并扩充前面讨论来温习这些原则的好时机。

## 编译器为你生成的成员函数

正如第 12 章首次讨论的那样，编译器会自动生成某些公有成员函数，称为*特殊成员函数*。编译器这样做这一事实表明，这些特殊成员函数特别重要。现在让我们再次看看其中一些函数。

## 默认构造函数

默认构造函数是没有参数的构造函数，或者是所有参数都有默认实参的构造函数。如果你不定义任何构造函数，编译器会为你定义一个默认构造函数。它的存在使你能够创建对象。例如，假设 *Star* 是一个类。要使用下面的代码，就需要一个默认构造函数：

```cpp
Star rigel;        // create an object without explicit initialization
Star pleiades[6];  // create an array of objects
```

自动默认构造函数还会做一件事：为任何基类以及任何本身是另一个类对象的成员调用默认构造函数。

另外，如果你编写派生类构造函数时没有在成员初始化列表中显式调用基类构造函数，编译器会使用基类默认构造函数来构造新对象的基类部分。如果没有基类默认构造函数，在这种情况下就会遇到编译时错误。

如果你定义了任何一种构造函数，编译器就不会为你定义默认构造函数。在这种情况下，如果需要默认构造函数，就由你提供。

注意，拥有构造函数的一个动机是确保对象始终得到正确初始化。另外，如果类有任何指针成员，它们当然应该被初始化。因此，最好提供一个显式默认构造函数，把所有类数据成员初始化为合理的值。

## 复制构造函数

类的复制构造函数是接受该类类型对象作为实参的构造函数。通常，声明的参数是对该类类型的常量引用。例如，Star 类的复制构造函数会有如下原型：

```cpp
Star(const Star &);
```

类复制构造函数用于以下情形：

- 当新对象被初始化为同一类的对象时
- 当对象按值传递给函数时
- 当函数按值返回对象时
- 当编译器生成临时对象时

如果程序不使用复制构造函数（无论显式还是隐式），编译器会提供一个原型，但不提供函数定义。否则，程序会定义一个执行逐成员初始化的复制构造函数。也就是说，新对象的每个成员都被初始化为原对象对应成员的值。如果某个成员本身是类对象，那么逐成员初始化会使用为该特定类定义的复制构造函数。

在某些情况下，逐成员初始化并不可取。例如，用 new 初始化的成员指针通常要求你实施深复制，就像 baseDMA 类示例那样。或者，类可能有一个需要修改的静态变量。在这些情况下，你需要定义自己的复制构造函数。

## 赋值运算符

默认赋值运算符处理将一个对象赋值给同一类的另一个对象。不要把赋值和初始化混淆。如果一条语句创建新对象，它使用的是初始化；如果一条语句改变现有对象的值，它就是赋值。

```cpp
Star sirius;
Star alpha = sirius;    // initialization (one notation)
Star dogstar;
dogstar = sirius;        // assignment
```

默认赋值使用逐成员赋值。如果某个成员本身是类对象，那么默认逐成员赋值会使用为该特定类定义的赋值运算符。如果你需要显式定义复制构造函数，那么出于同样的原因，你也需要显式定义赋值运算符。Star 类赋值运算符的原型如下：

```cpp
Star & Star::operator=(const Star &);
```

注意，赋值运算符函数返回对 Star 对象的引用。baseDMA 类展示了显式赋值运算符函数的典型示例。编译器不会生成用于将一种类型赋值给另一种类型的赋值运算符。假设你希望能够把一个字符串赋值给 Star 对象。一种方法是显式定义这样的运算符：

```cpp
Star & Star::operator=(const char *) {...}
```

第二种方法是依靠转换函数（见下一节的“转换注意事项”）把字符串转换为 Star 对象，并使用 Star 到 Star 的赋值函数。第一种方法运行得更快，但需要更多代码。转换函数方法可能导致让编译器困惑的情形。

第 18 章“拜访新的 C++ 标准”讨论了 C++11 新增的另外两个特殊方法：移动构造函数和移动赋值运算符。

## 其他类方法注意事项

定义类时还有几个其他要点需要记住。下面几节列出了其中一些。

## 构造函数注意事项

构造函数与其他类方法不同，因为它们创建新对象，而其他方法由现有对象调用。这是构造函数不被继承的一个原因。继承意味着派生对象可以使用基类方法，但就构造函数而言，对象在构造函数完成其工作之前并不存在。

## 析构函数注意事项

你需要记住定义一个显式析构函数，它删除类构造函数中用 new 分配的任何内存，并处理销毁类对象所需的任何其他特殊簿记工作。如果该类要作为基类使用，那么即使该类不需要析构函数，你也应该提供虚析构函数。
