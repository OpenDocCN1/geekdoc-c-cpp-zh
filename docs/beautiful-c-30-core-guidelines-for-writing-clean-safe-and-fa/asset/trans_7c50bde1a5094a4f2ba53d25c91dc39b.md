
```cpp
special_cases::special_cases(int a, int b)
: m_mst(f2(a, b))
{}
```

但是除非 f2 还有其他用途，否则你创建了一个专门供构造函数调用的特殊函数。对维护者来说这不是一件好事，而维护者很可能就是未来的你。这正是立即调用 Lambda 表达式，或 IILE 的用例。IILE 是一个简单的惯用法，看起来像这样：

```cpp
special_cases::special_cases(int a, int b)
: m_mst([=](){ // Capture by value, taking no parameters
    int const x = perform_f2_related_checks(a, b);
    int const y = perform_boundary_checks(a, x);
    int const z = perform_initialization_checks(b, y);
    return my_special_type{y, z};
}())            // Immediately invoke the lambda expression
{}
```

我们声明 Lambda 表达式，然后立即调用它。
命名很难，有时候你只能说出自己在做什么，把它变成缩写，然后接受它（另见 RAII）。现在我们的初始化函数集中在了一处。

我们也可以将其应用于另一个示例：

```cpp
int const var = []() {
    if (first_check()) return simple_init();
    return complex_init();
}();
```

用于初始化对象的单一功能片段通常会导致创建临时状态，而该状态的实用性在相关对象的声明之后就会过期。由于临时状态是对象的一个依赖项，因此必须在同一作用域中声明。将它打包到 Lambda 表达式中会创建一个本地作用域，该作用域可以导出一个值。

## Eliminating state

```cpp
void accumulate_mst(std::vector<my_special_type>& vec_mst,
                    std::vector<int> const& source) {
    auto source_it = source.begin();
    while (source_it != source.end()) {
        auto s_it = source_it++;
        my_special_type mst{*s_it, *s_it};
        vec_mst.push_back(mst);
    }
}
```

在 while 循环内部，会构造一个 my_special_type 的实例并将其推入向量。你可以考虑完全避免构造，而是改推回一个右值实例：

```cpp
void accumulate_mst(std::vector<my_special_type>& vec_mst,
                    std::vector<int> const& source) {
    auto source_it = source.begin();
    while (source_it != source.end()) {
        auto s_it = source_it++;
        vec_mst.push_back(my_special_type{*s_it, *s_it});
    }
}
```

在未优化的构建中，这将创建一个临时对象并调用 push_back(my_special_type&&)，从而可以使用移动构造函数而不是拷贝构造函数。但我们可以通过使用 emplace_back 进一步改进：

```cpp
void accumulate_mst(std::vector<my_special_type>& vec_mst,
                    std::vector<int> const& source) {
    auto source_it = source.begin();
    while (source_it != source.end()) {
        auto s_it = source_it++;
        vec_mst.emplace_back(*s_it, *s_it);
    }
}
```

> *在用处处声明可以提高代码的可读性，而完全不声明状态则会进一步改善。推理状态需要全面的记忆，而这随着代码库的扩展会成为一种日益减少的资产。*

我们已经从函数中消除了一些状态。现在，你可能会认为这样做提高了程序的性能。然而，这些函数都做同样的事情，编译器很可能会为每个函数生成相同的汇编代码。在第一个示例中，编译器可以看到 my_special_type 的实例不会超出 while 循环的范围，因此能够调用 push_back(my_special_type&&) 而不是 push_back(my_special_type const&)。在第三个函数中，我们进一步推迟了构造，但这只是移动了拷贝省略位置的情况。对象将只构造一次，在正确的位置，得益于拷贝省略。事实上，emplace_back 比 push_back 更昂贵地编译：它是一个类模板成员函数模板，而不是类模板成员函数。这可能会影响你使用它的决定。

这些示例假设移动构造函数和拷贝构造函数已被默认并且是平凡的。如果没有移动构造函数，或者执行成本很高，那么你可能考虑使用 emplace_back。默认情况下，使用 push_back 并就地构造。

## Summary

你可能会问自己，“嗯，如果它们都生成相同的代码，有什么区别？我为什么要选择其中一个而不是另一个？”答案是，此准则不是关于性能，而是关于维护。在用处处声明可以提高代码的可读性，而完全不声明状态则会进一步改善。推理状态需要全面的记忆，而这随着代码库的扩展会成为一种日益减少的资产。

尽可能晚地推迟声明会带来多项好处。不必要的状态可以减少甚至消除。作用域被最小化。对象不会在初始化之前被使用。可读性得到改善。所有这些加起来会提高安全性，有时还会改善性能特征。我认为这是一条应尽可能遵循的黄金法则。

## Chapter 5.5

### Per.7: Design to enable optimization

### Maximizing the frame rate

我靠做游戏为生。更准确地说，如今我帮助做游戏为生，因为我在一支由数百人组成、拥有不同专业领域的团队中工作。除了动画师、艺术家、音频工程师、QA 和制作人员外，还有一支庞大的工程师团队。

并非一直如此。我在 1980 年代曾独自制作游戏，游戏的生死取决于帧率。在英国，家用电脑会使用家庭 PAL 电视机进行显示，连接到 50Hz 的电网。CRT 显示器在交替帧上产生隔行图像，因此你会希望整个游戏循环在 40 毫秒内运行，每秒产生 25 帧。

这是一个不可动摇的数字，受物理定律或至少家庭供电的限制。我为 Sinclair ZX Spectrum 开发，该机运行在 Z80 处理器上。我知道每条指令执行需要多少微秒。通过仔细记账，我知道在每个块中会扫过多少条扫描线（我不愿使用“函数”这个词）。当我达到 625 时，我就知道时间到了。

当然，任何向美国市场销售的想法都是不可能的。电力供应为 60Hz，但处理器运行速度相同。做事的时间更少，我必须削减功能以实现更高的帧率。高清电视兴起的一个优势是分辨率和帧率的一致性：1920 x 1080 像素，60Hz。不幸的是，随着市场再次在 4K 电视和 HDTV 之间分裂，这一一致性时期已经结束。希望硬件军备竞赛最终会稳定在 4K。

回到 1980 年代的视频游戏开发，优化意味着一件事，而且只有一件事：用更少的空间更快地执行。没有只为速度优化：固定的 RAM 容量意味着循环展开是在拆东墙补西墙。同样，只为大小优化意味着显示一帧所需的时间会增加。

常见的技巧包括手工指定的内联。一旦函数编写并调试完成，你可以自行决定是进行函数调用还是将代码插入调用点。掌握每条指令执行所需的时间以及这种替换将花费多少 RAM，这可以非常精确地找到速度提升。

这种替换与循环展开不同。展开时，循环体会被复制一次或多次以减少返回循环开始处的跳转次数。这当然会占用空间成本。然而，用函数体替换函数调用有时可以节省空间，因为通过简单地复制函数，可以消除调用函数所需保存寄存器的开销。

堆栈操作是特别喜欢的。当处理器遇到调用指令而不是跳转指令时，它会在堆栈上存储程序计数器并将程序计数器更改为调用操作数。当处理器遇到返回指令时，它会将堆栈内容弹出到程序计数器中。虽然这完美地支持单一入口、单一返回的想法，但它可以被巧妙地破坏以创建跳转表。如果你知道一组函数必须按特定顺序执行，你可以按所需执行顺序的逆序将它们的地址压入堆栈然后返回。每个函数都会执行，并“返回”到堆栈中的下一个函数。这是一种宝贵的节省空间的方法，但调试起来非常困难且完全不可移植。

我发现优化是制作游戏最有趣的部分。你可以不断地改进，直到决定已经到达尽头，然后你会宣布你的函数是最优的。优化依赖于对平台的深入而亲密的了解。当我使用 Z80 处理器工作时，我必须知道寄存器加载指令位于 0x40 到 0x7f 之间，条件返回指令从 0xc、0xd、0xe 或 0xf 开始并以 0x0 或 0x8 结束，并且 xor 指令从 0xA8 运行到 0xAF，顺序为 b、c、d、e、h、l、(hl)、a。
