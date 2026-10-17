
```cpp
helloworld.cpp
#include <iostream>
using namespace std;

int main() {

cout << "Hello, world\n";
}
```

## 步骤 6 为了将新更改应用到代码，需要重新编译、构建并运行它。这次，你只需点击构建/运行图标（黄色小齿轮和绿色按钮的组合图标）。

## 步骤 9 点击构建并运行图标以将更改应用到代码。由于你设置了错误，Code::Blocks 拒绝执行。在屏幕底部的日志面板中，你会收到此类错误提示：Expected '}' token，表示缺少分号。

![](img/0b5e7d59f3578d974082f03180129000_102_0.png)

![](img/0b5e7d59f3578d974082f03180129000_102_1.png)

## 步骤 7 正如我们在之前的页面中提到的，如果你已经在代码开头声明了 `namespace std;`，就不需要使用 `std::cout` 了。虽然我们可以直接点击构建/运行图标，但值得了解一下可用选项。你也可以看到，在构建和运行时，文件已保存。

## 步骤 10 补回分号，并在剪切行下方为你的代码添加新行：

`cout << "And greetings from C++\n";`

`\n` 在输出文本的最后一行添加一个换行。

构建并运行代码，显示你的结果。

![](img/0b5e7d59f3578d974082f03180129000_102_2.png)

![](img/0b5e7d59f3578d974082f03180129000_102_3.png)

# 使用注释

虽然注释在组成游戏、应用程序甚至整个操作系统的数行代码中看起来像是一个微不足道的元素，但理解代码在哪里出了问题或哪里运行得出色，可能是最重要的因素之一。

## 注释的重要性

代码内部的注释是非常符合人类阅读习惯的描述，详细说明了代码在特定一点正在做什么。它们不是特别重要，但无论你是专业人士还是初学者，没有注释的代码都是编程中许多令人令人沮丧的领域之一。

简而言之，对代码的注释方式应该有效地描述某行、某个部分或单个元素的目的。你应该养成尽可能多注释的习惯，这样不了解编程的人也能快速接手你的代码并快速理解它。

在专业环境中，注释对于代码和公司的成功至关重要。在组织中，经理与工程师、其他开发者、硬件分析师等并肩工作。如果你是编写软件团队的一员，你的注释可以帮助当另一个团队成员必须接手并追踪路径以定位问题时，节省出错的时间。

把自己设想成某人的立场，他的工作是检查你的超过 800,000 行代码（分布在多个模块中）程序。你可能会遇到原始程序员提供的帮助，这种帮助的形式就是良好的注释。

> 最好的注释是简洁的并且在逻辑上连接代码，详细说明当程序运行到某行或某部分时会发生什么。你不需要对每一行进行注释，类似 `x = 0` 这样的内容不需要你注释 `x` 等于零然后执行某些操作：这对读者来说是显而易见的。然而，如果等于零对用户的程序发生了剧烈变化，例如他们的行数用完了，那么就需要注释。

即使你在写注释时要像要和其他公开分享一样。这样你回过头来就能准确地理解你为什么要这样做，或者哪里做错了或哪里运行得出色。

良好的实践和经验帮助你理解何时需要添加注释，以及在必要时如何这样做。

```
DEF 240,220,324,305B,0,G,370,700,720,770,780B,720B,320B
DEF 320B,324B,305B,400B,410B,420B,430B,440B,450B,460B,470B,480B
DEF 490B,500B,510B,520B,540B,550B,560B,570B,580B,590B,600B,610B
DEF 620B,630B,640B,650B,660B,670B,680B,690B,700B,710B,720B,730B
```

## C++ 注释

在 C++ 中注释涉及使用双斜杠 `//`，或者斜杠加星号 `/* */`。你已经见过简短的示例，但这就是它们的工作方式。

步骤 1 以 Hello World 代码为例，你可以轻松地使用双斜杠对代码的不同部分进行注释：

```cpp
// My first C++ program
cout << "Hello, world\n";

#include <iostream>
using namespace std;

int main() {
    // My first C++ program
    cout << "Hello, world\n";
}
```

## 步骤 4 注释时要小心，尤其是使用注释块时。很容易忘记添加星号和斜杠来忽略掉落在注释块内的任何代码。

```cpp
HelloWorld.cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, world\n";
    cout << "And greetings from C++";
    // cover several lines
    // the need to add more slashes
    cout << "This line is now ignored by the compiler";
}
```

## 步骤 2 你也可以注释掉行代码，以更好的方式描述：`cout << "Hello, world\n";` `\n` 表示换行。

注意，你不需要在注释末尾放分号。因为它是被忽略的。

```cpp
HelloWorld.cpp
#include <iostream>
using namespace std;

int main() {
    // My first C++ program
    cout << "Hello, world\n"; // This line is ...
}
```

## 步骤 5 如果你想要通过注释掉缺失的括号 `}` 来隐藏代码块，回去纠正将浪费时间。坦率地说，Code::Blocks 的颜色会识别你的注释。

```cpp
helloworld.cpp
#include <iostream>
using namespace std;

int main() {
    // My first C++ program
    cout << "Hello, world\n";
    // This comment
    // cover several lines
    // the need to add more slashes
    cout << "This line is now ignored by the compiler";
}
```

## 步骤 3 你可以使用斜杠和星号注释掉几行：

> /* This comment

cover several lines

without the need to add more slashes /*

只需用相反的星号和斜杠结束注释块即可。

```cpp
int main() {
    // My first C++ program
    cout << "Hello, world\n";
    cout << "And greetings from C++";
    /* This comment
    cover several lines
    without the need to add more slashes */
}
```

## 步骤 6 如果你卡住了，在 C++ 中一个良好的习惯是在注释块的每行添加一个星号。这有助于你在继续编写代码之前关闭注释块：

> /* This comment

cover several lines

without the need to add more slashes /*

```cpp
int main() {
    // My first C++ program
    cout << "Hello, world\n";
    cout << "And greetings from C++";
    /* This comment
    cover several lines
    without the need to add more slashes */
    cout << "This line is now ignored by the compiler";
}
```

# C++ 基础

## 变量

使用 C++ 与 Python 相比略有不同。在 Python 中，你可以简单地声明 'a' 等于 10 并赋值给变量。但在 C++ 中，变量在使用之前必须用其类型进行声明。

## 变量的声明

你通过代码中的语句来声明 C++ 变量。你可以声明几种不同类型的变量。以下是其工作原理。

- **第 1 步** 打开一个新的空白 C++ 文件并输入通常的代码头文件：

- **第 2 步** 从创建两个变量 a 和 b 开始，另一个赋值为 10，你可以使用数据类型来声明这些变量。

- **第 3 步** 你可以构建并运行代码，但除了将值 10 和 5 存储在整数 a 和 b 中之外，你做不了什么。要输出变量的内容，添加：

```cpp
cout << a;
cout << "\n";
cout << b;
```

`cout << "\n";` 部分简单地在 10 和 5 的输出之间放置了一个换行符。

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a;
    int b;

    a = 10;
    b = 5;

    cout << a;
    cout << "\n";
    cout << b;
}
```

```cpp
Variables.cpp
1 2 3 4 5 6 7 8 9 10
#include <iostream>
using namespace std;

int main()
{
    int a;
    int b;

    a = 10;
    b = 5;

    cout << a;
    cout << "\n";
    cout << b;
}
```

- **第 4 步** 自然地你可以声明一个新变量 result，并输出一些简单的算术：

```cpp
int a;
int b;
a = 10;
b = 5;

int result;
result = a + b;
cout << result;
```

将上述代码插入到截图所示。

```cpp
Variables.cpp
1 2 3 4 5 6 7 8 9 10 11 12 13 14
#include <iostream>
using namespace std;

int main()
{
    int a;
    int b;
    int result;
    a = 10;
    b = 5;
    result = a + b;
    cout << result;
}
```

## **第 5 步**

一旦声明变量，就可以立即为其赋值。你输入的代码可能像这样：

```cpp
int a = 10;
int b = 5;
int result = a + b;

cout << result;
```

## **第 8 步**

之前的步骤创建了 StartLives，这是一个全局变量。在游戏中，玩家的生命值取决于表现的好坏。当玩家重启时，StartLives 返回到默认值：3。在这里我们分配了 3 次生命，减去 1 次，剩下 2 次。

```cpp
C:\Users\david\Documents\Variables.cpp
```

![](img/0b5e7d59f3578d974082f03180129000_106_0.png)

```
Process returned (0) execution time: 0:000
Press any key to continue.
```

![](img/0b5e7d59f3578d974082f03180129000_106_1.png)

## **第 9 步**

现代 C++ 编译器比大多数程序所认为的要智能得多。虽然你可以为变量声明许多数据类型，但你可以使用 `auto` 特性：

```cpp
#include <iostream>
using namespace std;
auto pi = 3.141593;

int main() {
```

```cpp
double area, radius = 1.5;
area = pi * radius;
cout << area;
```

![](img/0b5e7d59f3578d974082f03180129000_106_2.png)

## **第 6 步**

专门针对 C++，你也可以使用以下方法在声明时立即为变量赋值：

```cpp
int a (10);
int b (5);
```

从 C++ 2011 标准开始，使用大括号：

```cpp
{a+b};
```

![](img/0b5e7d59f3578d974082f03180129000_106_3.png)

```cpp
#include <iostream>
using namespace std;
auto pi = 3.141593;
int main() {
```

```cpp
double area, radius = 1.5;
area = pi * radius;
cout << area;
```

![](img/0b5e7d59f3578d974082f03180129000_106_4.png)

## **第 7 步**

你可以创建全局变量，它们声明在代码外部，并在任何函数中使用。到目前为止使用的变量是局部的：在函数内部使用。例如：第一个，auto 直到标准。然后新的数据类型 `double` 意味着双精度浮点数，将构建并运行代码：结果是 2.0000

```cpp
#include <iostream>
using namespace std;
int StartLives = 3;

int main() {
    StartLives = StartLives - 1;
    cout << StartLives;
}
```

![](img/0b5e7d59f3578d974082f03180129000_106_5.png)

![](img/0b5e7d59f3578d974082f03180129000_106_6.png)

## 数据类型

正如我们看到的，变量是程序员可以调用和操作的内存位置。在 C++ 中有许多不同的类型可用，例如整数、浮点、布尔、字符等。广泛接受有七种基本类型，但你可以创建自己的数据类型。这七种基本类型非常精确，但那些数字只精确到五位小数。默认输出的这种数字也有问题，你可以通过在括号内添加 `.precision()` 函数来解决，然后受限于 `double` 类型的精度。例如，尝试这段代码：

| 类型 | 命令 |

|---|---|

| 整数 | Integer |

| 浮点数 | float |

| 字符 | char |

| 布尔 | bool |

| 双精度浮点数 | double |

| 宽字符 | char_t |

| 无值 | void |

```cpp
#include <iostream>
using namespace std;
double PI = 3.14159265358979238463;

int main() {
    cout << PI;
}
```

![](img/0b5e7d59f3578d974082f03180129000_107_0.png)

```cpp
#include <iostream>
using namespace std;
double PI = 3.14159265358979238463;

int main() {
    cout << PI;
}
```

```
C:\Users\Documents\C++-Data.exe
Process Returned (0) execution time: 0.054 s
Press any key to continue...
```

这些基本类型也可以使用修饰符扩展：`Long`、`Short` 和 `Unsigned`。基本上修饰符可以扩展每个数据类型的最小最大范围。例如，`int` 类型的范围是 -2147483648 到 2147483647，这是一个公平的值，你会同意的。现在，如果你使用其中一个修饰符，范围会改变：

- Unsigned int = 0 to 4294967295

- Signed int = -2147483648 to 2147483647

- Signed short = -32768 to 32767

- Unsigned short = 0 to 65535

- Signed short = -32768 to 32767

- Signed long = -2147483648 to 2147483647

- Signed long = -2147483648 to 2147483647

- Unsigned long = 0 to 4294967295

自然，你可以不使用修饰符使用基本类型，因为每个数据类型都有大量的范围值。然而，在可能的情况下修饰符被认为是良好的 C++ 编程。

构建并运行代码，你会发现输出只有 3.141，这代表了 `cout` 在其方面的局限性。你还可以控制上述的 `cout.precision` 以获得更高的精度。使用以下代码将精度提高到 22 位小数：

使用修饰符时存在问题。虽然 `double` 代表双精度浮点，但你可以将其用于：

```cpp
#include <iostream>
using namespace std;
double PI = 3.14159265358979238463;

int main() {}
```

![](img/0b5e7d59f3578d974082f03180129000_107_1.png)

## 数据类型
