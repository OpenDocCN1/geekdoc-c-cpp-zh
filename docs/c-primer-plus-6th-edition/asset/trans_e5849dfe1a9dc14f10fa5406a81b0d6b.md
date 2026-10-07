

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
a. 重量 weight 大于或等于 115 但小于 125。
b. ch 为 q 或 Q。
c. x 是偶数但不是 26。
d. x 是偶数但不是 26 的倍数。
e. 捐款 donation 在 1,000–2,000 范围内或者 guest 等于 1。
f. ch 是小写字母或大写字母。（假设像 ASCII 一样，小写字母是连续编码的，大写字母也是连续编码的，但在大写和小写字母之间存在代码隙。）

+ 5. 在英语中，语句“I will not speak”与“I will speak”意思相同。在 C++ 中，`!!=x` 等于 `x` 吗？

+ 6. 构建一个条件表达式，其值等于变量的绝对值。也就是说，如果变量 x 为正数，表达式的值为 x；但如果 x 为负数，表达式的值为 -x（即正数）。

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

+ 1. 编写一个程序，将键盘输入读入 @ 符号中，并回显数字以外的输入，将每个大写字符转换为小写，反之亦然。（不要忘记使用 ctype 函数。）

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

注意，“按偏好显示”并不意味着显示 preference 成员；而是显示与偏好编号对应的成员。例如，如果 preference 为 1，选项 d 将显示程序员的职位。示例运行可能如下：

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

7. 编写一个程序读取输入，直到输入单独的 q。程序应报告元音的数量、辅音的数量以及其他的数量。示例运行可能如下：
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

