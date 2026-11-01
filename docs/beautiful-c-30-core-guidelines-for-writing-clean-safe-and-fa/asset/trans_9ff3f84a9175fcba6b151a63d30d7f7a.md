
## 第 2.4 章

### C.47：在成员声明的顺序中定义并初始化成员变量

只有一种成员数据的初始化顺序，那就是声明的顺序。你无法改变这一点。这一规则不可更改是有非常好的理由的，我们将在本章中描述。

但首先，举个例子。Bryn 是大型公司的一名新工程师，被要求编写一个人口服务，用于查询建筑物内有多少人。建筑物深处的一个服务器处理入场和离场。它老旧且缓慢。正面用红色字刻着一家早已被人遗忘的硬件公司的名字，该公司很久以前被一家贪婪且资金充足的初创公司收购。查询相当繁琐且耗时。新安全法规要求人数必须即时可用，但由于有人在前台签到大约需要一分钟，因此认为可以安全地查询服务器、缓存该值并保留 30 秒。这样可以防止查询堆积得比处理速度更快。

我知道你在笑。这是真实的故事，虽然我改了名字。Bryn 制作了这个简单的解决方案：

点击此处查看代码图像

```
class population_service {
public:
    population_service(std::string query);
    float population() const;

private:
    mutable float current_population;
    mutable std::time_t expiry;
    std::string query;
};
```

该类使用服务器查询进行构造。对 population 的调用会检查人口值的过期时间，并在必要时使用查询进行更新。这种延迟求值是 mutable 的典型用例。

Bryn 编写了构造函数：

点击此处查看代码图像

```
population_service::population_service(std::string query_)
{
    query = std::move(query_);
    expiry = std::chrono::system_clock::to_time_t(

    std::chrono::system_clock::now());
    current_population = population();
}
```

population 函数很简单。所有测试都通过了，Bryn 将其提交进行代码评审。他被要求将初始化从构造函数体迁移到初始化列表。为了给人留下好印象，Bryn 很快就完成了并制作了这个：

点击此处查看代码图像

```
population_service::population_service(std::string query_)
    : query(std::move(query_))
    , expiry(std::chrono::system_clock::to_time_t(

    std::chrono::system_clock::now()))
    , current_population(population())
{}
```

他提交后，他的负责人 Beth 敲了门。
“Bryn，”她问道，“你测试过吗？”
“嗯，全是绿色，”他天真地回答。
“你在迁移到初始化列表之后测试过吗？”她坚持道。
“嗯，没必要吧？”他回应道。“我只是把所有东西都移到了大括号之前。”
Beth 在内心死了一点。她脑海中正在准备“自动化你的测试并在提交前始终测试”的讲座，以面对这个回答。她不需要运行代码就能看出有问题。

不幸的是，将所有内容移上去改变了代码的行为。现在发生的第一件事是 current_population 通过调用 population 进行初始化。撇开从初始化列表中调用成员函数的 questionable 智慧不谈，这并不是工程师的本意。他希望先初始化 query 和 expiry 时间。在这些值正确初始化之前，对 population 的调用几乎不可能成功。

要绝对明确，成员数据是按照声明的顺序进行初始化的。那是唯一的顺序。没有神奇的选择，也没有任何可供你选择的变体。在这种情况下，current_population 首先被声明，因此它由对成员函数 population 的调用进行初始化。expiry 成员接下来被初始化，但 std::time_t 没有构造函数，通常由内置的整数类型组成，因此它没有被初始化为确定值。最后，query 通过移动构造进行初始化。

有两种方法可以修复这个问题。正确初始化此对象的方法是先将 current_population 初始化为零，将 expiry 初始化为 now()，然后移动构造 query，如下所示：

点击此处查看代码图像

```
population_service::population_service(std::string query_)
  : current_population(0)
  , expiry(std::chrono::system_clock::to_time_t(
std::chrono::system_clock::now()))
, query(std::move(query_))
{}
```

你可以选择在构造函数体中调用 **population**。不过由于它是一个需要缓存的昂贵函数，我们不会在值需要之前调用它。

另一种修复问题的方法是重新排列类定义中的成员数据，如下所示：

[点击此处查看代码图像](#)

```
class population_service {
public:
    population_service(std::string query_);
    float population() const;

private:
    std::string query;
    mutable std::time_t expiry;
    mutable float current_population;
};
```

有了这种排序，**population** 可以安全地在初始化列表中调用，尽管出于同样的原因我不会这样做。

这引出了一个关于类布局和对齐的有趣旁注。考虑这个程序：

[点击此处查看代码图像](#)

```
#include <iostream>
struct int_two_bools {
    bool m_b1;
    int m_i;
    bool m_b2;
};
int main() {
    std::cout << sizeof(int_two_bools);
}
```

你会期望看到什么答案？

我们使用 x64 MSVC 19.28 在 Compiler Explorer 上构建并运行了此程序，得到了答案 12。每个成员占用四个字节。

![](img/1f717ab54347ad0154ca00897b584f1a_129_0.png)

图 2.4.1. 存储整数和两个布尔值的布局

然后我们交换了第二个和第三个成员，如下所示：

点击此处查看代码图像

```
struct int_two_bools {
    bool m_b1;
    bool m_b2;
    int m_i;
};
```

现在你会期望看到什么答案？你可以在 Compiler Explorer 上检查输出并观察答案是 8。

![](img/1f717ab54347ad0154ca00897b584f1a_129_1.png)

图 2.4.2. 存储整数和两个布尔值的优化布局

的确，如果你在 m_b2 之后添加第三个 bool，如下所示：

点击此处查看代码图像

```
struct int_two_bools {
    bool m_b1;
    bool m_b2;
    bool m_b3;
    int m_i;
};
```

你仍然会得到答案 8。

![](img/1f717ab54347ad0154ca00897b584f1a_130_0.png)

图 2.4.3. 存储整数和三个布尔值的优化布局

这可能令人惊讶。标准对对齐有一些说法，你可以在 [basic.align] 中找到。¹ 总之，单个对象必须在其大小匹配的边界上对齐。在此示例中，对于此实现，sizeof(bool) 为 1，sizeof(int) 为 4。在 int_two_bools 的第一个定义中，第一个 bool 成员占用一个字节。然后添加三个字节的填充，以便 int 成员位于四字节边界上。在第二个定义中，两个 bool 成员是连续的，只需在一字节边界上对齐。这意味着在 int 成员之前只需要两个字节的填充。在第三个定义中，只需要一个字节的填充，因为所有三个 bool 成员都可以容纳在四个字节中。

1. https://eel.is/c++draft/basic.align

这表明布局顺序对于类实例的大小很重要。如果你在受限大小的情况下有一百万个对象：那额外的四个字节可能非常宝贵。解决初始化顺序问题可能不如

正确的析构函数。

你现在似乎在随口编造。这个解决方案的问题在于你现在为一个很少使用的功能向类添加了另一个字段。你为每个类引入了运行时的开销。你创建了一个无论是否使用都必须付费的抽象。这违背了语言设计的基本原则之一：不要为你不使用的东西付费。外面的 C++ 代码有数十亿行。如果你在语言中引入此功能，那么你将对数百万个项目产生负面影响。它不会发生。不会有多个析构函数，也不会有可指定的初始化顺序。成员是按照它们声明的顺序初始化的，且仅按该顺序。我们希望这一点很清楚。

在我看来，C++ 的突出特性是确定性析构。外面的语言很多，其中很多会为你管理生命周期。使用 C++ 你决定对象的生命周期何时结束，以及何时释放其所有资源。当自动存储期对象的名称超出作用域时，其析构函数将被调用，并且其成员的析构函数将被调用。当你显式删除动态存储期对象时，其析构函数将被调用，并且其成员的析构函数将被调用。当程序结束时，所有静态存储期对象都按构造的相反顺序销毁：它们的析构函数被调用，并且它们的成员的析构函数被调用。当线程被销毁时，所有线程本地对象实例都按构造的相反顺序销毁：它们的析构函数被调用，并且它们的成员的析构函数被调用。

你可能会觉得我们在这里啰嗦，但这是语言的一个极其宝贵的特性，如果你之前接触过托管生命周期，你会明白为什么。例如，想象你将对数据库的连接存储为对象的成员，并且连接是有限资源。你依赖于在析构函数被调用时关闭该连接。它不应在对象被销毁之前关闭；它只应在确定不再需要时才关闭。这正是析构函数的用途。它是在对象生命周期结束时调用的函数。它保证在作用域退出时被调用，而垃圾回收根本无法做到

