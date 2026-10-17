
`typedef basic_string<char32_t> u32string; // C++11`

## 第16章 string 类与标准模板库

这允许你使用基于 `wchar_t`、`char16_t` 和 `char32_t` 类型以及 `char` 类型的字符串。只要你的类满足某些要求，你就可以开发某种类似字符的类，并配合 `basic_string` 类模板使用。`traits` 类描述了关于所选字符类型的特定事实，例如如何比较值。`char_traits` 模板针对 `char`、`wchar_t`、`char16_t` 和 `char32_t` 类型有预定义的特化，这些是 `traits` 的默认值。`Allocator` 类表示一个管理内存分配的类。`allocator` 模板针对各种字符类型有预定义的特化版本，这些是默认值。它们使用 `new` 和 `delete`。

## 智能指针模板类

智能指针是一个行为类似于指针但具有额外功能的类对象。在这里我们将查看三个可以帮助管理动态内存分配使用的智能指针模板。让我们先看看可能需要什么以及如何实现。考虑以下函数：

```cpp
void remodel(std::string & str)
{
    std::string * ps = new std::string(str);
    ...
    str = ps;
    return;
}
```

你可能已经看到了它的缺陷。每次调用该函数时，它都会从堆上分配内存，但从不释放内存，从而导致了内存泄漏。你也知道解决方案——只需在 `return` 语句之前添加以下语句，记住释放分配的内存即可：

`delete ps;`

然而，涉及“只需记住”这种短语的解决方案很少是最佳方案。有时你 own忘记。或者你记住了，但不小心删除了或注释了该代码。即使你记住了，仍然可能存在问题。考虑以下变体：

```cpp
void remodel(std::string & str)
{
    std::string * ps = new std::string(str);
    ...
    if (weird_thing())
        throw exception();
    str = *ps;
    delete ps;
    return;
}
```

## 智能指针类

如果抛出异常，`delete` 语句将不会执行，再次导致内存泄漏。你可以像第 14 章“在 C++ 中重用代码”中所示的那样修复这一疏忽，但那不是一个完美的解决方案。让我们思考需要什么。当函数 `remodel()` 终止时，无论是正常终止还是通过抛出异常，局部变量都会从栈中移除——因此指针占用的内存被释放。如果 `ps` 指向的内存也能释放就太好了。因此，`ps` 的问题在于它只是一个普通的指针，而不是具有析构函数的类。如果它是一个对象，它可以删除其指向的内存。这就是 `auto_ptr`、`unique_ptr` 和 `shared_ptr` 背后的思想。`auto_ptr` 模板是 C++98 的解决方案。然而，尽管它已被弃用，但它提供了另外两个作为替代。

这三个智能指针模板（`auto_ptr`、`unique_ptr` 和 `shared_ptr`）各定义了一个类指针的对象，旨在由 `new`（直接或间接地）分配一个地址。当智能指针失效时，它的析构函数会删除内存。因此，如果你将 `new` 返回的地址赋值给这些对象之一，你就不需要释放内存；它将由智能指针对象自动释放。图 16.2 展示了 `auto_ptr` 与普通指针之间的行为差异。`shared_ptr` 和 `unique_ptr` 在这种情况下具有相同的行为。要创建这些智能指针对象之一，你需要包含包含模板定义的内存头文件。然后你使用模板语法来实例化所需的指针类型。例如，`auto_ptr` 模板包含了以下构造函数：

```cpp
template<class X> class auto_ptr {
public:
    explicit auto_ptr(X* p = 0);
    ...
```

## 智能指针模板类

如果列表 16.5 代表了你编程追求的巅峰，那么这三个智能指针中的任何一个都能满足你的需求。但故事背后还有更多内容。

## 智能指针的考虑因素

为什么有三个智能指针？（实际上有四个，但我们不讨论 `weak_ptr`。）为什么 `auto_ptr` 被废弃了？

首先考虑赋值操作：

```
auto_ptr<string> ps (new string("I reigned lonely as a cloud."));
auto_ptr<string> vocation;
vocation = ps;
```

赋值会产生什么结果？如果 `ps` 和 `vocation` 是普通指针，结果将是两个指向同一个字符串对象的指针。这是不可接受的，因为程序将尝试两次删除同一个对象——一次是在 `ps` 过期时，另一次是在 `vocation` 过期时。有方法可以避免这个问题：

- 定义赋值运算符，使其执行深拷贝。这会导致两个指针指向两个不同的对象，其中一个是另一个拷贝。
- 引入*所有权*（ownership）的概念，只允许一个智能指针拥有特定的对象。只有当智能指针拥有对象时，它的析构函数才会删除该对象。赋值则转移所有权。这是 `auto_ptr` 和 `unique_ptr` 使用的策略，尽管 `unique_ptr` 的限制更为严格。
- 创建一种更智能的指针，跟踪有多少个智能指针引用特定对象。这被称为*引用计数*（reference counting）。例如，赋值会将计数加一，指针的过期会使计数减一。当最后一个指针过期时，将调用 `delete`。这就是 `shared_ptr` 的策略。

我们讨论的赋值策略当然也适用于拷贝构造函数。
每个方法都有其用处。列表 16.6 显示了一个 `auto_ptr` 并不适合的示例。

### 列表 16.6 fowl.cpp

```
// fowl.cpp -- auto_ptr 是一个糟糕的选择
#include <iostream>
#include <string>
#include <memory>
int main()
{
    using namespace std;
    auto_ptr<string> films[5] =
```
```
{auto_ptr<string> (new string("Fowl Balls")),
 auto_ptr<string> (new string("Duck Walks")),
 auto_ptr<string> (new string("Chicken Runs")),
 auto_ptr<string> (new string("Turkey Errors")),
 auto_ptr<string> (new string("Goose Eggs"))
}
auto_ptr<string> pwin;
pwin = films[2]; // films[2] 丢失所有权
cout << "The nominees for best avian baseball film film are\n";
for (int i = 0; i < 5; i++)
  cout << *films[i] << endl;
cout << "The winner is " << *pwin << "!\n";
cin.get();
return 0;
```

这里是示例输出：
最佳鸟类棒球电影提名者有：
Fowl Balls
Duck Walks
Segmentation fault (core dumped)

“core dumped”信息应该帮助你在记忆中记住，误用 `auto_ptr` 可能会导致问题。（这类代码的行为是未定义的，因此取决于 `films[2]` 的所有权，你可能会遇到不同的行为）这里是以下语句转移的问题：
`pwin = films[2]; // films[2] 丢失所有权`

这导致 `films[2]` 不再引用该字符串。`auto_ptr` 放弃了对象的所有权，它不再访问该对象。当程序尝试打印 `films[2]` 指向的字符串时，它发现了空指针，这似乎是一个不快的惊喜。

假设你回到列表 16.6 但使用 `shared_ptr` 代替 `auto_ptr`。（你需要一个支持 C++11 `shared_ptr` 类的编译器。）那么程序将正常运行，并给出此输出：
最佳鸟类棒球电影提名者有：
Fowl Balls
Duck Walks
Chicken Runs
Turkey Errors
Goose Eggs
冠军是 Chicken Runs!

# 智能指针模板类 977

你可能在好奇 `unique_ptr` 与 `auto_ptr` 不同，它是如何区分安全和可能不安全的。答案是它使用了 C++11 新增的移动构造函数和右值引用，正如第 18 章讨论的那样。
此外，`unique_ptr` 相比 `auto_ptr` 另一个优势：它有一个与数组配合变体。记住，你必须将 `delete` 与 `new` 配对，将 `delete []` 与 `new []` 配对。`auto_ptr` 模板使用 `delete` 而不是 `delete []`，因此它只能与 `new` 使用，不能与 `new []` 使用。但 `unique_ptr` 有 `new[]` 和 `delete []` 版本：

```
std::unique_ptr<double> _pda(new double(5)); // 将使用 delete
```

## 注意事项

你应该只对通过 `new` 分配的内存使用 `auto_ptr` 或 `shared_ptr` 对象，而不要通过 `new []` 分配的内存。对于不是通过 `new []` 分配的内存（或者对于 `unique_ptr` 来说不是通过 `new` 或 `new []` 分配的内存），你不应该使用 `auto_ptr`、`shared_ptr` 或 `unique_ptr`。

## 选择智能指针

你应该使用哪种指针类型？如果程序对一个对象使用多个指针，`shared_ptr` 是你的首选。例如，你可能有一个指针数组以及一些辅助指针来识别特定元素，如最大值最小值。或者你可能有两种包含同一个对象的对象的类型。或者你可能有一个指针 STL STL。许多 STL 算法包含拷贝或赋值操作，这些操作对 `shared_ptr` 有效，但对 `unique_ptr`无效（你会得到编译器警告）或对 `auto_ptr`无效（你会得到未定义行为）。如果你的编译器没有提供 `shared_ptr`，你可以从 Boost 库获取一个版本。
如果程序不需要指向同一个对象的多个指针，`unique_ptr` 即可工作。它是返回指向由 `new` 分配的内存指针的函数返回类型的良好选择。这样，所有权就转移给了赋值返回值的 `unique_ptr`，并且智能指针承担了调用 `delete` 的责任。你可以将 `unique_ptr` 对象存储在 STL 容器中，只要你不调用像 `sort()` 这样会将 `unique_ptr` 拷贝或赋值给另一个 `unique_ptr` 的方法或算法。例如，假设包含了正确的头文件和 `using` 语句，程序可以使用如下代码片段：

```
unique_ptr<int> make_int(int n)
{
    return unique_ptr<int>(new int(n));
}
void show(unique_ptr<int>& pi) // 按引用传递
{
    cout << *pi << ' ';
}
int main()
{
```
```
vector<unique_ptr<int>> vp(size);
for (int i = 0; i < vp.size(); i++)
  vp[i] = make_int(rand() % 1000); // 拷贝转移 unique_ptr
  vp.push_back(make_int(rand() % 1000)); // 确，因为参数是临时变量
  for_each(vp.begin(), vp.end(), {});    // 使用 for_each()
```

对 `push_back()` 的调用之所以有效，是因为它传递了一个临时 `unique_ptr` 赋值给一个 `unique_ptr`。同样注意，如果 `show` 是按值而非按引用传递对象，`for_each()` 语句将失败，因为那时必须将 `pi` 初始化为 `vp` 中非临时的 `unique_ptr`，这是不允许的。如前所述，编译器会捕获不当使用 `unique_ptr` 的尝试。

在可以将一个 `shared_ptr` 赋值给另一个的相同条件下，你可以将 `unique_ptr` 赋值给 `shared_ptr`——源必须是一个右值。正如之前提到的，在下面的代码中 `make_int()` 是一个返回类型为 `unique_ptr<int>` 的函数：

```
unique_ptr<int> make_int(rand() % 1000); // OK
shared_ptr<int> spp(pup); // 不允许，pup 是左值
shared_ptr<int> spr(make_int(rand() % 1000)); // OK
```

`shared_ptr` 模板包含一个显式构造函数用于将 `unique_ptr` 转换为 `shared_ptr`。`shared_ptr` 接管了之前由 `unique_ptr` 拥有的对象。虽然可以使用 `auto` 代替 `unique_ptr`，但后者更好。如果你的编译器没有提供 `unique_ptr`，你可能考虑 BOOST 库的 `scoped_ptr`，它是类似的。

# 标准模板库

STL 提供了一组代表容器、迭代器、函数对象和算法的模板。容器是一个单元，类似于数组，可以存放多个值。STL 容器是同质的；也就是说它们持有相同类型的值。算法是完成特定任务的配方，例如对数组排序或在列表中查找值。迭代器是你在容器中移动的对象，就像指针允许你遍历数组；它们是指针的泛化。函数对象是可以像函数一样工作的对象；它们可以是类指针或函数指针（包括作为指针的函数名）。STL 允许你构建各种容器，包括数组、队列和列表，让你能够执行各种操作，包括搜索、排序和匹配。

Alex Stepan 和 Meng Lee 在惠尔惠开发了 STL，并于 1994 年发布了实现版本。ISO/ANSI C++ 委员会投票将其作为 C++ 标准的一部分纳入。STL 不是面向对象编程的范。相反，它代表了一种不同的编程范式，称为泛型编程。这使得 STL 在功能和方法上都非常有趣。

# 标准模板库 979

关于 STL 的信息太多，无法在一个章节内介绍，因此我们将查看一些具有代表性的示例并研究泛型编程方法的精神。我们将从几个具体的示例开始。然后当你对比较器、迭代器和算法有了直观的理解，我们将查看底层的设计哲学，然后对整个 STL 进行概述。附录 G，“STL 方法和函数”总结了各种 STL 方法和函数。

# vector 模板类

第 4 章简要地提到了 `vector` 类。现在我们来更仔细地观察它。在计算中，`vector` 一词对应于数组，而不是第 11 章“处理类”中讨论的数学向量。（从数学角度来看，一个 N 维数学向量可以用 N 个分量的集合表示，在这方面，数学向量具有额外的属性，如内积和外积，而计算机向量并不一定具有。）计算风格的 `vector` 持有一组可以随机访问的值。也就是说，你可以使用索引访问 vector 的第 10 个元素，而无需访问第 14 章引入的 `varlay` 和 `ArrayFP` 类的前 9 个元素，以及第 4 章引入的 `array` 类的元素。计算风格的 `vector` 持有一组可以随机访问的值。也就是说，你可以使用索引访问 vector 的第 10 个元素，而无需访问第 14 章引入的 `varlay` 和 `ArrayFP` 类的前 9 个元素，以及第 4 章引入的 `array` 类的元素。计算风格的 `vector` 持有一组可以随机访问的值。也就是说，你可以使用索引访问 vector 的第 10 个元素，而无需访问第 14 章引入的 `varlay` 和 `ArrayFP` 类的前 9 个元素，以及第 4 章引入的 `array` 类的元素。

```
#include vector
```

# 再次提到分配器

像 `string` 类一样，各种 STL 容器模板都接受一个可选的模板参数，指定使用哪个分配器来管理内存。例如，`vector` 模板如下：

`template <class T, class Allocator = allocator<T> > class vector {`

如果你省略了该模板参数，容器模板默认使用 `allocator<T>` 类。该类使用 `new` 和 `delete`。

列表 16.7 在一个需求性程序中使用该类。这个特定的程序创建了 `vector` 对象，一个 `int` 特化和一个 `string` 特化；每个都有五个元素。

# 列表 16.7 vect1.cpp
