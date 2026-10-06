
![](img/8b33dbf2a2ef620c5ea6844ae78b2983_101_1.png)

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_101_2.png)

- 步骤 2 如果你看到的和我们的截图类似，请查看屏幕顶部的菜单栏。在顶层菜单的 `File` 选项下，你可以看到一组图标：黄色齿轮、绿色播放按钮以及齿轮/播放按钮。这些是构建（`Build`）、运行（`Run`）和函数（`Functions`）。

- 步骤 4 现在点击运行（`Run`）图标，即绿色播放按钮。显示单词：`Hello, world!`; 紧接着是执行代码的时间，并提示你按任意键继续。干得好，你刚刚编译并执行了你的第一个程序。

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_101_3.png)

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_101_4.png)

### C++ 程序结构

### 注释 (COMMENTS)

双斜杠开头的行是注释。这意味着它们不会在代码中执行，并且会被编译器忽略。注释的设计是为了帮助你，或者查看你代码的另一个程序员，解释正在发生什么。注释有两种类型：`//` 覆盖多行注释，`//` 是单行注释。

这里使用的尖括号（chevrons）是插入运算符。这意味着尖括号后的任何内容都将插入到语句中。如果它们是 `'Hello, world'`，那么在执行代码时它们将显示在屏幕上。

```cpp
// helloworld.cpp

#include <iostream>

int main() {

    // 我的第一个 C++ 程序

    cout << "Hello, world!";

    return 0;

}
```

```cpp
// Hello, "world!"

const string_name_full_ref = "Hello, world!";

string_name_full_ref = "Hello, world!";

string_name_full_ref = "Hello, world!";

string_name_full_ref = "Hello, world!";

string_name_full_ref = "Hello, world!";

int copy_i = 0;

cout << backward() << bt2;
```

| | |
| :--- | :--- |
| | cout |
| | 打开声明 |
| | 关闭顶部 |

## STD

`while` 代表的是完全不同的含义，在 C++ 中，它代表“标准”（Standard）。它是 C++ 标准命名空间（Standard Namespace）的一部分，涵盖了许多语句和命令。你可以从代码中省略 `std` 部分，但它必须在开头声明：`using namespace std;`。两者不可兼得。例如：

```cpp
#include <iostream>

using namespace std;
```

接下来，“Hello, world!" 是我们在代码执行时显示在屏幕上的内容。你可以输入任何你想输入的内容，只要它在引号内。括号是必须的，但有些注释位于里面。`\n` 表示要插入新行。

```cpp
// helloworld.cpp

#include <iostream>

int main() {

    // 输出消息

    cout << "Hello, world!\n"; 

    return 0;

}
```

```cpp
// 我的第一个 C++ 程序

cout << "Hello...
```

## COUT

在这个示例中，我们使用了 `cout`，它是标准命名空间的一部分，它之所以在那里，是因为要求 C++ 使用该特定命名空间中的内容。`cout` 意味着字符输出（Character Output），显示或屏幕。为了显示屏幕，如果我们使用 `std;`，我们必须像之前提到的那样在代码开头声明它。

## 分号 (;) 和 与 (AND)

最后，你可以在函数代码块内的行（注释除外）中使用分号。这标记了语句的结束，且 C++ 中的所有语句末尾必须有一个分号，否则编译器将无法构建代码。最后一行有一个大括号，表示函数的结束。

```cpp
// helloworld.cpp

#include <iostream>

using namespace std;

int main() {

    // 我的第一个 C++ 程序

    cout << "Hello, world!";

    return 0;

}
```

```cpp
// helloworld.cpp

#include <iostream>

using namespace std;

int main() {

    // 我的第一个 C++ 程序

    cout << "Hello, world!\n";

    return 0;

}
```

## C++ 基础

### 编译与执行

你创建了第一个 C++ 程序，现在你理解了结构背后的基础知识。让我们实际行动起来，编译并执行（或者如果你愿意，叫运行）程序，看看它看起来是什么样。

### 来自 C++ 的问候

在 Code:Blocks 中编译和执行 C++ 代码非常简单；只需点击图标并查看结果即可。以下是操作方法：

- 打开 Code:Blocks（如果还没有打开的话），并加载之前创建的 Hello World 代码。确保没有可见的错误，例如 `std::cout` 行末尾缺少分号。

- 首先点击构建（`Build`）图标，即黄色齿轮。此时，你的代码已经通过了 Code:Blocks 编译器的检查并检查了错误。你可以通过查看底部窗格来查看构建结果。任何关于代码质量的都会都会显示在这里。

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_101_0.png)

```cpp
#include <iostream>

int main() {

    std::cout << "Hello, world!" << std::endl;

    return 0;

}
```

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_101_1.png)

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_101_2.png)

- 步骤 2 如果你看到的和我们的截图类似，请查看屏幕顶部的菜单栏。在顶层菜单的 `File` 选项下，你可以看到一组图标：黄色齿轮、绿色播放按钮以及齿轮/播放按钮。这些是构建（`Build`）、运行（`Run`）和函数（`Functions`）。

- 步骤 4 现在点击运行（`Run`）图标，即绿色播放按钮。显示单词：`Hello, world!`; 紧接着是执行代码的时间，并提示你按任意键继续。干得好，你刚刚编译并执行了你的第一个程序。

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_101_3.png)

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_101_4.png)

## 使用注释 (Using Comments)

虽然注释可能只是代码中的一个微小元素，但（此处原文截断）

虽然注释可能看起来是代码中的一个微小元素，但当代码组合成一个游戏、应用程序甚至整个操作系统时，事实上它们可能是最重要的因素之一。

## 注释的重要性 (THE IMPORTANCE OF COMMENTING)

注释内部的代码基本上是人类可读的描述，详细说明代码在特定一点的功能。它们看起来并不重要，但没有注释的编程是非常令人沮丧，无论你是专业人士还是初学者。

简而言之，代码应该以有效地描述行、部分或单个元素的方式进行注释。你应该养成尽可能注释的习惯，这样不了解编程的人也可以阅读你的代码并理解它将做什么。

在专业环境中，注释对于代码的成功至关重要。在组织中，许多程序员与工程师、开发者、分析师一起工作。如果你是开发软件的团队的一部分，你的注释可以帮助团队发现某些错误，另一个团队成员可能会接手并追踪线索来确定问题。

把自己放在一个工作是处理超过 80 万行代码的位置，这些代码分布在多个不同的模块中。你可以看到对原始程序员寻求帮助的需要，形式就是良好的注释。

## C++ 注释

在 C++ 中，注释涉及使用双正斜杠 `//`，或者正斜杠加星号 `/*`。你已经见过一些简短的示例，但这里是它们的工作原理。

以 Hello World 代码为例，你可以使用正斜杠轻松对代码的不同部分进行注释：

在编写注释时要小心，尤其是多行注释。很容易忘记添加星号和正斜杠来取消掉掉落在注释块内的任何代码。

```cpp
// 我的第一个 C++ 程序

cout << "Hello, world!\n";

#include <iostream>

using namespace std;

int main() {

    // 我的第一个 C++ 程序

    cout << "Hello, world!\n";

}
```

```cpp
#include <iostream

using namespace std;

int main() {
```
