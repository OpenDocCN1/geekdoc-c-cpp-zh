
最后这项测试表明，`RegEx_search()` 函数能在字符串中找到三位数值。显然，当你需要定位信息时，`RegEx_search()` 函数很好用，但当你需要确保信息准确时就不适用了。当你需要精确的模式匹配时，请改用 `RegEx_match()`。

## 使用 Tokenizer 将字符串拆分为标记

人类将字符串视为一个句子，或至少是一个短语。词语的组合创造出我们一眼就能理解的含义。

![](img/128ab511de4e7360e167e3b15cdd5dd0_876_0.png)

另一方面，计算机什么都不理解。计算机可以执行模式匹配和数学运算，但它无法理解吉卜林（想进一步了解这位迷人的作家，请访问 https://www.poetryfoundation.org/poets/rudyard-kipling）。正是因为计算机缺乏理解能力，你必须为计算机对文本进行分词。计算机可以对单个标记（通常是单个词或符号）进行比较，并基于这些比较生成输出。

你使用的编译器依赖分词器（一种将文本拆分为标记的应用程序组件），把你输入的文本转换成计算机可以执行的机器码。然而，分词器出现在各种应用程序中。例如，当你对文档执行拼写检查时，文字处理应用程序会使用分词器将文本拆分为单个词，然后将这些词与其内部词典中的词进行比较。

清单 5-2 所示的 Tokens 示例展示了一种从字符串创建标记的方法。这种基本技术适用于任何短语、字符串或一系列字符串。通常，你会在创建完标记之后处理它们。

### 清单 5-2：从字符串创建标记

```cpp
#include <iostream>
#include "boost/tokenizer.hpp"

using namespace std;
using namespace boost;

int main() {
    string MyString = "This is a test string!";
    tokenizer<> Tokens(MyString);

    // Display each token on screen.
    tokenizer<>::iterator Iterate;
    for (Iterate = Tokens.begin(); Iterate != Tokens.end();
        Iterate++)
        cout << *Iterate << endl;
    return 0;
}
```

tokenizer 模板将 MyString 的分词形式放入 Tokens。应用程序现在有了一组可供处理的标记。要查看这些标记，必须通过创建 tokenizer<>::iterator（即 Iterate）来遍历它们。应用程序使用 Iterate 输出各个标记。运行此应用程序时，你会看到以下输出：

```text
This
is
a
test
string
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_877_0.png)

此示例展示了一个基本例程，几乎可以用于任何需求。不过，你可能需要 tokenizer 类的一些扩展功能。请查看 https://www.boost.org/doc/libs/1_73_0/libs/tokenizer/doc/index.html 上的材料，以获取有关 tokenizer 和 tokenizer<>::iterator 的更多信息。

## 执行数值转换

执行数值转换并不难——难的是执行*准确*的数值转换。在从一种数字类型转换为另一种数字类型时，得到正确结果至关重要。当然，如果你的游戏分数差了一两分，你可能不会太在意；但你肯定会注意到储蓄账户里少了的美元。更糟的是，在太空旅行时，一个舍入误差完全可能毁掉你的一天，让你朝着太阳而不是地球飞去。

Boost 库包含 converter 模板，它使从一种数字类型转换为另一种数字类型相对容易。converter 模板具有各种灵活性。清单 5-3 所示的 Convert 示例展示了 converter 模板的两种不同使用层次。

### 清单 5-3：*（续）*

```cpp
int main() {
    typedef converter<int, double> Double2Int;
    double MyDouble = 2.1;
    int MyInt = Double2Int::convert(MyDouble);

    cout << "The double value is: " << MyDouble << endl;
    cout << "The int value is: " << MyInt << endl;

    // See what happens with a larger value.
    MyDouble = 3.8;
    MyInt = Double2Int::convert(MyDouble);
    cout << "The double value is: " << MyDouble << endl;
    cout << "The int value is: " << MyInt << endl;

    // Round instead of truncate.
    typedef conversion_traits<int, double> Traits;
    typedef converter<int, double, Traits,
        def_overflow_handler, RoundEven<double> >
        Double2Rounded;
    MyInt = Double2Rounded::convert(MyDouble);
    cout << "The int value is: " << MyInt << endl;
    return 0;
}
```

该示例首先创建一个 converter 对象 Double2Int。这个第一个对象展示了你可以提供的最少信息——目标类型（int）和源类型（double）的值。默认设置会截断浮点值（其中包括 float 和 double）以获得 int 值。要执行转换，代码依赖 convert 方法，该方法需要一个所需源类型的变量作为参数。

![](img/128ab511de4e7360e167e3b15cdd5dd0_879_0.png)

converter 模板支持四种舍入方式。你必须使用正确的舍入方式来满足应用程序的要求。想象一下，如果真正需要的是舍入操作，而你却使用了截断，计算会发生什么。下面的列表描述了 converter 支持的全部四种舍入方式：

- Trunc：移除值的小数部分（向 0 舍入）
- RoundEven：根据需要向上或向下舍入值，使最终值为偶数（也称为银行家舍入法）。因此，1.5 向上舍入为 2，而 2.5 向下舍入为 2。

## 使用 Foreach 创建改进的循环

如果你希望应用程序以最佳性能运行，编写高效的循环是一项要求。有趣的是，许多循环都会使用一定量的*样板*代码（即每次编写时本质上相同、但带有细微差别的代码）。

![](img/128ab511de4e7360e167e3b15cdd5dd0_881_0.png)

记住

本书中描述的模板和其他方法提供了一种手段，可以克服编写本质上相同代码的枯燥感。然而，迄今为止的示例都没有展示一种久经考验的方法：宏。*宏*本质上是一种替换技术，它用一个关键字替换你通常编写的样板代码。宏通常以大写形式出现，例如 BOOST_FOREACH，它就是本章这一节使用的宏。你不必键入与某个宏相关的所有代码，只需键入宏名称，编译器就会为你完成其余工作。

![](img/128ab511de4e7360e167e3b15cdd5dd0_881_1.png)

技术内容

BOOST_FOREACH 宏背后的魔力在于，它会创建你通常手工编写的所有迭代代码。换句话说，你并没有向编译器提供更少的代码；你只是让宏替你编写这些代码。Boost 库仍然依赖标准库的 for_each 算法；你避免了在使用该算法时原本要编写的所有代码。有关 BOOST_FOREACH 宏的更多信息，请参见 https://www.boost.org/doc/libs/1_73_0/doc/html/foreach.html。清单 5-4 中的 ForEach 示例展示了如何使用 BOOST_FOREACH 循环遍历一个 vector。

### 清单 5-4 — 创建 BOOST_FOREACH 循环

```cpp
#include <iostream>
#include <vector>
#include "boost/foreach.hpp"

using namespace std;
using namespace boost;

int main() {
    vector<string> names;
    names.push_back("Tom");
    names.push_back("Dick");
    names.push_back("Harry");
    names.push_back("April");
    names.push_back("May");
    names.push_back("June");

    BOOST_FOREACH(string Name, names)
        cout << Name << endl;

    cout << endl << "Backward:" << endl;
    BOOST_REVERSE_FOREACH(string Name, names)
        cout << Name << endl;
    return 0;
}
```

此示例首先创建一个 vector。事实上，它与第 5 册第 6 章清单 6-1 中 Vectors 示例所使用的 vector 相同。在本例中，示例随后创建一个 `BOOST_FOREACH` 循环来遍历 `names`。每次迭代都会将 `names` 中的一个值放入 `Name`。然后代码打印该单个名称。

Boost 库的一个有趣特性是，你可以反转迭代顺序。在本例中，代码使用 `BOOST_REVERSE_FOREACH` 循环按相反方向——从末尾到开头——进行迭代。该技术与正向迭代完全相同。以下是应用程序的输出：

```text
Tom
Dick
Harry
April
May
June

Backward:
June
May
April
Harry
Dick
Tom
```

如你所见，正向和反向迭代完全按预期工作。`BOOST_FOREACH` 和 `BOOST_REVERSE_FOREACH` 宏支持多种容器类型：

- 任何标准模板库（STL）容器
- 数组
- 以 null 结尾的字符串（char 和 wchar_t）

## 提升一步
