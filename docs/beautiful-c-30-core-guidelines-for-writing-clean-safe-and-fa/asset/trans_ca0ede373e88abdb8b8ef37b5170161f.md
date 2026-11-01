
需要花费时间来决定是否要花费时间去想办法防止它泄漏。养成总是清理自己留下的东西的习惯。

第三，特别是在文件的情况下，在某些操作系统上，如果正在运行的应用程序保持文件打开，用户将无法在程序结束前修改、移动或删除该文件。这可能导致极大的恼怒——有时甚至迫使用户重启机器来删除一个不需要的文件。

最后，不能不加怀疑地认为操作系统会完成所有清理工作。如果你使用的是遗留的第三方库，泄漏资源可能会产生长期后果。请考虑以下片段：

点击此处查看代码图片

```
int open_database(const char*);
void close_database(int);

int main()
{
    auto db =
open_database("//network/customer.db");
}
```

在你的机器的某个远程位置存在一个数据库。这段代码打开了一个连接然后泄漏了它。操作系统不知道如何清理这次泄漏。万幸的话，数据库服务器是一段写得很好的软件，它会分配一个连接，如果连接在超时时间内未使用则关闭连接。但这并不是一个安全的假设。

然而，我们不能特化 std::default_delete，因为 open_database 没有返回指针。你可能会想用 reinterpret_cast 把 int 转换成指针，但那样在代码评审时你会得到一个严厉的注视，因为你是在公然对编译器撒谎。正确的解决方案是创建一个代理，像这样：

点击此处查看代码图片

```
#include <memory>

int open_database(const char*);
void close_database(int);

struct DATABASE_PROXY {
    DATABASE_PROXY(int db_) : db(db_) {}
    operator int() { return db; }
    int db;
};

template <>
struct std::default_delete<DATABASE_PROXY> {
    void operator()(DATABASE_PROXY* p) {
close_database(*p); }
};

int main()
{
    auto db = std::unique_ptr<DATABASE_PROXY>
        (new
DATABASE_PROXY(open_database("//network/customer.db")));
}
```

DATABASE_PROXY 类包装了返回的值，允许你从自由存储区分配一个副本并将其传递给 std::unique_ptr 构造函数。这对于比 int 更大的对象也适用，尽管如果一个结构体是从函数返回的，人们希望其适当资源管理会在其设计中作为一部分进行。

前三个类对于单个作用域内的 RAII 很有用。如果一个函数异常地长，退出作用域的方式可能有很多，这些类确保无论如何退出作用域，清理工作都可以进行。如果你想区分异常退出和成功退出，这个选项在 std::experimental::scope_fail 和 std::experimental::scope_success 中可用。例如：

点击此处查看代码图片

```
void grow(vector<int>& v) {
    std::experimental::scope_success guard([]{
        std::cout << "Good!" << std::endl; });
    v.resize(1024);
}
```

从这个函数中存在两种退出方式：要么 v.resize(1024) 成功，要么它抛出异常。std::experimental::scope_success 对象只有在 resize 成功时才会向标准输出写入内容。

std::experimental::unique_resource² 与 std::unique_ptr 非常相似。然而，与 std::unique_ptr 不同，std::experimental::unique_resource 不要求资源是一个指针。

2. std::experimental 命名空间用于存放 C++ 标准委员会批准的实验性特性。诞生于此的实体如果获得足够积极的反馈，可能会进入 std 命名空间。

重新审视 std::fopen 示例：

点击此处查看代码图片

```
#include <experimental/scope>
#include <cstdio>

int main()
{
```

```
using std::experimental::unique_resource;
auto file = unique_resource(
    std::fopen("output.txt", "r"),
    [](auto fp){ std::fclose(fp); });
}
```

这里有一个问题：万一 std::fopen 失败了怎么办？我们需要一种方法来表示 std::fopen 的结果的无效值，或者实际上是我们想要以这种方式包装的任何资源。

还有一个与 std::make_unique 函数模板类似的模拟，其函数签名有点冗长：

点击此处查看代码图片

```
template <class R, class D, class S=decay_t<R>>
std::experimental::unique_resource<decay_t<R>,
decay_t<D>>
    std::experimental::make_unique_resource_checked
        (R&& resource, const S& invalid, D&& d)

noexcept(std::is_nothrow_constructible_v<decay_t<R>, R> &&

std::is_nothrow_constructible_v<decay_t<D>, D>);
```

这是一个函数模板，它接受一个资源类型、资源类型的无效值以及一个析构函数对象，返回一个 std::experimental::unique_resource 对象。如果资源与无效值匹配，则析构函数对象将不会被调用。

以下是我们如何重写 std::fopen 示例：

点击此处查看代码图片

```
#include <experimental/scope>
#include <cstdio>
```

```
int main()
{
    auto file =
    std::experimental::make_unique_resource_checked(

    std::fopen("potentially_nonexistent_file.txt",
    "r"),
        nullptr,
        [](auto fptr){ std::fclose(fptr); });
}
```

逐步分析这个示例，我们调用 std::experimental::make_unique_resource_checked 并传入 std::fopen 的结果，意图是在文件成功打开时调用 std::fclose。如果 std::fopen 返回的值为 nullptr，则会避免调用 std::fclose。

## 你可以在哪里获得它？

这些是工具箱中非常有用的工具。不幸的是，它们不一定由你的实现厂商提供。我偏好的厂商不提供 <experimental/scope>，尽管实验目录中有一些条目。

这并不能阻止你自己实现它。完整的规范在技术规范中提供，该规范链接在之前的脚注中。搜索 [scopeguard]；方括号中的标签被称为稳定索引。在那里你会找到这些四个类和非成员函数应该如何工作的完整规范。阅读它应该不到 15 分钟。实现它所需的时间比你想象的要少。

自己实现它有三个好处。首要好处是你现在就可以开始使用这些对象，如果它们被采纳进标准，而这很可能发生，你只需要对你的源代码做最小的改动。

其次的好处是你将开始学习标准是如何指定的，以及如何实现库特性。第三个好处是如果你在技术规范中遇到任何错误或歧义，你可以将这些信息反馈给编辑，使他们能够在它被采纳进标准之前进行修复。一旦某物进入标准，修复它就非常困难。当然，最好在部署之前提前发现所有错误。

最后，如果你认为这是对语言的有用补充，你应该让委员会知道并请他们优先将其纳入。如果认为这是过度设计、过于繁琐、不必要或不值得进入标准，你也可以通过写一篇论文阐述你的论点来让委员会知道。委员会由来自许多国家和公司的代表组成，他们自愿花费时间改进 C++ 标准。他们在合理辩论可取性、可行性和达成共识的范围内，做全世界要求他们做的事情，以提供支持 C++ 社区需求的 C++ 标准。请注意进展可能非常缓慢：让来自数十家公司、行业和国家的上百人达成一致是一个缓慢的过程。

必须强调这项工作的自愿性质。没有会员测试，没有私人邀请，没有秘密握手：参与仅仅是通过参加委员会会议并帮助推进流程来实现的。行为准则规范了所有行为并保持程序开放透明。

有几种参与途径。就我而言，作为英国居民，我联系了英国标准协会并请求加入 BSI C++ 小组的信息。 （在加拿大，Kate 居住的地方，你联系的是加拿大标准委员会。在美国是 INCITS。）每个国家都有自己国家标准发展组织（SDO）的名称，以及自己的成本结构，有些参与是免费的，有些收取会员费。你可能能够联系你自己的标准机构进行咨询。即使你不想完全参与，你也应该能够向你的国家机构表达你的观点。

并非世界上的每个国家都在 C++ 委员会中代表，但新的国家总是受欢迎的，正式参与可以由任何准备好与其本国标准机构接触的人发起和进行。有时一个人就可以带来

