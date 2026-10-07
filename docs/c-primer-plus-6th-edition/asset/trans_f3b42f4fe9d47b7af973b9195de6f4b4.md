

## TR1

技术报告 1，或 TR1，是 C++ 标准委员会的一个子集的项目。TR1 是与 C++98 标准兼容的库扩展的汇编，这些扩展并非标准所必需。它们是标准下一迭代的候选。TR1 库使 C++ 社区能够测试库组件的价值。然后，当委员会将 TR1 的大部分内容纳入 C++11 时，它处理的都是已知且经过验证的库。

Boost 库为 TR1 贡献了 tuple 模板类、array 模板类、bind 和 function 模板、智能指针（有一些名称和实现上的更改）、static_assert，以及 regex 库。此外，Boost 社区以及 TR1 用户的经验导致了实际的语言更改，例如弃用异常规范，以及添加变参模板，这使得类型类和函数模板的实现更好。

## 使用 Boost

虽然你现在可以作为 C++11 标准的一部分访问许多由 Boost 开发的库，但仍有许多额外的 Boost 库可供探索。例如，Conversion 库中的 lexical_cast 提供了数字类型和字符串类型之间简单的转换。其语法模仿了 dynamic_cast，你将目标类型作为模板参数提供。清单 18.11 显示了一个简单的示例。

### Listing 18.11 lexcast.cpp

```
// lexcast.cpp -- simple cast from float to string
#include <iostream>
#include <string>
#include <boost/lexical_cast.hpp>
int main()
{
    using namespace std;
    cout << "Enter your weight: ";
    float weight;
    cin >> weight;
    string gain = "A 10% increase raises";
    string wt = boost::lexical_cast<string>(weight);
    gain = gain + wt + " to "; // string operator+()
    weight = 1.1 * weight;
    gain = gain + boost::lexical_cast<string>(weight) + " ";
    cout << gain << endl;
    return 0;
}
```

以下是几个示例运行：

Enter your weight: 150
A 10% increase raises 150 to 165.

Enter your weight: 156
A 10% increase raises 156 to 171.600006.

第二个示例运行显示了 lexical_cast 的一个局限性之一；它不提供对浮点格式的控制。要获得该功能，你需要使用第 17 章“输入、输出和文件”中讨论的更复杂的格式化设施。你也可以使用 lexical_cast 将字符串转换为数值。

此前，Boost 还有更多内容。例如，Any 库允许在 STL 容器中存储（恢复）不同类型的异构值和对象集合，使用 Any 模板作为各种值的包装器。

Boost Math 库扩展了标准数学库之外的函数列表。Boost Filesystem 库便于编写在不同文件系统上可移植的代码。你可以参考 Boost 网站（www.boost.org）以获取有关库内容的更多信息以及如何将其添加到各种平台。还有任何 C++ 发行版，例如来自 Cygwin 的发行版，都附带了 Boost 库。

## 现在怎么办？

如果你通读了本书，你应该对 C++ 的规则有很好的掌握。然而，这只是学习这门语言的开始。第二阶段是学习有效使用该语言，而这是一段更长的旅程。最好的阶段是处于工作或学习环境中，让你接触到优秀的 C++ 代码和程序员。而且现在你已经了解了 C++，你可以阅读专注于更高级主题和面向对象编程的书籍。

附录 H，“精选阅读和互联网资源”，列出了其中一些资源。

OOP 的一个承诺是促进大型项目的开发并提高其可靠性。OOP 方法的基本要素之一是发明代表你正在建模的系统（称为问题域）的类。由于实际问题通常很复杂，找到合适的类集可能具有挑战性。从头开始创建复杂系统通常不起作用；相反，最好采取迭代、演进的方法。为此，领域从业者开发了几种技术和策略。特别是，在分析和设计阶段进行尽可能多的迭代和演进，而不是编写和重写实际代码，这一点很重要。

两种常见技术是用例分析和 CRC 卡。在用例分析中，开发团队列出他们期望最终系统被使用的常见方式或场景。在 CRC 卡中，开发团队识别出建议可能类和类特征的元素、操作和职责。使用 CRC（类/职责/协作者）卡是分析此类场景的一种简单方法。开发团队为每个类创建一个索引卡。卡片上包含类名；类职责，作为表示数据执行的动作；以及类协作者，即类交互的其他类。然后团队可以使用 CRC 卡提供的接口遍历一个场景。这可能导致对新类的建议、职责转移等。

## 第 18 章 访问新的 C++ 标准

在更大规模上是用于处理整个项目的系统方法。其中最新的是统一建模语言（UML）。UML 不是编程语言；相反，它是表示编程项目分析和设计的语言。它由 Grady Booch、Jim Rumbaugh 和 Ivar Jacobson 开发，他们是三种早期语言的主要开发者：Booch 方法、OMT（对象建模技术）和 OOSE（面向对象软件工程），UML 是这三种语言的演进继承者，ISO/IEC 于 2005 年将其发布为标准。

除了提高你对 C++ 的整体理解之外，你可能还想学习特定的类库。例如，Microsoft 和 Embaradero 提供了广泛的类库以便于为 Windows 环境编程，而 Apple Xcode 为 Apple 产品（包括 iPhone）提供了类似的设施。

## 摘要

新的 C++ 标准为语言添加了许多功能。其中一些旨在使语言更易于学习和使用。示例包括统一大括号列表初始化、auto 的自动类型推导、类内成员初始化以及基于范围的 for 循环。其他更改扩展并澄清了类设计。这些更改包括默认和已删除方法、委托构造函数、继承构造函数，以及用于澄清虚函数设计的 override final 和 specifies。

Lambda 表达式相对于函数指针和仿函数具有优势。函数模板可用于减少模板实例化的数量。值引用使移动语义成为可能，并允许移动构造函数和移动赋值运算符。

其他更改提供了做事的方式。作用域枚举提供了对枚举的作用域和底层类型的更好控制。unique_ptr 和 shared_ptr 模板提供了处理用 new 分配的内存的更好方法。

模板设计通过添加 decltype、尾随返回类型、模板别名和变参模板而得到增强。

对联合、POD、alignof() 运算符、alignas 说明符和 constexpr 机制的修改规则支持低级编程。

多个库添加，包括新的 STL 类、tuple 模板和 regex 库，为许多常见的编程需求提供了解决方案。

新标准通过 thread_local 关键字和 atomic 库支持并发编程。

总的来说，新标准提高了 C++ 的可用性和可靠性，无论是对新手还是专家。

## 章节回顾

+ 1. 重写以下代码使用大括号初始化列表语法；重写应取消使用数组 ar：
```cpp
class Z200 {
private:
    int j;
    char ch;
    double z;
public:
    Z200(int jv, char chv, double zv) : j(jv), ch(chv), z(zv) {}
};
```
double x = 8.8;
std::string s = "What a bracing effect!";
int k(99);
Z200 zip(200,'Z',0.675);
std::vector<int> ai(5);
int ar[5] = {3, 9, 4, 7, 1};
for (auto pt = ai.begin(), int i = 0; pt != ai.end(); ++pt, ++i)
*pt = ai(i);
```

+ 2. 对于以下简短程序，哪些函数调用是错误以及为什么？对于有效的调用，引用参数指的是什么？
```cpp
#include <iostream>
using namespace std;
double up(double x) { return 2.0* x; }
void r1(const double&rx) { cout << rx << endl; }
void r2(double&rx) { cout << rx << endl; }
void r3(double&rx) { cout << rx << endl; }

int main() {
    double w = 10.0;
    r1(w);
    r1(w+1);
    r1(up(w));
}
```

