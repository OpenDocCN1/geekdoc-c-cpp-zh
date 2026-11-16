

## 5.7. 嵌套条件语句

```
if (minutes == 1)
    std::cout << " minute ";
else
    std::cout << " minutes ";
}
// Print seconds at all?
if (seconds > 0 || (hours == 0 && minutes == 0 && seconds == 0)) {
    std::cout << seconds;
    // Decide between singular and plural form of seconds
    if (seconds == 1)
        std::cout << " second";
    else
        std::cout << " seconds";
}
std::cout << "\\n";
}
```

在清单 5.14（timeconv2.cpp）中，每个负责打印时间值及其英文单位的代码段都受到一个 `if` 语句的保护，该语句仅在时间值大于零时才允许代码执行。秒的处理是个例外：如果所有时间值都为零，程序应打印 `0 seconds`。请注意，每个负责确定单数或复数形式的 `if`/`else` 语句都嵌套在决定是否打印该值的 `if` 语句中。

清单 5.14（timeconv2.cpp）的一次运行产生

```
Please enter the number of seconds: 10000
2 hours 46 minutes 40 seconds
```

由于所有值都大于一，所有单词都是复数形式。另一次运行产生

```
Please enter the number of seconds: 9961
2 hours 46 minutes 1 second
```

请注意，单词 `second` 是单数形式，正如它应该的那样。

```
Please enter the number of seconds: 3601
1 hour 1 second
```

同样，打印的单词与它们所代表的值的数量一致。

```
Please enter the number of seconds: 7200
2 hours
```

另一次运行产生：

```
Please enter the number of seconds: 60
1 minute
```

最后，以下运行显示程序正确处理零秒：

```
Please enter the number of seconds: 0
0 seconds
```

### 图 5.5 带有多个可选执行路径的流程图

![](img/e84ad11adb18201d71595b31ce6c9eff_123_0.png)

## 5.8 多路 if/else 语句

简单的 if/else 语句可以在两个执行路径之间进行选择。假设我们希望从几个可能的路径中选择一个执行路径，如图 5.5 所示？

清单 5.9（enhancedcheckrange.cpp）展示了如何从三个选项中进行选择。如果许多动作中恰好只有一个应该被采取，该怎么办？需要嵌套 if/else 语句，这些嵌套 if/else 语句的形式如清单 5.15（digittoword.cpp）所示。

### 清单 5.15: digittoword.cpp

```
#include <iostream>

int main() {
    int value;
    std::cout << "Please enter an integer in the range 0...5: ";
    std::cin >> value;
    if (value < 0)
        std::cout << "Too small";
    else
        if (value == 0)
            std::cout << "zero";
        else
            if (value == 1)
                std::cout << "one";
            else
                if (value == 2)
                    std::cout << "two";
                else
                    if (value == 3)
                        std::cout << "three";
                    else
                        if (value == 4)
                            std::cout << "four";
                        else
                            if (value == 5)
                                std::cout << "five";
                            else
                                std::cout << "Too large";
    std::cout << '\n';
}
```

观察清单 5.15（digittoword.cpp）的以下几点：

- 它根据用户的输入恰好打印八条消息中的一条。
- 请注意，每个 `if` 主体包含一条打印语句，每个 `else` 主体（最后一个除外）包含一个 `if` 语句。控制逻辑迫使程序依次检查每个条件。第一个匹配的条件获胜，其相应的 `if` 主体将被执行。如果没有条件为真，则将打印最后一个 `else` 的 `Too large` 消息。
- 不需要花括号来界定 `if` 或 `else` 主体，因为每个主体只包含一条语句（尽管一个深度嵌套的 `if`/`else` 语句是一个非常大的语句）。

清单 5.15（digittoword.cpp）的格式遵循早期示例中使用的约定。因此，随着检查的条件增多，文本量会向右漂移。一种常用的替代样式，如清单 5.16（restyleddigitword.cpp）所示，避免了这种向右漂移。

### 清单 5.16: restyleddigitword.cpp

```
#include <iostream>

int main() {
    int value;
    std::cout << "Please enter an integer in the range 0...5: ";
    std::cin >> value;
    if (value < 0)
        std::cout << "Too small";
    else if (value == 0)
        std::cout << "zero";
    else if (value == 1)
        std::cout << "one";
    else if (value == 2)
        std::cout << "two";
    else if (value == 3)
        std::cout << "three";
    else if (value == 4)
        std::cout << "four";
    else if (value == 5)
        std::cout << "five";
    else
        std::cout << "Too large";
    std::cout << '\n';
}
```

根据我们迄今的经验，清单 5.16（restyleddigitword.cpp）的格式在某种程度上掩盖了程序逻辑的真实结构，但这种格式化多路 `if`/`else` 语句的样式非常常见，以至于大多数程序员都认为是可接受的。所有缩进到同一级别的 else if 行序列将此结构标识为多路 if/else 语句。

清单 5.17（datetransformer.cpp）使用多路 if/else 将月/日格式的数字日期转换为扩展的美国英语形式和国际西班牙语形式；例如，2/14 将被转换为 February 14 和 14 febrero。

### 清单 5.17: datetransformer.cpp

```cpp
#include <iostream>

int main() {
    std::cout << "Please enter the month and day as numbers: ";
    int month, day;
    std::cin >> month >> day;
    // Translate month into English
    if (month == 1)
        std::cout << "January";
    else if (month == 2)
        std::cout << "February";
    else if (month == 3)
        std::cout << "March";
    else if (month == 4)
        std::cout << "April";
    else if (month == 5)
        std::cout << "May";
    else if (month == 6)
        std::cout << "June";
    else if (month == 7)
        std::cout << "July";
    else if (month == 8)
        std::cout << "August";
    else if (month == 9)
        std::cout << "September";
    else if (month == 10)
        std::cout << "October";
    else if (month == 11)
        std::cout << "November";
    else
        std::cout << "December";
    // Add the day
    std::cout << " " << day << " or " << day << " de ";
    // Translate month into Spanish
    if (month == 1)
        std::cout << "enero";
    else if (month == 2)
        std::cout << "febrero";
    else if (month == 3)
        std::cout << "marzo";
    else if (month == 4)
        std::cout << "abril";
    else if (month == 5)
        std::cout << "mayo";
    else if (month == 6)
        std::cout << "junio";
    else if (month == 7)
        std::cout << "julio";
    else if (month == 8)
        std::cout << "agosto";
    else if (month == 9)
        std::cout << "septiembre";
    else if (month == 10)
        std::cout << "octubre";
    else if (month == 11)
        std::cout << "noviembre";
    else
        std::cout << "diciembre";
    std::cout << "\\n";
}
```

清单 5.17（datetransformer.cpp）的示例运行如下所示：

![](img/e84ad11adb18201d71595b31ce6c9eff_126_0.png)

图 5.6 比较了诸如清单 5.16（restyleddigitword.cpp）这样的程序中的 if/else 语句结构与诸如清单 5.10（binaryconversion.cpp）这样的程序中的结构。

在诸如清单 5.16（restyleddigitword.cpp）这样的程序中，if/else 语句是嵌套的，而在诸如清单 5.10（binaryconversion.cpp）这样的程序中，if/else 语句是顺序的。

C++ 提供了构建一些非常复杂的条件语句的工具。重要的是要抵制使事情过于复杂的冲动。考虑计算用户提供的五个整数值中最大值的问题。完整的解决方案留作第 5.10 节的练习，但这里我们将概述一个适当的策略。

假设你允许用户一次性输入所有值；例如，对于整数变量 n1、n2、n3、n4 和 n5：

```
std::cout << "Please enter five integer values: ";
std::cin >> n1 >> n2 >> n3 >> n4 >> n5;
```

现在，允许自己有一个名为 max 的额外变量。所有变量都有含义，它们的名称应该以某种方式反映其含义。我们将让额外的 max 变量表示“目前为止我确定的最大值”。以下是解决问题的一种方法：

- 1. 将 max 设置为等于 n1。这意味着就我们目前所知，n1 是最大的数字，因为 max 和 n1 具有相同的值。
- 2. 将 max 与 n2 进行比较。如果 n2 大于 max，则将 max 更改为 n2 的值，以反映我们确定 n2 更大的事实；如果 n2 不大于 max，我们就没有理由更改 max，因此不要更改它。
- 3. 将 max 与 n3 进行比较。如果 n3 大于 max，则将 max 更改为 n3 的值，以反映我们确定 n3 更大的事实；如果 n3 不大于 max，我们就没有理由更改 max，因此不要更改它。
- 4. 对 n4 和 n5 遵循相同的过程。

最终，max 变量的含义保持不变——“目前为止我确定的最大值”，但是，在将 max 与所有输入变量进行比较后，我们现在知道它是所有五个输入值中的最大值
