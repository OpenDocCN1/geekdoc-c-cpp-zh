
- 将算法的每一步转换为代码。如果它使用了一个尚未声明的软件对象，请添加一条声明语句来指定该对象的类型和名称。

例如，我们可能会这样开始：

```
/* This program converts a Celsius temperature to Fahrenheit.

Written by John Doe for CS 104 -- Project #1 -- Feb. 3, 2012

Input:  the Celsius temperature
Output: the corresponding Fahrenheit temperature
------------------------------------------------------------*/

#include <iostream>    // cin, cout, <<, >>
using namespace std;

int main()
{
}
```

程序以开头文档注释开始，如前一节所述。其后是 iostream 库的 `#include` 指令，该库提供了此指令后面注释中列出的对象（`cin` 和 `cout`）以及运算符（`<<` 和 `>>`）。实现我们算法的 C++ 语句将放置在 `int main()` 后面的花括号（`{` 和 `}`）之间。由于这个程序框架是一个完整的程序，我们可以编译它来检查语法是否正确。如果需要，我们甚至可以执行它，尽管不会产生任何输出。

现在我们继续将算法的各个步骤转换为代码。如果你是编程新手，把算法的步骤（或它们的概要）作为注释实际放在 `main()` 的花括号 `{` 和 `}` 之间，可能会有所帮助：

```
...
int main()
{
    // 1. Output a prompt for the Celsius temperature to cout.
    // 2. Input a real value from cin and store it in celsius.
    // 3. Compute fahrenheit = 1.8 * celsius + 32.
    // 4. Output fahrenheit to cout.
}
```

双斜线（`//`）告知编译器，该行后面的一切都是注释。

现在，我们一次一行地将算法的每一步转换成 C++ 代码。教你掌握能够实现这一转换的 C++ 特性，将是后续各章的目的；现在，我们仅用我们的例子来演示这一转换过程。

算法的第一行可以转换为下面的 C++ 语句：

```
cout << "Enter the Celsius temperature: ";
```

并将其添加到 main 函数中：

```
. . .
int main()
{
    // 1. Output a prompt for the Celsius temperature to cout.
    cout << "Enter the Celsius temperature: ";

    // 2. Input a real value from cin and store it in celsius.
    // 3. Compute fahrenheit = 1.8 * celsius + 32.
    // 4. Output fahrenheit to cout.
}
```

我们现在可以编译这个程序，看看是否存在语法错误；如果没有，则执行它，看看提示信息在屏幕上如何显示：

```
Enter the Celsius temperature:
```

屏幕上的光标将位于这一行的末尾，也就是输入温度值的位置。如果程序没有编译成功——例如，如果我们漏掉了某个双引号（`"`）或语句末尾的分号——我们就需要进行修正，然后重新编译并重新执行修正后的程序。同样，如果我们不喜欢产生的输出——比如，如果我们更希望提示符为“Please enter the temperature in Celsius:”——我们可以进行修改，然后重新编译并重新执行。

一旦我们有了一个可接受的第一条语句，我们就可以继续算法的下一步，并为它编写 C++ 语句：

```
. . .
int main()
{
    // 1. Output a prompt for the Celsius temperature to cout.
    cout << "Enter the Celsius temperature: ";

    // 2. Input a real value from cin and store it in celsius.
    double celsius;
    cin >> celsius;

    // 3. Compute fahrenheit = 1.8 * celsius + 32.
    // 4. Output fahrenheit to cout.
}
```

我们同样可以编译并执行这个新版本的程序。

最终，我们会得到一个完整的程序，如示例 2.2 所示：

### 示例 2.2 温度转换器

```
/* This program converts a Celsius temperature to Fahrenheit.

Written by John Doe for CS 104 -- Project #1 -- Feb. 3, 2012

Input: the Celsius temperature
Output: the corresponding Fahrenheit temperature
-------------------------------------------------------------------*/

#include <iostream> // cin, cout, <<, >>
using namespace std;

int main()
{
    // 1. Output a prompt for the Celsius temperature to cout.
    cout << "Enter the Celsius temperature: ";

    // 2. Input a real value from cin and store it in celsius.
    double celsius;
    cin >> celsius;

    // 3. Compute fahrenheit = 1.8 * celsius + 32.
    double fahrenheit = 1.8 * celsius + 32;

    // 4. Output fahrenheit to cout.
    cout << celsius << " degrees Celsius is equivalent to "
         << fahrenheit << " degrees Fahrenheit.\n";
}
```

可以使用一种称为文本编辑器的软件程序将此程序输入计算机的内存中，并在以后修正发现的任何错误。这种文本编辑器通常内置于 Visual C++ 等编程环境中，但也可能是独立的编辑器，例如 Unix 系统中的 emacs。

### 2.2.4 测试、执行与调试

程序中可能会引入多种错误，包括：

- **语法错误**：当违反编程语言的某些语法规则时产生；
- **运行时错误**：在程序执行过程中发生；以及
- **逻辑错误**：存在于程序所基于的算法的设计中。

查找并修复这些错误被称为调试程序。

当编译器尝试将 C++ 程序翻译成给定计算机的机器语言时，它会定位语法错误，并生成解释（表面）问题的错误消息。例如，如果我们忘记了在示例 2.2 程序中的这一行的末尾输入分号：

```
double celsius;
```

而输入的是：

```
double celsius
```

那么编译器可能会显示如下错误消息：

```
(19) error: missing ';' before identifier 'cin'
```

不同的编译器可能会对同样的错误显示不那么精确的诊断信息，例如：

```
In function 'int main()':
(19) error: expected initializer before 'cin'
```

编译器会显示在检测到问题时正在处理的行的行号，该行紧邻包含错误的行的下一行。学会理解编译器生成的错误消息是一项重要的技能。

第二类错误称为运行时错误，只有在程序执行时才能被检测到。它们包括在算术表达式中除以零、计算负数的平方根以及生成某个超出给定范围的值等情况。一旦确定了错误的原因，就必须用正确的语句或表达式替换有问题的语句或表达式，并重新编译、重新执行修改后的程序。例如，示例 2.2 中的程序包含以下语句：

```
double fahrenheit = 1.8 * celsius + 32.0;
```

但假设我们误读了温度转换公式，在第一个 `*` 运算符的位置键入了 `+` 号：

```
double fahrenheit = 1.8 + celsius + 32.0;
```

因为这是一个合法的 C++ 语句，编译器不会检测到这个错误。程序可以编译并执行，但会产生错误的值，因为用于计算华氏温度的公式不正确。

为了检查逻辑错误，必须使用样本数据运行程序，并检查输出是否正确。这种程序测试应使用多种输入进行多次，以测试程序的不同部分。如果任何输入组合产生了错误的输出，则程序中存在逻辑错误。

一旦确定存在逻辑错误，找到错误所在便是编程中最困难的方面之一。可能有必要逐步跟踪执行过程，直到找到计算值与期望值不同的那个点。为了简化这种跟踪，大多数 C++ 实现都提供了集成的调试器，使程序员可以一次一行地执行程序，观察每一行执行对所生成的值的影响。一旦找到错误，就可以使用文本编辑器进行修正。

应该用几种不同类型的数据（正值、负值、小值、大值等）来测试程序，直到我们有理由相信其正确性为止。然而，几乎不可能用所有可能的测试数据集来测试程序，因此错误可能会在几个月——甚至几年——之后才出现。随着程序规模和复杂性的增长，测试它们的难度也随之增加。无论进行多少测试，总还能进行更多测试。测试永远不会完成，而只是被停止，并且无法保证程序中的所有错误都已被发现和修正。测试只能证明错误的存在，而不能证明错误的不存在。它不能证明程序是正确的，只能证明它是不正确的。

在为编程作业编写的程序中，错误的影响通常并不严重。也许学生只是在该作业上丢掉了几分，或者运气好，评分者甚至没有注意到这个错误。然而，对于现实世界中的问题，面临的利害关系远不止课程成绩——可能是金钱、工作，甚至生命。以下是从大量软件恐怖故事中选取的几个例子：

- 1999 年 9 月，火星气候轨道探测器（Mars Climate Orbiter）撞向火星，未能进入安全轨道。NASA 调查委员会的一份报告指出，该航天器失事的主要原因是地面导航相关任务软件的某一部分未能将火箭推力的测量值从英制单位转换为公制单位。

- 1996 年 6 月，欧洲航天局耗资 70 亿美元研制的无人阿丽亚娜 5 型火箭在首飞升空 37 秒后爆炸。调查委员会的报告指出，故障的原因是惯性参考系统软件中的规格和设计错误导致制导与姿态信息完全丢失。更具体地说，是当一个 64 位浮点数被转换为 16 位整数时发生了运行时错误。

- 1991 年 3 月，DSC Communications 向其贝尔客户交付了一个软件升级，该产品用于大容量电话呼叫路由和交换系统。当年夏天，加利福尼亚州、哥伦比亚特区、马里兰州、弗吉尼亚州、西弗吉尼亚州和宾夕法尼亚州的这些系统发生了重大电话中断事故。事故起因是在修改代码时在信令软件中引入了一个错误：在数百万行代码中更改了三行代码，而该公司认为没有必要重新测试该程序。

- 1991 年 2 月 25 日，海湾战争期间，沙特阿拉伯达兰的一个爱国者导弹防御系统未能跟踪并拦截一枚来袭的飞毛腿导弹。这枚导弹击中了一座美国陆军军营，造成 28 名士兵死亡，98 人受伤。一个错误在
