

```cpp
std::cout << "The number is too large.\n";
else { /* x > 0 but x <= 1000 */
    std::cout << "The number is positive.\n";
}
}
```

在这里可以清楚看出哪个 `else` 到底属于哪一个 `if`。但深层缩进是以可读性为代价的。对于标准的 `if-else` 级，最好不要将 `else` 分支封装在自己的块中。

## 8.5.1 带有初始化器的 "if" 在实际条件之前放置一个（初始化）表达式：
`if( Initialization ; Condition ) Statement`

通常情况下，你会在 `Initialization` 中声明一个变量，但也可以在这里编写任何表达式。声明的变量在 `if` 语句内部是有效的，因为这等于以下内容：

```cpp
{ Initialization ; if( Condition ) Statement }
```

在程序中，它看起来如下所示：

```cpp
// https://cppbolt.org/z/d6PscKx4M
#include <map>
#include <string>
#include <algorithm> // any of
#include <iostream> // secr
std::map<int, std::string> m;
int main() {
    if(auto i = m.find(10); i != m.end()) return i->second.size();
    if(char buf[10]={0}; fgets(buf, 10, stdin)) { m[0] += buf; }
    std::string s;
    if(auto keywords = {"if", "for", "while"};
    std::any_of(keywords.begin(), keywords.end(),
    [s](const char* kw) { return s == kw; })); {
        std::cerr << "Error ";
    }
}
}
```
```
# Listing 8.10 这些 if 语句包含了初始化器。

变量 `i`、`buf` 和 `keywords` 仅在语句内部有效。当然，你也可以使用 `else` 分支。初始化在在该分支内也是有效的。

如果你不想在某些情况下将某段代码包含在程序中，可以使用自 C++17 起的 `constexpr if`：

```cpp
if constexpr( Condition ) Statement
```

编译器随后会在编译时评估条件，并有权从最终程序中排除整个代码块。这对于调试常量或泛型函数非常有意义。

```cpp
// https://godbolt.org/z/Ycse4EWav
#include <iostream> // count
template<typename T>
void memory(T X) {
    if constexpr(sizeof(T) > 4) {
        std::cout << "Requires a lot of memory: " << x << " ";
    }
}
constexpr auto DEBUG = true;
int main() {
    if constexpr(DEBUG) {
        std::cout << "Debug is on. ";
    }
}
```

```cpp
memory<long long>(44LL);
}
```
**Listing 8.11** 编译器可以在编译时评估条件。

这种工作以前只能通过宏或巧妙的模板编程实现。

你完全可以添加一个 `else` 分支并与初始化表达式一起使用。

从 C++23 开始，还有一个 `if consteval`，它用于判断调用上下文是否为 `constexpr`；请参见第 13 章第 13.10.9 节。

## 8.6 “while” 循环

`while` 循环只要指定的条件满足，就会执行语句。该过程如图 8.3 所示。你可以这样写它：

```cpp
while( Condition ) Statement
```

对于 `Condition` 和 `Statement`，我提到的关于 `if` 的所有内容都适用。因此，下面的示例对你来说应该没有困难。

```cpp
// https://gdbbolt.org/z/h466fY4W
#include <iostream>
int main() {
    /* 从 1 到 100 求和 */
    int sum = 0;
    int number = 1;
    while(number <= 100) // condition
        sum += number; // 重复执行的块
        number += 1; // 下一个数字
    } // 重复块的结束
    std::cout << sum << std::endl;
}
```
Listing 8.12 循环运行 100 次。

在循环执行之前，首先检查条件。因此，这个循环将为 1 到 100 之间的每个数字运行一次——恰好 100 次。每个数字都会被加到末尾，`sum` 包含了从 1 到 100 所有数字之和的结果——据说这位数学家在小学时几秒钟内就在脑海中解决了这项任务，因为他意识到自己只需要计算 $(100 \cdot 101) / 2$。嗯，在计算机的帮助下，你比高斯还要快。

![](img/290cf54dfcaad53865de6b8cca8f)
**Figure 8.3** “while”循环的流程图。

当你编写这样的循环时，确保条件不再满足并终止循环是非常重要的。在这里，`number` 是一个简单的计数变量，并在块内递增。常见的错误包括忘记递增或错误地设置条件。你能看到如果忘记 `number = number + 1` 会发生什么吗？

```cpp
while(number <= 100) { // 检查了 number 但从未递增
    sum += number;
}
```
这个循环将无限运行，因为 `number` 永远不会递增，所以 `number <= 100` 的条件始终为真。程序永远不会到达输出，你必须从外部终止它。在 IDE 中，你会找到一个用于此的按钮或菜单项。在控制台中，`Ctrl+C` 通常能救你。也可能是条件从一开始一开始就不满足。在这种情况下，语句块将不会执行。

> 循环设计
> 循环是编程中一个具有挑战性的方面，也是错误的常见源头。错误并不总是像忘记递增那样容易找到。为了安全地工作，请向自己明确相关变量在循环中扮演什么角色：该变量是计数器吗？它是可变的吗？它与条件有什么关系？

## 8.7 “do-while” 循环

这种罕见的 `while` 循环变体条件位于末尾：

```cpp
do Statement while( Condition )
```

在这里，`Statement` 先执行，然后检查 `Condition`，如流程图 8.4 所示。检查发生在每次迭代之后。这意味着语句至少会被执行一次。

```cpp
// https://cppbolt.org/z/6hhKhEx
#include <iostream> // cin
#include <string>
int main() {
    std::string line;
    do {
        std::getline(std::cin, line); // 至少执行一次 getline
        if(!std::cin) break; // 错误或文件结束
    } while(line != "quit"); // 在特定输入时结束
}
```
**Listing 8.13** “do-while”循环的主体至少执行一次。

你不应该经常使用这种 `while` 循环变体，因为它相当不常见。此外，循环中的条件是如此重要，将其放在末尾可能会阻碍理解。

![](img/290cf54dfcaad53865de6b8cca8f_359)
**Figure 8.4** “do-while”循环的流程图。

## 8.8 “for” 循环

你在 `while` 循环中已经看到，你通常为循环初始化一个计数变量，并在循环结束时对其进行递增。因为这非常常见，所以它在 `for` 循环中被封装在一起并从而简化了：

```cpp
for( Initialization ; Condition ; Update ) Statement
```

`Statement` 和 `Initialization` 是语句，而 `Condition` 和 `Update` 是表达式。

在初始化中定义循环变量、在更新中修改它、并在条件中检查它，是常见的做法。一个循环很好地对应于这个组织良好的 `while` 循环：

```cpp
{ Initialization ; while( Condition ) { Statement ; Update } }
```

在图 8.5 中，你可以看到该过程的示意。我将在接下来的列表中将 Listing 8.12 重写为 `for` 循环。

```cpp
// https://godbolt.org/z/7fYocAmaz
#include <iostream>
int main() {
    /* 从 1 到 100 求和 */
    int sum = 0;
    for(int number=1; number <= 100; number+=1) { // 紧凑形式
        sum += number; // 为了结果
    }
    std::cout << sum << std::endl;
}
```
**Listing 8.14** 使用 “for”循环求和。

这里是初始化 `int number=1`。在循环中的语句执行之前，检查条件 `number <= 100`。然后执行循环，这里是 `sum += number;`。在块的结束处，执行更新 `number += 1`。

然后再次检查条件。如果满足，则进入下一次循环迭代；如果不，循环结束。

即使使用 `for`，`number` 最终也是 101。按照我现在的写法，我无法输出它，因为 `number` 变量只在循环内部存在。但是，你可以在循环之前声明它并让初始化部分为空。

```cpp
// https://godbolt.org/z/185ha3q3f
#include <iostream>
int main() {
    /* 1到100求和 */
    int sum = 0; // 循环前的初始化
    int number = 1;
    for(; number <= 100; number=number+1) { // 空初始化
        sum = sum + number;
    }
    std::cout << number << std::endl; // number 现在也存在
}
```
**Listing 8.15** 带有空初始化部分的 “for”循环。

在这里你也可以在循环外部访问 `number`，从而看到它是如何打印 101 的。

