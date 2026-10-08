

# 第 12 章 二维数组

| 天数 | 最高 | 最低 |
|---|---|--|
| 1 | 95 | 67 |
| 2 | 98 | 54 |
| 3 | 86 | 70 |
| 4 | 99 | 56 |
| 5 | 83 | 34 |
| 6 | 75 | 68 |
| 7 | 80 | 45 |

图 12-27

- 22. 在此练习中，你将修改计算机练习 21 中的程序。如有必要，创建一个名为 Intermediate22 的新项目。将 `Intermediate22.cpp` 文件中的指令复制到源文件 `Intermediate22.cpp` 中。更改第一个注释中的文件名。除了显示平均最高气温和平均最低气温外，程序还应该显示存储在第一列和第二列中的最高温度和最低温度。保存并运行程序。使用图 12-27 显示的数据测试程序。

- 23. 按照启动 C++ 并打开 `Advanced23.cpp` 文件的说明进行。该文件位于 `Cpp6/Chapter12/Advanced23` 项目文件夹或 `Cpp6/Chapter12` 文件夹中。编写程序，要求用户输入每个价格应增加的金额。程序随后增加第一列中的每个价格。例如，当用户输入数字 10 时，程序将每个值增加 10 美元。将更新后的价格存储在数组的第二列。在增加每个价格后，程序应按行显示数组的内容。保存并运行程序。将每个价格增加 10 美元。

- 24. 在此练习中，编写一个应用程序，显示某个值在二维数组中出现的次数。按照启动 C++ 并打开 `Advanced24.cpp` 文件的说明进行。该文件位于 `Cpp6/Chapter12/Advanced24` 项目文件夹或 `Cpp6/Chapter12` 文件夹中。编写程序，使其显示从 1 到 9 的每个数字在数组中出现的次数（提示：使用一个计数变量的一维数组）。保存并运行程序。

- 25. 如必要，创建一个名为 Advanced25 的新项目。创建一个新的源文件 `Advanced25.cpp`。JM 在一月、二月和三月的销售额如图 12-28 所示。将销售额存储在二维数组中。程序管理一个应用程序，允许他输入当前奖率。程序应显示每个销售人员的编号（1 到 10）、总销售额和总奖金。它还应该显示支付给所有销售人员的总奖金。金额保留两位小数。保存并运行程序。使用 10% 的奖率测试程序。

# 练习

| 销售人员 | 一月 | 二月 | 三月 |
| --- | --- | --- | --- |
| 1 | 2400 | 3500 | 2000 |
| 2 | 1500 | 7000 | 1000 |
| 3 | 600 | 450 | 2100 |
| 4 | 790 | 240 | 500 |
| 5 | 1000 | 1000 | 1000 |
| 6 | 6300 | 7000 | 8000 |
| 7 | 1300 | 450 | 700 |
| 8 | 2700 | 5500 | 6000 |
| 9 | 4700 | 4800 | 4900 |
| 10 | 1200 | 1300 | 500 |

图 12-28

- 26. 按照启动 C++ 并打开 `StuBugs26.cpp` 文件的说明进行。该文件位于 `Cpp6/Chapter12/StuBugs26` 项目文件夹或 `Cpp6/Chapter12` 文件夹。调试程序。

# 练习答案

## 笔练习

1. `double balances[4][6] = {0};`
2. `for (int row = 0; row < 4; row++)`
   `for (int col = 0; col < 6; col++)`
   `cout << balances[row][col] << endl;`
   也可以使用 `row++` 和 `col++`。
15. 图 12-29。

## 计算机

```cpp
// Try15.cpp
// 显示二维数组的内容
// 由 <name> 创建 <current date>

#include <iostream>
using namespace std;

int main() {
    // 声明并初始化数组
    int orders[4][3] = {0};

    // 输入数据
    int region = 0;
    int month = 0;
    while (region < 4) {
        while (month < 3) {
            cout << "Number of orders for Region " << region + 1 << ": ";
            cin >> orders[region][month];
            month++;
        }
        month = 0;
        region++;
    }
    // 显示数组的内容
    region = 0;
    month = 0;
    while (region < 4) {
        cout << "Region " << region + 1 << ":" << endl;
        while (month < 3) {
            cout << "Month " << month + 1 << ": " << endl;
            cout << orders[region][month] << endl;
            month++;
        }
        region++;
    }
    system("pause");
    return 0;
} // main 函数
```
你也可以在第 24 和 42 行使用 `month++`，在第 26 和 44 行使用 `region++`。

```cpp
// Try16.cpp
// 显示二维数组的内容
// 由 <name> 创建 <current date>

#include <iostream>
using namespace std;

// 函数原型
void displayArray(int nums[][], int numRegions);

int main() {
    // 声明并初始化数组
    int orders[4][3] = {0};

    // 输入数据
    for (int region = 0; region < 4; region++) {
        for (int month = 0; month < 3; month++) {
            cout << "Number of orders for Region " << region + 1 << " Month " << month + 1 << ": ";
            cin >> orders[region][month];
        }
    }

    // 显示数组的内容
    displayArray(orders, 4);
    return 0;
} // main 函数

**** 函数定义 ****
void displayArray(int nums[][], int numRegions) {
    for (int region = 0; region < numRegions; region++) {
        cout << "Region " << region + 1 << endl;
        for (int month = 0; month < 3; month++) {
            cout << "Month " << month + 1 << ": ";
            cout << nums[region][month] << endl;
        }
    }
} // displayArray 函数
```
图 12-30

---分页

# 字符串

学习第 13 章后，你应该能够：
- 在程序中使用字符串位置
- 使用 `getline` 函数获取字符串输入
- 使用 `ignore` 函数忽略字符
- 确定字符串字符数量
- 访问字符串中的字符
- 搜索字符串
- 从字符串中删除字符
- 替换字符串中的字符
- 在字符串中插入字符
- 重复字符串中的字符
- 拼接字符串

# string 数据类型

## 如何声明和初始化字符串变量和常量

示例 1
`string zipCode = "";`
声明并初始化字符串变量 `zipCode`。

示例 2
`string playAgain = "Y";`
声明并初始化名为 `playAgain` 的字符串变量。

示例 3
`const string VALID_LENGTH = "Valid length";`
声明并初始化名为 `VALID_LENGTH` 的常量。

示例 4
`const string COMPANY_NAME = "ABC Company";`
声明并初始化名为 `COMPANY_NAME` 的常量。

> 存储图 13-1 每个示例中字符串所需的内存不同，并由 `string` 类管理。

> 你在第 3 章学过空字符串。

图 13-1 如何声明和初始化字符串变量和常量

类也被称为用户定义数据，它们允许程序员通过定义新数据类型（类）的特征和属性来扩展 C++ 语言。通常，特征和属性与类相关。所有行为都实现为与每个类相关的成员函数。因此，每个类都有自己的一套成员函数。在本章中，你将探索与 `string` 类的一些常用的成员函数。

# Creative Sales 程序

图 13-2 显示了 Creative Sales 程序的问题规范和 IPO 图，该程序从键盘获取销售人员姓名和销售金额。它计算销售人员的奖金并在屏幕上显示销售人员姓名和奖金金额。

Creative Sales 希望销售经理输入销售人员姓名和销售金额。程序应通过将销售金额乘以 10% 来计算销售人员的奖金。然后在屏幕上显示销售人员姓名和奖金金额。

| 问题规范 | 处理 | 输出 |
| --- | --- | --- |
| | 处理项目：无 | 名称 |
| 销售率 (10%) | 算法：<br> 1. 输入姓名和销售额<br> 2. 将销售额乘以率计算奖金<br> 3. 显示姓名和奖金 | | |

图 13-2 Creative Sales 程序的问题规范和 IPO 图

到目前为止，你使用提取运算符 (>>) 从键盘获取用户获取数字和字符。提取运算符也可以从键盘获取字符串输入，如图 13-3 示例所示。（为了清晰起见，示例包含了声明语句。）但是，请记住提取运算符在遇到输入中的空白字符时停止读取。空白字符是空格、制表符或换行符。当你按下键盘上的空格键时输入空白字符。当你按下 Tab 键时输入制表符，按下回车键时输入换行符。如果用户在示例 1 中意外输入字符串 "43602"（而不是 45602）作为邮政编码，`cin >> zipCode;` 语句中的提取运算符将仅把 "43" 在 `zipCode` 变量中。

你在第 4 章学过提取运算符。

> 如何使用提取运算符 (>>) 获取字符串输入
示例 1
`string zipCode = "";`
`out << "Enter your zip code: \

图 13-3 如何使用提取运算符 (>>) 获取字符串输入

