
```java
String guessMessage = String.format(
    "There %s %s %s%s", verb, number, candidate, pluralModifier
);
print(guessMessage);
}
```

这个函数有点太长，而且这些变量贯穿始终。为了将函数拆分成更小的片段，我们需要创建一个 `GuessStatisticsMessage` 类，并将这三个变量设为该类的字段。这就为这三个变量提供了清晰的上下文。它们*确实*是 `GuessStatisticsMessage` 的一部分。上下文的改善还使得算法可以通过拆分成许多更小的函数而变得更加整洁。（参见[清单 2-2](#)。）

### 清单 2-2 变量具有上下文。

```java
public class GuessStatisticsMessage {
    private String number;
    private String verb;
    private String pluralModifier;

    public String make(char candidate, int count) {
        createPluralDependentMessageParts(count);
        return String.format(
            "There %s %s %s%s",
            verb, number, candidate, pluralModifier );
    }

    private void createPluralDependentMessageParts(int count) {
        if (count == 0) {
            thereAreNoLetters();
        } else if (count == 1) {
            thereIsOneLetter();
        } else {
            thereAreManyLetters(count);
        }
    }

    private void thereAreManyLetters(int count) {
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }

    private void thereIsOneLetter() {
        number = "1";
        verb = "is";
        pluralModifier = "";
    }

    private void thereAreNoLetters() {
        number = "no";
        verb = "are";
        pluralModifier = "s";
    }
}
```

### 不要添加不必要的上下文

在一个名为“Gas Station Deluxe”的虚构应用程序中，给每个类加上 GSD 前缀是个坏主意。坦率地说，你是在与你的工具作对。你输入 G 并按补全键，得到的却是系统中每个类的一长串列表。这明智吗？为什么要让 IDE 难以帮助你？

同样，假设你在 GSD 的会计模块中发明了一个 MailingAddress 类，并将其命名为 GSDAccountAddress。后来，你的客户联系应用程序需要一个邮寄地址。你会使用 GSDAccountAddress 吗？它听起来像正确的名称吗？17 个字符中有 10 个是多余或无关的。

只要清晰，较短的名字通常比较长的名字更好。不要给名字添加超出必要的上下文。

`accountAddress` 和 `customerAddress` 作为 `Address` 类的实例名是很好的名字，但作为类名可能就不太好了。`Address` 是一个不错的类名。如果我们需要区分 MAC 地址、端口地址和 Web 地址，我可能会考虑 `PostalAddress`、`MAC`、

## 第五章 模拟信号的频域分析

在连续时间信号与系统的分析中，傅里叶变换是一种非常重要的数学工具，它将信号的时域特性与频域特性联系起来，使人们对信号和系统的研究可以在频域中进行。本章首先介绍周期信号的傅里叶级数和非周期信号的傅里叶变换，然后讨论傅里叶变换的性质，最后介绍系统的频域分析方法。

### 5.1 周期信号的傅里叶级数

将周期信号表示为各个频率分量的线性组合，即傅里叶级数，是分析周期信号频域特性的基本方法。

设 f(t) 是一个周期为 T 的周期信号，即 f(t) = f(t + mT) (m 为任意整数)，且满足狄里赫利条件，则 f(t) 可以展开为如下形式的傅里叶级数：

f(t) = a₀/2 + Σₙ₌₁^∞ [aₙ cos(nω₀t) + bₙ sin(nω₀t)]

其中，ω₀ = 2π/T 称为基波角频率；a₀、aₙ、bₙ 为傅里叶系数，分别由以下公式给出：

a₀ = (2/T) ∫₀ᵀ f(t) dt,  aₙ = (2/T) ∫₀ᵀ f(t) cos(nω₀t) dt,  bₙ = (2/T) ∫₀ᵀ f(t) sin(nω₀t) dt

式中，n = 1, 2, 3, …。上述傅里叶级数还可表示为余弦形式：

f(t) = c₀/2 + Σₙ₌₁^∞ cₙ cos(nω₀t + φₙ)

## 3 函数

![](img/d3848357ae109884a140c7b3662e0e30_77_0.png)

在编程的早期，我们用例程和子例程来构建系统。然后，在 Fortran 和 PL/1 时代，我们用程序、子程序和函数来构建系统。如今，从那个时代保留下来的只有函数。函数是任何程序中的第一级组织单元。本章的主题就是如何写好函数。

请看[清单 3-1](#)中的代码。在 FitNesse¹ 中很难找到一个长函数，但经过一番搜索我找到了这个。它不仅很长，而且含有重复的代码、大量奇怪的字符串，以及许多陌生且不直观的数据类型和 API。看看你在接下来的三分钟内能从其中理出多少头绪。

### 清单 3-1 `HtmlUtil.java`（FitNesse 20070619）

```java
public static String testableHtml(
    PageData pageData,
    boolean includeSuiteSetup
) throws Exception {
    WikiPage wikiPage = pageData.getWikiPage();
    StringBuffer buffer = new StringBuffer();
    if (pageData.hasAttribute("Test")) {
        if (includeSuiteSetup) {
            WikiPage suiteSetup =
                PageCrawlerImpl.getInheritedPage(
                    SuiteResponder.SUITE_SETUP_NAME, wikiPage
                );
            if (suiteSetup != null) {
                WikiPagePath pagePath =
                    suiteSetup.getPageCrawler().getFullPath(suiteSetup);
                String pagePathName = PathParser.render(pagePath);
                buffer.append("!include -setup .")
                    .append(pagePathName)
                    .append("\n");
            }
        }
    }
    WikiPage setup =
        PageCrawlerImpl.getInheritedPage("SetUp", wikiPage);
    if (setup != null) {
        WikiPagePath setupPath =
            wikiPage.getPageCrawler().getFullPath(setup);
        String setupPathName = PathParser.render(setupPath);
        buffer.append("!include -setup .")
            .append(setupPathName)
            .append("\n");
    }
    buffer.append(pageData.getContent());
    if (pageData.hasAttribute("Test")) {
        WikiPage teardown =
            PageCrawlerImpl.getInheritedPage("TearDown", wikiPage);
        if (teardown != null) {
            WikiPagePath tearDownPath =
                wikiPage.getPageCrawler().getFullPath(teardown);
            String tearDownPathName = PathParser.render(tearDownPath);
            buffer.append("\n")
```

这还增加了文档价值，因为在块内调用的函数可以有一个很好的描述性名称。

这也意味着函数不应该大到能够容纳嵌套结构。因此，函数的缩进级别不应超过一级或两级。当然，这会使函数更容易阅读和理解。

### 只做一件事

显然，[清单 3-1](#) 所做的远远不止一件事。它创建缓冲区、获取页面、搜索继承的页面、渲染路径、拼接晦涩的字符串以及生成 HTML 等等。[清单 3-1](#) 忙于做许多不同的事情。另一方面，[清单 3-3](#) 只做一件简单的事情。它把 setups 和 teardowns 包含到测试页面中。

下面的建议以这样或那样的形式已经出现 30 年甚至更久。

![](img/d3848357ae109884a140c7b3662e0e30_83_0.png)

***函数应该只做一件事。应该把它做好。应该只做这一件事。***

这句话的问题在于，很难知道什么是“一件事”。[清单 3-3](#) 只做一件事吗？很容易论证它做了三件事：

- 判断页面是否为测试页面。
- 如果是，则包含 setups 和 teardowns。
- 以 HTML 形式渲染页面。

那么到底是哪一种？这个函数是在做一件事还是三件事？请注意，函数的这三个步骤比函数名称所陈述的抽象级别低一级。我们可以用一个简短的 TO⁴ 段落来描述这个函数：

> *为了渲染带 setups 和 teardowns 的页面，我们检查页面是否为测试页面，如果是，我们包含*

与基本概念混杂在一起，越来越多的细节往往会在函数内部累积。

### 从上到下阅读代码：阶梯规则

我们希望代码读起来像一篇自上而下的叙述。^5 我们希望每个函数后面跟着处于下一抽象级别的函数，这样我们在从上到下阅读函数列表时，就能逐级下降一个抽象级别。我把这称为*阶梯规则*。

换句话说，我们希望程序读起来就像一组 *TO* 段落，每个段落描述当前抽象级别，并引用下一级别的后续 *TO* 段落。

> *要包含 setups 和 teardowns，我们先包含 setups，然后包含测试页面内容，最后包含 teardowns。*

> *要包含 setups，如果是套件，我们先包含套件 setup，然后包含常规 setup。*

> *要包含套件 setup，我们在父层级中搜索 “SuiteSetUp” 页面，并添加一条包含该页面路径的 include 语句。*

> *要搜索父级…*

事实证明，程序员很难学会遵循这一规则并编写保持在单一抽象级别的函数。但学习这一技巧也非常重要。它是保持函数简短并确保它们“只做一件事”的关键。让代码读起来像一组自上而下的 *TO* 段落，是保持抽象级别一致的有效技巧。

看看本章末尾的[清单 3-7](#)。它展示了根据这里描述的原则重构的完整 `testableHtml` 函数。注意每个函数是如何引出下一个函数的，并且每个函数都保持一致的抽象级别。

### Switch 语句

