

```cpp
bool longer(const std::string& one, const std::string& other)
{
    return one.length() > other.length();
}
```

该程序输出以下结果：

```
Minimum element: 13
Maximum element: 92
Alphabetically last name: Shemp
Longest name: Curly Joe
```

对 findOptimum() 的前两次调用表明，这个函数确实可以用来在给定 vector 中查找最小值和最大值。顺便，我们还展示了一个不同的函数指针，它指向例如 greater<>() 这样的函数模板实例化。你只需在 < 和 > 之间指定所有模板实参，从而显式实例化该模板。

示例的后半部分也许更有趣。如你所知，std::string 的默认比较运算符按字母顺序比较字符串。因此，就像电话簿中一样，Shemp 总是会排在最后。但有时你希望以不同方式比较字符串。在 Ex19_02 中，通过向 findOptimum() 传入指向 longer() 的指针来查找最长字符串，向 findOptimum() 这类函数添加回调参数使这一能力得以实现。

这个示例展示了高阶函数和回调在你与代码重复永无止境的斗争中的巨大价值。如果没有一等函数，仅仅为了让 Ex19_02 工作，你就已经不得不编写至少三个不同的 findOptimum() 函数：findMinimum()、findMaximum() 和 findLongest()。那么这三者都会包含同一个循环，用于从给定 vector 中提取相应的最优值。对初学者而言，至少写几次这样的循环可能是不错的练习，但很快就会变得乏味，而且在专业软件开发中当然没有立足之地。幸运的是，标准库提供了大量类似于 findOptimum() 的泛型算法可供复用，而且它们都接受类似的回调函数，让你可以根据需要调整它们。下一章将更详细地讨论这一点。

> **注意** 一等回调函数的用途远不止作为高阶函数的实参。在日常面向对象编程的其他方面，回调也被积极使用。对象经常将回调函数存储在其成员变量中。回调函数可以有任意多种用途。回调可以构成逻辑中用户可配置的步骤，或向其他对象发出某事件已发生的信号。各种形式的回调促进了许多标准面向对象惯用法，最显著的是经典观察者模式的各种变体。不过，讨论面向对象设计超出了本书范围；有其他优秀书籍专门讨论这个。可以在本章末尾的练习中找到回调成员变量的基本示例。

## 函数指针的类型别名

相信你会同意，定义函数指针变量所需的语法相当可怕。这种语法你写得越少越好。auto 关键字可以提供帮助，但有时你确实想显式指定函数指针的类型。例如，当函数指针用作函数参数或对象的成员变量时。不过，因为“指向函数的指针”就像其他任何类型一样，所以你可以使用 using 关键字为这类类型定义别名（见第 3 章）。

例如，我们不妨看看 Ex19_02 中 findOptimum() 函数模板里回调参数的定义：

```cpp
bool (*compare)(const T&, const T&)
```

不幸的是，这个类型包含模板类型参数 T，这使事情有点复杂。我们暂时简化一下，改为从这个类型模板的一个具体实例化开始：

```cpp
bool (*string_compare)(const std::string&, const std::string&)
```

复制整个变量定义并去掉变量名 string_compare，就得到了这个变量的类型：

```cpp
bool (*)(const std::string&, const std::string&)
```

这个类型可真够长的，因此很值得为它创建别名。使用基于 using 关键字的现代语法，为这个类型定义别名就像这样简单：

```cpp
using StringComparison = bool (*)(const std::string&, const std::string&);
```

这种类似赋值的语法右侧就是匹配的类型名；左侧当然是你选择的名称。有了这个类型别名，声明像 string_compare 这样的参数立刻变得不那么繁琐，可读性也高得多：

```cpp
StringComparison string_compare
```

using 语法用于类型别名的一个好处是，它能优雅地扩展到模板化类型。要为 Ex19_02 的 compare 回调参数的类型定义别名，你只需以最自然的方式泛化 StringComparison 的定义；像往常一样，只需在前面加上 template 关键字，后面跟尖括号中的模板参数列表：

```cpp
template <typename T>
using Comparison = bool (*)(const T&, const T&);
```

这定义了一个别名模板，即生成类型别名的模板。在 optimum 模块中，你可以使用这个模板来简化 findOptimum() 的签名：

```cpp
export template <typename T>
using Comparison = bool (*)(const T&, const T&);
export template <typename T>
const T* findOptimum(const std::vector<T>& values, Comparison<T> compare);
```

当然，别忘了也要从模块中导出别名模板。

导入后，你还可以使用别名模板定义具有具体类型的变量：

```cpp
Comparison<std::string> string_compare{ longer };
```

> **注意**  为便于历史参考，下面是使用旧式 typedef 语法定义 StringComparison 的方式（另见第 3 章）：
>
> ```cpp
> typedef bool (*StringComparison)(const std::string&, const std::string&);
> ```

由于别名不必要地出现在中间，这种语法再次比使用 using 关键字的语法复杂得多。此外，使用 typedef 甚至无法定义别名模板。因此，第 3 章的结论依然成立，而且比以往更加有力：定义类型别名时，应始终使用 using；typedef 在现代 C++ 中没有立足之地。

## 函数对象

就像指向数据值的指针一样，函数指针是 C++ 从 C 编程语言继承而来的低级语言构造。就像原始指针一样，函数指针也有其局限性，而使用面向对象的方法可以克服这些局限。在第 6 章中你了解到，智能指针是对本质上不安全的原始指针的面向对象解决方案。本节介绍一种类似的技术：使用对象作为普通 C 风格函数指针的更强大替代方案。这些对象称为*函数对象*或*仿函数*（这两个术语同义）。与函数指针一样，函数对象的行为完全像函数；但与原始函数指针不同，它是一个完整的类类型对象——拥有自己的成员变量，甚至可能拥有各种其他成员函数。我们将向你展示，因此函数对象比普通 C 风格函数指针强大得多，也更具表现力。

### 基本函数对象

一个*函数对象*或*仿函数*是可以像函数一样被调用的对象。构造它的关键是重载函数调用运算符，第 13 章已简要介绍。为了看看如何做到这一点，我们将定义一个函数对象类，用它封装这个简单的函数：

```cpp
bool less(int one, int other) { return one < other; }
```

快速回顾第 13 章的内容，下面是如何定义带有重载函数调用运算符的类：

```cpp
// Less.cpp - A basic class of functor objects
export module less;

export class Less
{
public:
  bool operator()(int a, int b) const { return a < b; }
};
```

