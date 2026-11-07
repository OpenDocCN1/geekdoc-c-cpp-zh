
- 惰性计算的序列（称为生成器；第18.4节），按需一次产生一个值；⁴
- 无需回调函数的事件驱动编程⁵——例如，模拟、用户界面、服务器、游戏、非阻塞 I/O；⁶
- 协作式多任务；⁷˒⁸
- 结构化并发；⁹
- 响应式流编程；¹⁰ 以及
- 实现状态机。¹¹

## 18.2 协程支持库

协程需要各种支持类，这些类具有大量成员函数和嵌套类型。自行创建这些类既繁琐、复杂又容易出错。C++20 标准库只包含库作者构建协程支持库所需的底层原语。曾参与多个此类库开发的 Lewis Baker 说，这些原语“可以被视为协程的底层汇编语言。”¹² 大多数开发者会更愿意使用协程支持库。标准库的协程支持预计将在 C++23 中提供。¹³˒¹⁴

在此期间，开源社区已经创建了几个非标准的实验性协程支持库。以下是我们为本次演示考虑的库：

- Lewis Baker 的 **cppcoro**[^15] 在许多书籍、视频和博客文章中经常被提及，但已不再受支持。[^16]
- Facebook 的 **folly::coro** 是其广受欢迎的大型开源 C++ 实用工具库 **folly** 的一个子集。[^17] Lewis Baker 是负责 **folly::coro** 的 Facebook 团队成员。该库的文档表明 **folly::coro** 是实验性的。遗憾的是，**folly::coro** 不能脱离 **folly** 独立安装。
- David Haim 的 **concurrencpp**[^18] 正在积极维护。该库使你能够使用 **co_await**、**co_return** 和 **co_yield** 方便地开发协程。
- Sy Brand 的 **generator**[^19] 是一个仅头文件的库，用于开发通过 **co_yield** 一次返回一个值的协程。生成器协程**按需**产生值，这称为惰性求值。这与贪婪求值形成对比——例如，`std::ranges::generate` 算法（第14.4.1节）会立即生成值并将它们放入一个范围，例如 vector。对于大量元素，创建范围可能占用大量内存和时间。如果程序不需要一次性获取所有值，生成器可以减少程序的内存消耗并提高性能。生成器还可以定义无限序列，例如斐波那契数列（第18.4节）或质数。[^20]

在我们的协程演示中，我们使用 **concurrencpp** 和 **generator**。[^21] **concurrencpp** 安装简单，维护积极，并且有清晰的文档和许多代码示例。它提供高级并发功能，包括：

- 用于**异步地**执行函数的**任务**，
- 用于调度任务的**执行器**，可能在不同线程中执行这些任务，
- 用于在未来执行任务的**定时器**，以及
- 各种实用函数。

在第18.4节的示例中，我们使用 **generator** 库实现一个斐波那契生成器协程，该协程按需生成序列中的下一个斐波那契值，并通过 **co_yield** 将其返回给调用者。第18.5节的示例介绍 **concurrencpp** 的任务和**执行器**——预计 C++23 中会提供它们各自的标准版本。第18.6节的示例使用这些来实现一个演示 **co_await** 和 **co_return** 的协程。

## 18.3 安装 concurrencpp 和 generator 库

### concurrencpp 库

要安装 **concurrencpp**，请按照以下地址中针对你平台的说明操作：

https://github.com/David-Haim/concurrencpp#building-installing-and-testing

如果你使用的是 Visual C++，请执行以下附加步骤：

1. 从该库的 `concurrencpp\build\lib` 中打开 `concurrencpp.sln`，并生成解决方案以生成库文件。
2. 在将使用 **concurrencpp** 的 Visual Studio 解决方案中，按照第3.14节中的说明，将 `concurrencpp\include` 文件夹添加到头文件包含路径中。
3. 接下来，选择 **文件 > 添加 > 现有项目...**，导航到 **concurrencpp** 库的 `concurrencpp\build\lib` 文件夹，并将 `concurrencpp.vcxproj` 添加到你的解决方案中。
4. 最后，右键单击你的项目，选择 **添加 > 引用...**，然后在**添加引用**对话框中，勾选 concurrencpp 项目并单击**确定**。

### generator 库

你可以直接从以下地址下载仅头文件的 **generator** 库：

https://github.com/TartanLlama/generator

并将其包含到你的项目中。如果你愿意，也可以克隆该 GitHub 仓库，然后将该库的 include 文件夹添加到编译器的头文件包含路径中。

## 18.4 使用 co_yield 和 generator 库创建生成器协程

生成器是一种按需产生值的协程。当你调用生成器时，它使用 `co_yield` 表达式来**暂停其执行，并将下一个生成的值返回**给调用者。生成器支持预计将成为 C++23 标准库的一部分。对于此示例，我们将使用 **generator** 库。它的 `tl::generator` 类模板使你能够指定生成器协程的返回类型。它提供了使 `co_yield` 能够将值返回给生成器协程调用者的机制。

图18.1定义了一个生成斐波那契数列的生成器协程

0, 1, 1, 2, 3, 5, 8, 13, 21, …

该数列以0和1开始，并且具有如下性质：后续每个斐波那契数都是前两个斐波那契数之和。

- 4. “协程”，访问于2023年4月18日。https://en.cppreference.com/w/cpp/language/coroutines。
- 5. David Mazières，“我对 C++20 协程的教程与看法”，2021年2月。访问于2023年4月18日。https://www.scs.stanford.edu/~dm/blog/c++-coroutines.html。
- 6. Techmunching，“协程及其在 C++ 中的引入”，2020年5月30日。访问于2023年4月18日。https://techmunching.com/coroutines-and-their-introduction-in-c/。
- 7. Rainer Grimm，“C++20：协程的更多细节”，2020年3月27日。访问于2023年4月18日。http://modernescpp.com/index.php/component/content/article/54-blog/c-20/488-c-20-coroutines-more-details。
- 8. Bobby Priambodo，协作式与抢占式：最大化并发能力之探索，2019年9月3日。访问于2023年4月18日。https://medium.com/traveloka-engineering/cooperative-vs-preemptive-to-maximize-concurrency-power-3b10c5a920fe。
- 9. Lewis Baker，“结构化并发：使用协程和算法编写更安全的并发代码”，2019年10月14日。访问于2023年4月18日。https://www.youtube.com/watch?v=IwYySq3s2rg。
- 10. Jeff Thomas，“探索协程”，2021年4月7日。访问于2023年4月18日。https://blog.coffeecode.com/2021/04/exploring-coroutines/。
- 11. Steve Downey，“将状态机转换为 C++20 协程”，2021年6月29日。访问于2023年4月18日。https://www.youtube.com/watch?v=Z8jHi9Cs6Ug。
- 12. Lewis Baker，“C++ 协程：理解运算符 co_await”，2017年11月17日。访问于2023年4月18日。https://lewissbaker.github.io/2017/11/17/understanding-operator-co-await。
- 13. Ville Voutilainen，“大胆提出 C++23 的总体计划”，2019年11月25日。访问于2023年4月18日。http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p0529r4.html。
- 14. “C++23。”访问于2023年4月18日。https://en.wikipedia.org/wiki/C%2B%2B23。
- 15. Lewis Baker，“cppcoro。”访问于2023年4月18日。https://github.com/lewissbaker/cppcoro。
- 16. 在2021年9月18日的一封电子邮件交流中，Baker 先生表示 cppcoro 已不再受支持。他现在从事 Facebook 的实验性 folly::coro 和 libunifex 库的工作。
- 17. “facebook/folly。”访问于2023年4月18日。https://github.com/facebook/folly。
- 18. David Haim，“concurrencpp。”访问于2023年4月18日。https://github.com/David-Haim/concurrencpp。
- 19. Sy Brand（Microsoft 的 C++ 开发者倡导者），“generator。”访问于2023年4月18日。https://github.com/TartanLlama/generator。
- 20. Visual C++ 在其 <experimental/generator> 头文件中提供了 std::experimental::generator 实现。
- 21. 感谢 Anthony Williams（https://www.linkedin.com/in/anthonyjwilliams）——《C++ Concurrency in Action, Second Edition》（https://www.manning.com/books/c-plus-plus-concurrency-in-action-second-edition）的作者——在我们决定如何编写本协程章节时与我们分享他的想法。
