
要使用列表 6.16 中的程序，你必须先创建一个包含数字的文本文件。你可以使用文本编辑器（例如你编写源码时使用的编辑器）来创建此文件。假设文件名为 `scores.txt` 且内容如下：

18 19 18.5 13.5 14
16 19.5 20 18 12 18.5
17.5

程序必须能够找到该文件。通常情况下，除非你的输入包含文件路径，否则程序将在包含可执行文件的相同文件夹或目录中查找。

> 注意
> Windows 文本文件使用回车符紧随换行符来结束一行文本。（通常的 C++ 文本在读取文件时会将此组合转换为换行符，并在写入文件时反转该转换。）某些文本编辑器（如 Metroworks CodeWarrior IDE 编辑器）不会在最后一行自动添加此组合。因此，如果你使用此类编辑器，需要在退出文件前输入最后一次编辑时按下 Enter 键。

以下是列表 6.16 程序的示例运行：

+ Enter name of data file: `scores.txt`
End of file reached.
Items read: 12
Sum: 204.5
Average: 17.0417

## 程序说明

列表 6.16 中的程序没有硬编码文件名，而是将用户提供的名称存储在字符数组 `filename` 中。然后该数组被作为 `open()` 的参数使用：`inFile.open(filename);`

正如本章早期讨论的那样，测试打开文件的尝试是否成功至关重要。以下是一些可能出现的问题：
- 文件可能不存在。
- 程序可能没有读取该文件的权限。
- 文件可能损坏。
- 输入可能包含非数字数据。
- 文件可能意外结束。

```cpp
while (cin.get(ch))    // quit on eof
{
    if (ch == ' ')
        spaces++;
    else if (ch == '\n')
        newlines++;
}
```

第二种形式相比第一种形式有什么优点？

+ 2. 在列表 6.2 中，将 `++ch` 替换为 `ch+1` 的效果是什么？

+ 3. 仔细考虑以下程序：
```cpp
#include <iostream>
using namespace std;
int main()
{
    char ch;
    int ct1, ct2;
    ct1 = ct2 = 0;
    while ((ch == cin.get()) != '$')
    {
        cout << ch;
        ct1++;
        if (ch == '$')
            ct2++;
        cout << ch;
    }
    cout << "ct1 = " << ct1 << ", ct2 = " << ct2 << "\n";
    return 0;
}
```

假设你提供了以下输入，并在每行末尾按回车键：
Hi!
Send $10 or $20 now!

输出是什么？（回输入是经过缓冲的。）

+ 4. 构建逻辑表达式来表示以下条件：
a. 重量 `weight` 大于或等于 115 但小于 125。
b. `ch` 为 q 或 Q。
c. `x` 是偶数但不是 26。
d. `x` 是偶数但不是 26 的倍数。
e. 捐款 `donation` 在 1,000–2,000 范围内或者 `guest` 等于 1。
f. `ch` 是小写字母或大写字母。（假设像 ASCII 一样，小写字母是连续编码的，大写字母也是连续编码的，但在大写和小写字母之间存在代码隙。）

+ 5. 在英语中，语句“I will not speak”与“I will speak”意思相同。在 C++ 中，`!!=x` 等于 `x` 吗？

+ 6. 构建一个条件表达式，其值等于变量的绝对值。也就是说，如果变量 `x` 为正数，表达式的值为 `x`；但如果 `x` 为负数，表达式的值为 `-x`（即正数）。

+ 7. 使用 `switch` 重写以下代码段：
```cpp
if (ch == 'A')
    a_grade++;
else if (ch == 'B')
    b_grade++;
else if (ch == 'C')
    c_grade++;
else if (ch == 'D')
    d_grade++;
else
    f_grade++;
```

+ 9. 考虑以下代码片段：
```cpp
int line = 0;
char ch;
while (cin.get(ch))
{
    if (ch == 'Q')
        break;
    if (ch != '\n')
        continue;
    line++;
}
```

不使用 `break` 或 `continue` 重写这段代码。

# 编程练习

+ 1. 编写一个程序，将键盘输入读入 `@` 符号中，并回显数字以外的输入，将每个大写字符转换为小写，反之亦然。（不要忘记使用 `ctype` 函数。）

+ 2. 编写一个程序，将最多 10 个捐款值读入一个 `double` 数组中。（或者，如果你喜欢，使用数组模板对象）。程序在遇到非数字输入时终止输入。它应该报告数字的平均值，并报告数组中有多少数字大于平均值。

+ 3. 编写一个菜单驱动程序的雏形。该程序应该显示一个包含四个选择的菜单，每个选择用一个字母标记。如果用户响应的是四个有效选择以外的字母，程序应提示用户输入有效响应，直到用户遵守为止。然后，程序应使用 `switch` 根据用户的选择执行一个简单的操作。程序的运行可能如下：

```
Please enter one of the following choices:
c) carnivore
p) pianist
t) tree
g) game
Please enter a c, p, t, or g: q
Please enter a c, p, t, or g: t
A maple is a tree.
```

+ 4. 当你加入“程序员慈善协会”（Benevolent Order of Programmers）时，你可以在 BOP 会上以你的真实名、职位或你的秘密 BOP 名称身份介绍。编写一个程序，你的真实名可以按真实名、职位、秘密名称或成员偏好列出成员。基于以下结构编写程序：
```cpp
// Benevolent Order of Programmers name structure
struct b {
    char fullname[strsize]; // real name
    char title[strsize]; // job title
    char bopname[strsize]; // secret BOP name
    int preference; // 0 = fullname, 1 = title, 2 = bopname
};
```

在程序中，创建一个此类结构的小数组并将其初始化为合适的值。让程序运行循环，让用户从不同的选项中选择：
- a. 按姓名显示
b. 按职位显示
c. 按 bopname 显示
d. 按偏好显示
q. 退出

# 第 6 章 分支语句和逻辑运算符

注意，“按偏好显示”并不意味着显示 `preference` 成员；而是显示与偏好编号对应的成员。例如，如果 `preference` 为 1，选项 d 将显示程序员的职位。示例运行可能如下：

```
Benevolent Order of Programmers Report
a. display by name      b. display by title
c. display by bopname      d. display by preference
q. quit
Enter your choice: a
Wimp Macho
```

5. 中特托尼亚王国（Kingdom of Neutonia）的货币单位如下：
- 5,000: 0% 税
- 10,000: 10% 税
- 20,000: 15% 税
- 30,000: 20% 税
- 40,000: 25% 税
- 50,000: 30% 税
- 60,000: 35% 税
- 70,000: 40% 税
- 80,000: 45% 税
- 90,000: 50% 税
- 100,000: 55% 税
- 110,000: 60% 税
- 120,000: 65% 税
- 130,000: 70% 税
- 140,000: 75% 税
- 150,000: 80% 税
- 160,000: 85% 税
- 170,000: 90% 税
- 180,000: 95% 税
- 190,000: 100% 税
- 200,000: 105% 税

6. 编写一个程序来跟踪捐款。使用结构数组。每个结构应该有一个字符数组（或字符串对象）来存储名称，以及 `double` 成员来持有金额。在读取所有数据后，程序应列出捐赠 10,000 元或以上的。该列表应以“Patrons”（赞助人）为标题。

7. 编写一个程序读取输入，直到输入单独的 `q`。程序应报告元音的数量、辅音的数量以及其他的数量。示例运行可能如下：
```
Enter words (q to quit):
the awesome
quietly across
q
5 vowels
4 consonants
2 others
```

8. 编写一个程序打开一个文本文件，逐字符字符读取到文件末尾，并报告文件中的字符数。

9. 完成编程练习 6，但修改为从文件获取信息。文件中的第一个项目是贡献者的数量，文件的其余部分由行对组成，每对的第一行是贡献者的名字，第二行是捐赠金额。也就是说，文件应该是这样的：
```
4
Sam Stone
2000
Freida Flass
100500
Tammy Tubbs
5000
Rich Raptor
55000
```

306 第 7 章 函数：C++ 的编程模块

## 函数回顾

让我们回顾一下你已经学过的函数知识。要使用 C++ 函数，你必须执行以下操作：
- 提供函数的定义 `definition`
- 提供函数的声明 `prototype`
- 调用该函数

如果你使用的是库函数，该函数已经为你为你定义并编译好了。此外，你也可以并且应该使用标准库头文件来提供函数类型。你做的就是调用函数声明。本书到为止的示例已经多次演示了这一点。例如，标准 C 库包含了用于查找字符串长度的 `strlen()` 函数。相关的标准头文件 `string` 包含了 `strlen()` 以及其他字符串相关函数的声明。这种优势允许你可以在程序中使用 `strlen()` 而无需再担心其他问题。

但当你创建自己的函数时，你必须自己处理所有方面的工作——定义、声明和调用。列表 7.1 用一个简短的示例展示了这些步骤。

## 列表 7.1 calling.cpp
```cpp
// calling.cpp -- 定义、声明和调用一个函数
#include <iostream>
void simple(); // 函数声明
int main() {
    using namespace std;
    cout << "main() will call the simple() function:\n";
    simple(); // 函数调用
    cout << "main() is finished with the simple() function.\n";
    cin.get();
    return 0;
}
// 函数定义
void simple() {
    using namespace std;
    cout << "I'm but a simple function.\n";
}
```

## 函数回顾
307

以下是列表 7.1 中程序的输出：
```
main() will call the simple() function:
I'm but a simple function.
main() is finished with the simple() function.
```

当转移到 `simple()` 函数时，`main()` 中的程序执行停止。当 `simple()` 完成，`main()` 中的程序执行继续。这个示例在每个函数定义内部放置了 `using` 指令，因为每个函数都使用了 `cout`。或者，程序也可以函数定义上方放置单个 `using` 指令，或者直接使用 `std::cout`。

让我们详细查看这些步骤。

## 定义函数

你可以将函数分为两类：没有返回值的函数和有返回值的函数。没有返回值的函数被称为 `void` 类型函数，具有以下通用形式：
```cpp
void functionName(parameterList)
{
    statement(s)      // 可选
    return;
}
```

在这里，`parameterList` 指定了传递给函数的参数的类型和数量。本章稍后会更更深入地研究这个列表。可选的 `return` 语句标记函数的结束。否则，函数在右括号处终止。`void` 函数对应于 Pascal 过程、FORTRAN 子程序和现代 BASIC 子程序过程。通常，使用 `void` 函数来执行某种操作。例如，一个按指定次数（`n`）打印 *Cheers!* 的函数看起来可能像这样：
```cpp
void cheers(int n)      // 无返回值
{
    for (int i = 0; i < n; i++)
        std::cout << "Cheers!";
        std::cout << std::endl;
}
```

参数列表 `n` 意味着当你调用此函数时，`cheers()` 期望有一个 `int` 类型的值作为参数传递给它。

带有返回值的函数会产生一个值并将其返回给调用它的函数。换句话说，如果函数返回 9.0 的平方根（`sqrt(9.0)`），那么该函数调的值就是 3.0。此类函数声明为与它返回的值相同的类型。其通用形式是：
```cpp
typeName(parameterList)
{
    statements
    return value; // value 被强制转换为类型 typeName
}
```

带有返回值的函数要求你使用 `return` 语句，以便将值返回给调用它的函数。该值本身可以是常量、变量或更通用的表达式。唯一的要求是该表达式必须归约为值，并且可以转换为 `typeName` 类型。（如果声明的返回类型是 `double`，而函数返回一个 `int` 表达式，则该值会被强制转换为 `double` 类型。）该函数将最终值返回给它所调用的函数。C++ 也对你可以用于返回值的类型施加了限制：返回值不能是任何东西。万物皆可能的——整数、浮点数、指针，甚至是结构和对象！（有趣的是，尽管 C++ 函数不能直接返回数组，但它可以返回结构或对象中数组的一部分）。

作为程序员，你不需要知道函数是如何返回值的，但了解这种方法可能会让你更清楚这个概念。通常，函数通过将返回值复制到特定的 CPU 寄存器或内存位置来返回值。然后调用程序检查该位置。返回值的函数和调用的函数必须对该位置的数据类型达成一致。函数声明告诉调用程序应该期望什么，而函数定义告诉调用程序要返回什么（见图 7.1）。在声明和定义中提供相同的信息似乎是多余的工作，但它很有道理。当然，如果你想让快递员从你办公室的桌子上取点东西，如果你提供了关于你想让他们携带的物品的描述并告诉办公室的某人，就会增加任务正确完成的几率。

函数在执行 `return` 语句后终止。如果一个函数有多个 `return` 语句——例如，作为 `if else` 选择的替代方案——函数会在执行完它遇到的第一个 `return` 语句后终止。例如，在下面的示例中：
```cpp
int bigger(int a, int b) {
    if (a > b)
        return a;
    else
        return b;
}
```

在上面的例子中，如果 `a > b`，函数将返回 `a` 并终止。如果 `a` 不大于 `b`，函数将执行 `else` 分支并返回 `b`。

## 函数回顾
309
```cpp
int bigger(int a, int b) {
    if (a > b)
        return a;
    else
        return b;
}
```

这里是 `main()` 函数调用 `bigger(10, 20)` 的示例：
```cpp
int bigger(int a, int b) {
    if (a > b)
        return a;
    else
        return b;
}
int main() {
    using namespace std;
    cout << "The bigger value of 10 and 20 is " << bigger(10, 20) << endl;
    return 0;
}
```

输出：
```
The bigger value of 10 and 20 is 20
```

## 声明与调用函数

现在你已经熟悉函数调用了，但你可能对函数声明不太熟悉，因为通常隐藏在包含文件中。列表 7.2 展示了程序中使用的 `cheers()` 和 `cube()` 函数；注意函数声明。

310 第 7 章 函数：C++ 的编程模块

## 列表 7.2 protos.cpp
```cpp
// protos.cpp -- 使用声明和函数调用
#include <iostream>
void cheers(int);      // 声明：无返回值
double cube(double x); // 声明：有返回值
int main()
{
    using namespace std;
    cheers(5);
    cout << "Give me a number: *";
