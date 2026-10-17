
```d
if (month == 2) day = 28; // 注意：原文 OCR 在此处有误，逻辑上 2 月应该是 28

break;

case 31:

if (month == 2) day = 28;

else if (!longMonth(month)) day = 30;

break;

default:
// 无需操作
break;

}
```

函数 `nextDay` 处理了年份的进位，并使用辅助私有函数 `adjustDay` 来确保日期保持在有效日期范围内。这里正是问题所在：在进入 `adjustDay` 时，不变性可能会被破坏。或者可能会被破坏——`adjustDay` 的唯一目的就是修复 `Date` 对象！

什么让 `adjustDay` 特殊？它的保护级别：它是一个私有函数，只有允许修改 `Date` 对象的函数才能访问。在私有函数的进入和退出，通常情况下不变性是可以接受的。必须接受不变性的地方是公共方法边界：不允许客户端操作让对象处于无效状态。

受保护函数呢？根据讨论，并非所有支持合约的编程系统都允许一种忽略合约检查的模式。该模式应该只对经过彻底审查、验证和测试的程序激活。

## 10.6 跳过合约。发布构建

合约专门用于验证应用程序的内部逻辑。与此一致，任何 D 编译器提供了一个标志（在参考实现中为 `--release`）来完全忽略合约，它解析并类型检查所有合约代码，但在执行文件中不留任何痕迹。发布构建不运行合约检查（风险更高），但也可以全速运行（更快）。如果应用程序已经准备就绪，跳过合约检查的额外风险很低，速度的提升非常值得。不运行合约的可能性加强了这种警告：代码应使用合约来处理可能失败的常规检查。合约必须保留给反映程序 Bug 的非预期错误。再次，你不应该使用合约来确保用户输入正确。

### 10.6.1 enforceIsNot (相当) 断言

`assert` 在发布构建中消失很遗憾，因为使用它非常方便。与其编写：

```d
if (!expr1) throw new SomeException;

...

if (!expr2) throw new SomeException;

...

if (!expr3) throw new SomeException;
```

只需要写：

```d
assert(expr1);

...

assert(expr2);

...

assert(expr3);
```

由于 `assert` 如此简洁，许多库提供了一种“始终断言”功能，在条件为零时检查条件并抛出异常，无论你以何种模式编译。此类检查器在 C++ 中以 `VERIFY`、`ASSERT ALWAYS` 或 `ENFORCE` 等名称存在。D 在 `std.contracts` 模块中定义了这样的函数，名为 `enforce`。使用与 `assert` 相同的语法使用 `enforce`：

```d
enforce(expr1);
enforce(expr2, "That isn't quite true");
```

如果传入的表达式为零，无论你是在 release 模式还是非 release 模式编译程序，`enforce` 都会抛出一个 `Exception` 类型的对象。如果你想抛出不同类型，可以如下所示指定：

```d
import std.contracts;
bool something = true;
```

如果 `something` 为零，则会抛出第二个参数：`enforce` 采用惰性求，如果 `expr1` 非零，则不会发生对象创建。

尽管 `assert` 和 `enforce` 看起来和感觉非常相似，但它们的作用不同。不要忘记两者之间的区别：

- `assert` 检查你的断言逻辑，而 `enforce` 检查不会威胁到你断言完整性的条件。
- `assert` 抛出不可恢复的 `AssertionError` 异常，而 `enforce` 默认抛出一个可恢复的异常（并且可以通过额外的参数抛出任何异常）。
- `assert` 可能会消失，因此在考虑函数流程时不要将其考虑内；`enforce` 永远不会消失，所以在调用 `enforce(e)` 后，你可以假设 `e`是非零的。

### 10.6.2 assert(false)

针对编译期间已知为零的常量进行断言（例如 `assert(false)`、`assert(0)` 或 `assert(null)`），其行为与普通的 `assert` 不同。

在 release 模式下，`assert(false)` 什么都不做：它只是抛出一个 `AssertionError` 异常。

然而，在 release 模式下，`assert(false)` 并不会被编译掉；它始终会导致程序停止。这一次，在遇到 `assert(false)` 后将不会有异常，也没有继续运行的机会。程序将崩溃。这是通过执行 `HLT`（“停止”指令指令实现的，该指令会导致程序立即终止。

我们中的许多人倾向于将崩溃视为一种高度危险的事件，表明程序失了控制。这种倾向很可能是因为许多程序早晚都会通过崩溃而终止。

## 10.7 Contracts（契约）：不用于清理输入

`assert(false)` 是一种非常受控的终止程序的方式。事实上，在操作系统上，`HLT` 会自动加载你的调试器，并将其定位在触发崩溃的那一行代码上。

`assert(false)` 这种特定行为的目的是？一个显而易见的用途与系统级程序有关。需要一种可移植的方法来使用 `HLT`，而 `assert(false)` 与语言的其他部分集成得很好。此外，编译器感知 `assert(false)` 的语义，例如，它不允许随其出现死代码：

```d
int func(int x) {
    assert(false); // 错误！
    return x;      // 语句不可达
}
```

相反，在某些情况下，你可能需要添加 `assert(false)` 来抑制编译器错误。例如，考虑上面讨论过的标准库函数 `readText`：

```d
import std.contracts;
string func() {
    enforce(false, "can't continue"); // 总是抛出
    assert(false);                  // 不可达
}
```

`enforce` 的调用总是抛出异常，但编译器并不知道这一点。为了让编译器理解该点无法到达，请插入 `assert(false)`。以 `return` 结尾是可行的，但在那种，如果以后有人注释掉了 `enforce` 调用，`func` 就会返回虚假值。`assert` 保护你的代码免受此类情况的影响。

本节讨论了一个与契约相关的争议问题，它是辩论的。这个问题本质上归结为：如果一个函数必须进行某些检查，检查应该放在哪里——契约中还是函数体中？

当刚习惯契约编程（Contract Programming）时，我们许多人可能会将大多数检查移动到契约内部。例如，考虑一个名为 `readText` 的函数，它将整个文本文件作为字符串加载。有了契约，我们可以这样定义它：

```d
import std.file, std.utf;
string readText(in char[] filename) {
    std.utf.validate(result);
    return cast(string) filename;
}
```

`readText` 实际上是标准库中的函数；你可能想在 `std.file` 中查找它）。`readText` 依赖另外两个函数。首先，它使用 `read` 将整个文件加载到内存缓冲区。内存缓冲区类型为 `char[]`，`readText` 将其转换为 `string`。但留那样是不正确的：如果文件包含 UTF 字符怎么办？为了验证该转换，契约通过调用 `std.utf.validate` 来验证结果，如果缓冲区包含无效字符，它将抛出 `UtException`。

如果不是由于一个根本性问题，那将会是：契约必须验证应用程序的逻辑，而不是输入的有效性。任何不被视为应用程序问题的内容都不属于契约内部。此外，契约不应该阻止应用程序的变化——因此 D 语言刻意限制了在契约内部可以修改的内容。

假设没有契约失败，应用程序在不执行契约的情况下必须以相同的行为和结果运行。这是一个非常简单且无记忆状态的测试，用于判断什么是契约，什么不是契约。契约是特定的检查，如果这些检查在正确的实现中消失，也不会影响实现正常工作！契约就是这样管理的。期望文件始终有效可能表现出一种积极的态度，但不应应该是 `readText` 规范的一部分。`readText` 的正确定义使检查成为函数不可或缺的一部分：

```d
import std.file, std.utf;
string readText(in char[] filename) {
    auto result = cast(string) read(filename);
    std.utf.validate(result);
    return result;
}
```

## 10.8 Contracts 与继承

考虑到目前为止的讨论，关于检查放置位置问题的答案是：如果检查涉及应用程序逻辑，它应该放在契约中；否则，检查应该放在函数体中且永远不会被跳过。

这听起来很棒，但在由独立实体编写的独立通用库构建的应用程序中，如何定义“应用程序逻辑”呢？考虑一个大型通用库，例如 Microsoft Windows API 或 KDE 桌面环境。许多应用程序使用此类 API，库函数接收不符合规范的参数是不可避免的（在操作系统 API 中，可能需要接收各种格式错误的参数）。如果应用程序没有满足库函数的条件，责任归谁所有？这显然是应用程序的错，但承担后果的是库——在不稳定性、未定义行为、库内部状态损坏、崩溃等所有糟糕的日子方面。尽管这看起来可能不公平，但此类问题对库的负面影响（“XYZ 库容易出现不稳定性和意外的特性”）要大于使用它的那些满是 bug 的应用程序。

一个通用且大型分发的 API 应该理所当然地验证其所有函数的所有输入——而不是在契约中。未能验证参数无疑是一个库 bug。没有任何发言人会去验证一本书并说：“我们当时在用契约编程，所以我们没有责任。”

这是否否定了函数应该（例如在参数范围之前）使用前提的论点？完全没有。这是一个关于定义和区分“应用程序逻辑”与“用户输入”的问题。对于作为应用程序逻辑不可或缺部分的函数来说，它是契约的一部分。对于属于独立交付库的通用函数，参数仅仅是用户输入。

另一方面，库在其私有函数中使用契约是完全可以的。这些函数涉及库的内部运作，并且无法被用户代码访问，因此让它们使用契约来表达对规范的遵循是明智。

必须重写。灵活性的考虑仅限于那些不会负面影响合约理解的变体：允许替代者要求的更少而提供的更多。

### 10.8.1 继承与合约

再次考虑 `Date` 的例子。假设我们定义了一个非常简单、轻量级的 `BasicDate`，它只提供最小的支持，并将增强功能留给派生类。`BasicDate` 提供了一个 `format` 函数，它接受一个表示格式规格的字符串，并返回一个格式化后的日期字符串：

```cpp
import std.conv;
class BasicDate {
    private uint day, month, year;
    string format(string spec)
    in {
        // 要求 spec 等于 "%Y/%m/%d"
        assert(spec == "%Y/%m/%d");
    }
    body {
        // 简单的实现
        return text(year, '/', month, '/', day);
    }
    ...
}
```

`Date` 施加的合约要求格式规格必须完全是 `"%Y/%m/%d"`，我们假设这是“长格式的年份，后跟斜杠，然后是月份，再跟斜杠，最后是日期”。这是 `BasicDate` 考虑支持的唯一格式。派生类可以添加本地化、国际化等。

继承 `BasicDate` 的类想要提供一种更好的格式原语——例如，假设 `Date` 允许在任意位置并混合任意字符使用指定符 `%Y`、`%m` 和 `%d`。此外，应该应该允许 `%%`，因为它重复了实际字符 `%`。相同指定符重复出现也应该是允许的。为了强制执行这些规则，`Date` 写了自己的合约：

```cpp
import std.regex;
class Date : BasicDate {
    override string format(string spec)
    in {
        auto pattern = regex("%[mdY]||[^%]*");
        assert(!match(spec, pattern).empty());
    }
    {
      string result;
      ...
      return result;
      ...
    }
```

`Date` 通过正则表达式建立了对 `spec` 的约束条件。正则表达式在字符串处理中是无价的辅助；强烈推荐 Fried 的经典著作《正则表达式详解》（Mastering Regular Expressions）[26]。这里不是深入讨论正则表达式的地方，但只需说 `"%[mdY]%"` 意味着“% 后面跟着 m、d、Y 中的任意一个或除 %以外的任何字符——重复零或多次”。匹配字符串与模式的等效代码将冗长得多。`assert` 确保字符串与模式的匹配返回一个非空匹配，如果是，则有效。（关于在 D 中使用正则表达式的更多信息，你可能想查阅标准模块 `std::regex` 的在线文档。）

`Date.format` 的聚合合约是什么？它应该考虑 `BasicDate.format` 的合约但也要放宽它。如果合约失败了没关系，只要派生的 `in` 合约通过。此外，`Date.format` 的合约绝不应该加强 `BasicDate.format` 的合约。新兴的规则如下：在重写的方法中，首先执行基类合约。如果成功，则将控制权交给 `body`。否则，执行派生类合约。如果成功，则将控制权交给 `body`。否则，报告合约失败。

另一种方法是，使用带短路的逻辑析（disjunction）组合合约；但必须有一个通过，且首先尝试基类合约。派生合约不太可能比基类合约更难满足。相反，派生合约为失败的前置条件提供了第二次机会。

上述规则对于 `Date` 和 `BasicDate` 运行良好。首先，复合合约检查精确的模式 `"%Y/%m/%d"`。如果成功，则继续格式化。如果失败，则检查是否符合派生的、更宽松的合约。如果通过，则可以继续格式化。

组合合约生成的代码如下：

```cpp
void __in_contract_Date.format(string spec) {
try {
  // 尝试基类合约
  this.BasicDate::__in_contract.format(spec);
} catch (throwable) {
  // 基类合约失败，尝试派生合约
  this.Date...in contract.format(spec);
}
// 成功，可以调用 body
}
```

### 10.8.2 继承与 out 合约

对于 `out` 情况，情况完全相反：当用派生对象替换基类对象时，重写函数提供的必须比合约承诺的更多。从一开始，基类的 `out` 保证必须始终由重写方法履行（与 `in` 合约的情况不同）。

相反，这意味着基类应该将合约设置得尽可能宽松且有用，以避免过度约束派生类的风险。例如，如果 `BasicDate.format` 要求返回的字符串包含年/月/日，它将有效地阻止任何派生类执行任何其他格式化。也许 `BasicDate.format` 应该实施一个更弱的合约——例如，如果格式化字符串为空，则不允许空字符串作为输出。

```cpp
import std.range, std.string;
```

```cpp
class BasicDate {
    private uint day, month, year;
    string format(string spec)
    out(result) {
        assert(!result.empty || spec.empty);
    }
    body {
        return std.string.format("%04s/%02s/%02s", year, month, day);
    }
    ...
}
```

`Date` 设置得稍微高一点：它根据格式规格计算预期结果长度，然后将实际结果长度与预期长度比较：

```cpp
import std.algorithm, std.regex;
```

```cpp
class Date : BasicDate {
    override string format(string spec)
    out(result) {
        bool escaping;
```

```cpp
size_t expectedLength;
foreach (c; spec) {
  switch (c) {
    case '%':
      if (escaping) {
        ++expectedLength;
        escaping = false;
      } else {
        escaping = true;
      }
      break;
    case 'Y':
      if (escaping) {
        expectedLength += 4;
        escaping = false;
      }
      break;
    case 'm': case 'd':
```
