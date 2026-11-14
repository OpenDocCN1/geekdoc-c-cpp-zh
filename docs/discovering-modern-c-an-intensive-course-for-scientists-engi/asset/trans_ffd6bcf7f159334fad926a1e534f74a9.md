
让我们直接进入主题，从一个具有挑战性的示例开始。为了简洁，我们选择短名称：c1 和 c2 用于包含类的命名空间，f1 和 f2 用于包含调用函数的命名空间：

```cpp
namespace c1 {
    namespace c2 {
        struct cc {};
        void f(const cc& o) {}
    } // namespace c2
    void f(const c2::cc& o) {}
} // namespace c1

void f(const c1::c2::cc& o) {}
```

```cpp
namespace f1 {
    void f(const c1::c2::cc& o) {}
    namespace f2 {
        void f(const c1::c2::cc& o) {}
        void g()
        {
            c1::c2::cc o;
            f(o);
        }
    } // namespace f2
} // namespace f1
```

现在来个刁钻的问题：在 f1::f2::g 中调用的是哪个 f？让我们先逐一查看每个重载：

- c1::c2::f：通过 ADL 是候选项；
- c1::f：不是候选项，因为 ADL 不会考虑外部命名空间；
- f：在 g 的外部命名空间中，但被 f1::f2::f 隐藏；
- f1::f：与 f 相同；以及
- f1::f2::f：是候选项，因为它与 f1::f2::g 在同一命名空间中。

至少，我们可以排除五个重载中的三个，只剩下 c1::c2::f 和 f1::f2::f。剩下的问题是哪个重载优先。答案是没有；程序是歧义的。

现在我们可以对这五个重载的子集进行一些推演。首先，我们可以舍弃 c1::f；反正它也无关紧要。如果我们也省略 c1::c2::f 会怎样？那么情况就很清楚了：将调用 f1::f2::f。如果保留 c1::c2::f 并移除 f1::f2::f 呢？情况将是歧义的：在 c1::c2::f 和 c1::f 之间，现在哪个是可见的？到目前为止，所有重载都有相同的参数类型。让我们考虑全局 f 接受非常量引用的场景：

```cpp
void f(c1::c2::cc& o) {}
```

```cpp
namespace f1 {
    void f(const c1::c2::cc& o) {}
    namespace f2 {
        void f(const c1::c2::cc& o) {}
        void g()
        {
            c1::c2::cc o;
            f(o);
        }
    } // namespace f2
} // namespace f1
```

无论重载解析如何，全局 f 都是最佳匹配。然而，它仍然被 f1::f2::f 隐藏：尽管签名不同。事实上，任何名为 f 的东西（类、命名空间）都会隐藏函数 f。

### 名称隐藏

任何来自外部命名空间的项目（函数、类、typedef），只要在内部命名空间中使用了相同的名称，就不可见——即使是完全不同的东西。

为了让 g 可见全局 f，我们可以应用 using 声明：

```cpp
void f(c1::c2::cc& o) {}

namespace f1 {
    void f(const c1::c2::cc& o) {}
    namespace f2 {
        void f(const c1::c2::cc& o) {}
        using ::f;
        void g()
        {
            c1::c2::cc o;
            f(o);
        }
    } // namespace f2
} // namespace f1
```

现在，c1::c2 和全局命名空间中的函数对 g 都可见；并且全局 f 是最佳匹配，因为使用了非常量引用。

以下情况是否无歧义？如果是，将选择哪些 f 的重载？

```cpp
namespace c1 {
namespace c2 {
struct cc {};
void f(cc& o) {} // #1
} // namespace c2
} // namespace c1
void f(c1::c2::cc& o) {}
namespace f1 {
namespace f2 {
    void f(const c1::c2::cc& o) {} // #2
```

## A.6 模板细节

```cpp
void g()
{
    c1::c2::cc o;
    const c1::c2::cc c(o);
    f(o);
    f(c);
}
} // namespace f2
} // namespace f1
void f(c1::c2::cc& o) {} // #3
```

对于 const 对象 c，只有重载 #2 可接受且可见。好了，这就结束了。对于可变对象 o，我们需要仔细看一下。f 的最后一个重载（f #3）定义在 g 之后，因此在 g 中不可见。全局函数 f 被 #2 隐藏。因此只剩下 #1 和 #2，其中前者是更好的匹配（无需隐式转换为 const）。

总结一下，确定调用哪个函数重载的一般策略包含三个步骤：

1. 查找调用之前定义的所有重载
   - 在调用者的命名空间中；
   - 在其父命名空间中；
   - 在参数的命名空间中（ADL）；
   - 在导入的命名空间中（using 指令）；以及
   - 通过导入的名称（using 声明）。

   如果此集合为空，程序将无法编译。

2. 消除隐藏的重载。

3. 在可用重载中选择最佳匹配。如果这是歧义的，程序将无法编译。

本小节的示例无疑有些乏味，但正如 Monk 所说：“你以后会感谢我的。”好消息是：在你未来的程序员生涯中，情况很少会像我们编造的示例那样糟糕。

### A.6.3 针对特定硬件的特化

说到平台特定的汇编技巧，也许我们渴望贡献通过并行执行两个计算来探索 SSE 单元的代码。这可能如下所示：

```cpp
template <typename Base, typename Exponent>
Base inline power(const Base& x, const Exponent) { ... }

#ifdef SSE_FOR_TRYPTICHON_WQ_OMICRON_LXXXVI_SUPPORTED
std::pair<double> inline power(std::pair<double> x, double y)
{
    asm ("
    # Yo, I'm the greatest geek under the sun!
```

```cpp
movapd xmm6, x
...
")
return whatever;
}
#endif
#ifdef ... more hacks ...
```

关于这段代码片段有什么可说的？如果你不喜欢编写这样的特化（从技术上讲是一个重载），我们不责备你。但如果我们这样做，必须将此类技巧放入条件编译中。我们还必须确保构建系统仅在确定是支持汇编代码的平台时才启用宏。对于不支持的情况，我们必须保证泛型实现或另一个重载可以处理 double 对。否则，我们将无法在可移植应用程序中调用特化实现。

标准 C++ 允许我们在程序中插入汇编代码。这看起来就像调用一个名为 asm 的函数，并将字符串字面量作为参数。该字符串的内容，即汇编代码，当然是平台相关的。

在科学应用中使用汇编应该经过深思熟虑。在大多数情况下，收益无法证明所付出的努力和缺点是合理的。测试正确性甚至兼容性可能更加费力且容易出错。作者曾有过这样的经验：一个 C++ 库在 Linux 上运行顺畅，但在 Visual Studio 上由于汇编中的激进调优而几乎无法使用。说了这么多，当我们开始使用汇编片段调优性能时，这不仅会大幅增加开发和维护成本，而且在开源领域还可能失去用户对我们软件的信任。

### A.6.4 可变参数二进制 I/O

A.2.7 节给出了一个二进制 I/O 的示例。它包含重复的指针强制转换和 sizeof。使用类型推导和可变参数函数等语言特性，我们可以提供一个更方便的接口：

```cpp
inline void write_data(std::ostream&) {}
```

```cpp
template <typename T, typename ...P>
inline void write_data(std::ostream& os, const T& t, const P& ...p)
{
    os.write(reinterpret_cast<const char *>(&t), sizeof t);
    write_data(os, p...);
}
```

```cpp
inline void read_data(std::istream&) {}
```

```cpp
template <typename T, typename ...P>
inline void read_data(std::istream& is, T& t, P& ...p)
{
    is.read(reinterpret_cast<char *>(&t), sizeof t);
    read_data(is, p...);
}

int main(int argc, char* argv[])
{
    std::ofstream outfile("fb.txt", ios::binary);
    double o1 = 5.2, o2 = 6.2;
    write_data(outfile, o1, o2);
    outfile.close();

    std::ifstream infile("fb.txt", ios::binary);
    double i1, i2;
    read_data(infile, i1, i2);
    std::cout << "i1 = " << i1 << ", i2 = " << i2 << "\n";
}
```

这些可变参数函数允许我们在每次函数调用中写入或读取任意数量的自包含对象。可变参数模板的全部威力在与元编程（第 5 章）结合时才能释放。

## A.7 在 C++03 中使用 std::vector

以下程序展示了如何在 C++03 中实现 4.1.3.1 节中的 vector 用法：

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main ()
{
    using namespace std;
    vector<int> v;
    v.push_back(3); v.push_back(4);
    v.push_back(7); v.push_back(9);
    vector<int>::iterator it = find(v.begin(), v.end(), 4);
    cout << "After " << *it << " comes " << *(it+1) << "\n";
    v.insert(it + 1, 5); // insert value 5 at pos. 2
    v.erase(v.begin()); // delete entry at pos. 1
    cout << "Size = " << v.size() << ", capacity = "
         << v.capacity() << "\n";
    // The following block emulates shrink_to_fit() in C++11
    {
        vector<int> tmp(v);
        swap(v, tmp);
    }
    v.push_back(7);
    for (vector<int>::iterator it = v.begin(), end = v.end());
}
```
