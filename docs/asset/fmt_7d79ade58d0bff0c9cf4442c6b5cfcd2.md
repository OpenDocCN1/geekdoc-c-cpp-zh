
由于`cout`是预定义类的对象，你不需要创建它；只需正确激活它即可使用。像所有的 C++ 对象一样，`cout`只能执行某些定义良好的操作。对于`cout`来说，操作是组用于输出显示的数据。当字符串发送到`cout`时，该对象确保字符串在屏幕上正确显示，如程序 2.1 的输出所示：

```
Hello world!
```

# 使用 C++ 解决问题

C++ 中的字符串是任何字母、数字和特殊字符的组合，并包含在引号（`"string in here"`）中。引号界定（标记）字符串的开始和结束，而不被视为字符串的一部分。发送给`cout`的消息字符字符串必须包含在引号中，如程序 2.1 所示。

现在让我们另一个另一个程序以理解`cout`的多功能性。阅读程序 2.2 以确定它的功能。

![](img/023360499b401b1e52ce9fc94a17f42d_69_0.png)

### 程序 2.2

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Computers, computers everywhere";
    cout << "\n as far as I can C";

    return 0;
}
```

当运行程序 2.2 时，将显示以下内容：

```
Computers, computers everywhere
as as far as I can C
```

你可能在奇怪为什么`\n`没有出现在输出中。字符`\`和`n`在使用时被称为“换行序列”。它们告诉`cout`向显示设备发送指令，移动到新行的开头。否则，第二个`cout`语句将简单地追加在上一个语句的字符之后；它本身不会在一个新行开始。在 C++ 中，反斜杠（`\`）提供了对其后续字符正常解释的“转义”，并改变了它的含义——在这种情况下，是`n`。如果从程序 2.2 的第二个`cout`语句中省略反斜杠，`n`将作为字母 "n" 打印，程序将输出以下内容：

```
Computers, computers everywhere as far as I can C
```

换行转义序列可以放在发送给`cout`的消息的任何位置。你能否确定程序 2.3 产生的显示。

# 第 2 章 51

C++ 导论

### 程序 2.3

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Computers everywhere\n as far as\nI can see";

    return 0;
}
```

这是程序 2.3 的输出：

```
Computers everywhere
as far as
I can see
```

### 练习题 2.1

- 1. (练习) 判定以下函数名是否有效，如果是，说明它们是否是能够传达函数目的某些思想的助记名。如果是无效名称，请说明原因。

| power density | m1234 | newamp | 1234 | abcd |
| :--- | :--- | :--- | :--- | :--- |
| total tangent | abnaval | computed | b3b4 | 34ab |
| volts$ | a2b3 | while | minVal | $sine |
| cosine | speed | netdistance | return | stack |

- 2. (练习) 假设已编写了以下函数：`getLength()`、`getWidth()`、`calcArea()`、`displayArea()`。

- a. 从函数名称，你认为每个函数可能会做什么？

- b. 你认为`main()`函数可能会以什么顺序执行这些函数（基于它们的名称）？

- 3. (练习) 假设已编写了以下函数：`speed()`、`distance()`、`acceleration()`。

从函数名称，你认为每个函数可能会做什么？

# 52 使用 C++ 解决问题

- 4. (练习) 为执行以下功能的函数命名：

- a. 找到一组数字的平均值。

- b. 找到矩形的面积。

- c. 找到一组数字中的最小值。

- d. 找到钢门的密度。

- e. 将一组数字从低到高进行排序。

- 5. (程序) a. 使用`cout`编写一个 C++ 程序，在第一行显示你的名字，在第二行显示你的街道地址，在第三行显示你的城市和邮政编码。

- b. 运行你为练习 5a 编写的程序。（注意：你必须了解在特定的计算机安装上输入和运行 C++ 程序的步骤。）

- 6. (程序) a. 编写一个 C++ 程序显示以下输出：

```
一个角度的余割等于角度正弦的倒数。
```

- b. 编译并运行你为练习 6a 编写的程序。

- 7. (程序) a. 你将使用多少个`count`语句来显示以下输出？

| Degrees | Radians |
| :--- | :--- |
| 0 | 0.0000 |
| 180 | 1.5708 |
| 270 | 4.7214 |
| 360 | 6.2832 |

- b. 用于打印练习 7a 中的输出的最少需要多少个`count`语句？

- c. 编写一个完整的 C++ 程序产生练习 7a 所示的输出。

- d. 运行你为练习 7c 编写的程序。

- 8. (程序) a. 假设你的编译器不区分大小写，这些程序名称中哪些是等价的？

| AVERAG | MODE | BESSEL | Mode |
| :--- | :--- | :--- | :--- |
| Total | bessel | Temp | Densty | TEMP |
| denSTY | MEAN | total | mean | mode |

- b. 重做练习 8a。

### 项目结构化

大多数项目，包括编程和重编程，通常可以分解为更小的子任务。这些子任务可以委托给他人，以便项目能够完成。对于练习 9 到 14，确定一组共同执行即可完成项目的子任务。

# 第 2 章 编程风格 53

**注意：** 这些练习的目的是让你考虑组织任务的不同方式。虽然这些练习没有唯一的正确答案，但存在错误的解决方案。错误的解决方案是不完整指定任务的。一个解决方案比另一个更清晰或更容易识别出必须完成。

- 9. (练习) 你被分配的任务是在家里布线和安装灯具。确定一组子任务以完成此任务。（提示：第一个子任务是确定灯具的位置）。

- 10. (练习) 你被分配的任务是周末为五个人准备一餐。确定一组子任务以完成此任务。（提示：不一定是第一个是购买食物）。

- 11. (练习) 你是大学大二学生，计划读研究生院，你必须完成的目标列表。（提示：一个子任务是“确定应该上的课程。”）

- 12. (练习) 你被分配的任务是规划一个蔬菜园。确定一组子任务以完成此任务。（提示：一个子任务是规划花园的布局）。

- 13. (练习) 你负责规划今年夏天的家庭露营活动。确定一组子任务以完成此任务。（提示：一个子任务是选择营地）。

- 14. (数据处理) a. 国家医学实验室需要一个新的计算机系统来分析其测试结果。该系统必须能够处理每天的结果，还可以检索并输出符合某些标准的打印报告，例如针对特定医生或某个州的医院。确定可以将该系统分解为三个或多个程序单元（提示：可能的单元是“准备每日结果”以创建每天的结果）。

b. 假设有人输入了测试结果数据，在系统输入并存储了数据后发现了错误。需要什么程序单元来纠正这个问题？讨论为什么许多系统可能或不需要程序单元。

c. 假设存在一个允许用户更改已输入并存储数据的程序单元。讨论包含“审计追踪”的必要性，以便以后能够重建在何时以及如何进行的更改。

C++ 程序从`main()`函数开始开始。因为一个程序只能有一个起点，所以每个 C++ 程序必须包含且仅包含`main()`函数。正如你所看到的，构成`main()`函数的所有语句都包含在函数名称后面的括号内。虽然每个 C++ 程序都必须包含`main()`函数，但 C++ 不要求将`main`单词、括号或括号以任何特定形式呈现。上一节中使用的形式

```cpp
int main()
{
    program statements in here;

    return 0;
}
```

这种选择完全是为了程序的清晰清晰和易于阅读，但并非强制要求。例如，以下`main()`函数的通用形式也可以运行：

```cpp
int main()
{ } { first statement;second statement;
    third statement;fourth
statement;
    return 0;}
```

请注意，你可以在同一行放置多个语句，也可以将一个语句跨越多行。除了字符串、引号和标识符外，C++ 会忽略所有的空白字符。（空白字符是指任何空格、制表符或换行符的组合。）例如，更改程序 2.1 中的空白字符，并确保不将字符串`Hello world!`拆分成两行，可以得到以下有效的程序：

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout <<
    "Hello world!"
    return 0;
}
```

虽然这个版本的`main()`可以工作，但它是糟糕编程风格的示例，因为它难以阅读和理解。为了可读性，`main()`函数应该始终按照这种标准格式编写：

```cpp
int main()
{
    program statements in here;

    return 0;
}
```

在这种标准形式中，函数名从左对齐线开始（称为第 1 列），并带有所需的括号单独占一行。函数体的左大括号紧随其后位于下一行的第 1 列，直接对齐包含函数名那行的第一个字母。同样地，右大括号被单独放在第 1 列（与左大括号对齐），作为函数的最后一行。这种结构将函数作为一个单一单元凸显出来。

在函数内部，所有程序语句至少缩进两个空格。缩进是良好编程习惯的另一个标志，特别是当相似的语句组使用相同的缩进时。复习程序 2.2，可以看到两个`cout`语句使用了相同的缩进。

# 第 2 章 55 页

随着你对 C++ 的理解和掌握不断加深，你将形成自己的缩进标准。只需记住，你程序的最终形式应该保持一致，并始终能帮助他人阅读和理解你的程序。

### 注释

注释是程序中的说明性备注。当谨慎使用时，注释有助于明确程序的整体目的，解释一组学生应该完成什么，或者解释某人意图做什么。C++ 支持两种类型的注释：行注释和块注释。这两种类型都可以放置在程序的任何位置，且对程序执行没有影响。编译器会忽略所有注释——它们严格为了任何阅读程序的人的方便。

行注释以两个斜杠（`//`）开始，并一直持续到行的末尾。例如，以下示例是行注释：

```cpp
// this is a comment
// this program prints out a message
// this program calculates a square root
```

符号`//`之间没有空格，表示行注释的开始。注释所在所在行的末尾即为注释的结束。行注释可以单独占一行，也可以写在包含程序语句的行尾。程序 2.4 显示了程序中的行注释。

![](img/023360499b401b1e52ce9fc94a17f42d_74_0.png)

### 程序 2.4

```cpp
// this program displays a message
#include <iostream>
using namespace std;

int main()
{
	cout << "Hello there world!"; // this produces the display

	return 0;
}
```

第一个注释单独占一行或位于程序末尾，这一行是描述程序目的的良好注释处。如果需要更多注释，可以将它们放在每行，就像在`cout`语句之后一样。当注释长到无法放在一行时，每行都以`//`符号开头。例如，以下注释是非的，因为第二行没有以`//`开头：

```cpp
// this comment is invalid because it
extends two lines
```

# 使用 C++ 解决问题

以下注释是正确的：

```cpp
// this comment is used to illustrate
// comment that extends across two lines
```

跨行的注释方便地写成块注释，它们由符号`/*`定义并以`*/`结束，如下：

```cpp
/* This is a block comment
spanning three lines */
```

在 C++ 中，程序的结构旨在使其易读易懂，因此详细的注释是必要的。这一指南通过仔细选择函数名来传达目的得到了强化。如果程序的结构或上下文仍然不清晰，在需要的地方添加注释。

没有注释的晦涩代码是糟糕编程的标志，特别是当其他人必须维护或阅读程序时。同样，过度注释也是糟糕编程的标志，因为对编写程序缺乏足够的思考。任何程序都应该包含简短的描述、你的名字以及编写日期。这些初始注释仅作为传递给`cout`的消息的一部分使用。

![](img/023360499b401b1e52ce9fc94a17f42d_75_0.png)

### 练习 2.2

2. （修改）重写程序以符合编程习惯和语法：

a. 

```cpp
#include <iostream>
int main()
{
    cout << "The time has come";
	return 0;
}
```

b. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "New York is a city";
	return 0;
}
```

c. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "It is also a city";
	return 0;
}
```

d. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "Reading a program";
	return 0;
}
```

e. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "if a standard form for main is used";
	return 0;
}
```

f. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "and each statement is written";
	return 0;
}
```

g. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "on a line by itself";
	return 0;
}
```

h. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "Every C++ program";
	return 0;
}
```

i. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "must have one and only one";
	return 0;
}
```

j. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "main function";
	return 0;
}
```

k. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "the sequence of characters";
	return 0;
}
```

l. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "for a new line can be placed anywhere";
	return 0;
}
```

m. 

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "within the message passed to cout";
	return 0;
}
```

（思考）当使用块注释时，它会改变紧随其后的字符的含义。如果你想打印一个字符，必须告诉`cout`跳出它通常解释方式。你想使用什么字符来改变字符的解释方式？使用你的练习 3a，编写打印`a`的转义序列。

（思考）a. 计算机语言的标记（token）是任何字符序列，中间没有插入的字符或空白，作为一个单元具有独特的含义。使用这个标记的定义，确定转义序列、函数名和表 2.1 列出的关键字是否为 C++ 语言的标记。b. 讨论空白是否会改变消息，以及消息是否可以被视为 C++ 的标记。c. 使用练习 4a 中标记的定义，判断以下语句是否正确：“除了语言标记外，C++ 忽略所有的空白字符。”

# 第 2 章

## 2.3 数据类型

所有程序的目标都是处理数据，无论是数字、字母、音频还是视频。这一目标的核心是将数据分类为特定类型。例如，计算火箭的轨迹需要对数值数据进行数学运算，对姓名列表进行排序需要对基于字符的数据进行比较运算。此外，操作不适用于某些类型的数据。例如，将名称相加没有意义。为了防止程序员尝试执行不当的操作，C++ 允许仅对某些类型的数据执行某些操作。
