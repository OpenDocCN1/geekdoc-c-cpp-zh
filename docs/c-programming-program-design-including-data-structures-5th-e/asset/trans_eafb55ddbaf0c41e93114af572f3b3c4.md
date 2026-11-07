
```cpp
int main()
{
    //Declare variables
    int feet, inches;
    int totalInches;
    double centimeter;

    //Statements: Step 1 - Step 7
    cout << "Enter two integers, one for feet and "      //Step 1
         << "one for inches: ";
    cin >> feet >> inches;                              //Step 2
    cout << endl;
    cout << "The numbers you entered are " << feet
         << " for feet and " << inches
         << " for inches. " << endl;                    //Step 3

    totalInches = INCHES_PER_FOOT * feet + inches;      //Step 4

    cout << "The total number of inches = "
         << totalInches << endl;                        //Step 5

    centimeter = CENTIMETERS_PER_INCH * totalInches;    //Step 6

    cout << "The number of centimeters = "
         << centimeter << endl;                         //Step 7

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

输入两个整数，一个表示英尺，一个表示英寸：**15 7**

你输入的数字是：15 英尺和 7 英寸。
总英寸数 = 187
厘米数 = 474.98

## 编程示例：找零

编写一个程序，输入任意以美分表示的零钱。然后计算应找回的半美元、25美分硬币、10美分硬币、5美分硬币和1美分硬币的数量，按顺序尽可能多地返回半美元，然后依次是25美分硬币、10美分硬币、5美分硬币和1美分硬币。例如，483美分应找回9个半美元、1个25美分硬币、1个5美分硬币和3个1美分硬币。

- **输入：** 以美分表示的零钱。
- **输出：** 等值的半美元、25美分硬币、10美分硬币、5美分硬币和1美分硬币零钱。

### 问题分析与算法设计

假设给定的零钱是646美分。要找出半美元的数量，你用646除以50（一个半美元的值），得到商12和余数46。商12就是半美元的数量，余数46就是剩余的零钱。

接下来，用剩余的零钱除以25来找出25美分硬币的数量。由于剩余零钱是46，除以25得到商1，即25美分硬币的数量，余数为21，即剩余的零钱。对10美分硬币和5美分硬币重复此过程。要计算整数除法中的余数，使用取模运算符 %。

将上述讨论应用于646美分，得到以下计算：

- 1. 零钱 = 646
- 2. 半美元数量 = 646 / 50 = 12
- 3. 剩余零钱 = 646 % 50 = 46
- 4. 25美分硬币数量 = 46 / 25 = 1
- 5. 剩余零钱 = 46 % 25 = 21
- 6. 10美分硬币数量 = 21 / 10 = 2
- 7. 剩余零钱 = 21 % 10 = 1
- 8. 5美分硬币数量 = 1 / 5 = 0
- 9. 1美分硬币数量 = 剩余零钱 = 1 % 5 = 1

此讨论转化为以下算法：

- 1. 获取以美分表示的零钱。
- 2. 找出半美元的数量。
- 3. 计算剩余零钱。
- 4. 找出25美分硬币的数量。
- 5. 计算剩余零钱。
- 6. 找出10美分硬币的数量。
- 7. 计算剩余零钱。
- 8. 找出5美分硬币的数量。
- 9. 计算剩余零钱，即1美分硬币的数量。

### 变量

从前面的讨论和算法来看，程序似乎需要变量来保存半美元、25美分硬币等的数量。然而，半美元、25美分硬币等的数量不会在后续计算中使用，因此程序可以直接输出这些值，而不必将每个值都保存在变量中。唯一不断变化的是零钱，所以程序实际上只需要一个变量：

```c
int change;
```

### 命名常量

为了计算等值零钱，程序使用半美元的值50、25美分硬币的值25、10美分硬币的值10和5美分硬币的值5进行计算。由于这些数据很特殊，而且程序会多次使用这些值，因此将它们声明为命名常量是合理的。使用命名常量还简化了以后对程序的修改：

```cpp
const int HALF_DOLLAR = 50;
const int QUARTER = 25;
const int DIME = 10;
const int NICKEL = 5;
```

### 主算法

- 1. 提示用户输入。
- 2. 获取输入。
- 3. 通过在屏幕上显示输入的零钱来回显输入。
- 4. 计算并打印半美元的数量。
- 5. 计算剩余零钱。
- 6. 计算并打印25美分硬币的数量。
- 7. 计算剩余零钱。
- 8. 计算并打印10美分硬币的数量。
- 9. 计算剩余零钱。
- 10. 计算并打印5美分硬币的数量。
- 11. 计算剩余零钱。
- 12. 打印剩余零钱。

### 完整程序清单

```cpp
//**************************************************************
// Author: D. S. Malik
//
// Program Make Change: Given any amount of change expressed
// in cents, this program computes the number of half-dollars,
// quarters, dimes, nickels, and pennies to be returned,
// returning as many half-dollars as possible, then quarters,
// dimes, nickels, and pennies in that order.
//**************************************************************

    //Header file
#include <iostream>

using namespace std;

    //Named constants
const int HALF_DOLLAR = 50;
const int QUARTER = 25;
const int DIME = 10;
const int NICKEL = 5;

int main()
{
        //Declare variable
        int change;

        //Statements: Step 1 -- Step 12
        cout << "Enter change in cents: ";                 //Step 1
        cin >> change;                                     //Step 2
        cout << endl;

        cout << "The change you entered is " << change
             << endl;                                      //Step 3

        cout << "The number of half-dollars to be returned "
             << "is " << change / HALF_DOLLAR
             << endl;                                      //Step 4

        change = change % HALF_DOLLAR;                     //Step 5

        cout << "The number of quarters to be returned is "
             << change / QUARTER << endl;                  //Step 6

        change = change % QUARTER;                         //Step 7

        cout << "The number of dimes to be returned is "
             << change / DIME << endl;                     //Step 8

        change = change % DIME;                            //Step 9

        cout << "The number of nickels to be returned is "
             << change / NICKEL << endl;                   //Step 10

        change = change % NICKEL;                          //Step 11

        cout << "The number of pennies to be returned is "
             << change << endl;                            //Step 12

        return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```text
Enter change in cents: 583
```

```text
The change you entered is 583
The number of half-dollars to be returned is 11
The number of quarters to be returned is 1
The number of dimes to be returned is 0
The number of nickels to be returned is 1
The number of pennies to be returned is 3
```

![](img/f97f778697507bb6fdd80c5991210cba_138_0.png)

## 快速复习

- 1. 一个 C++ 程序是函数的集合。
- 2. 每个 C++ 程序都有一个名为 main 的函数。
- 3. 单行注释以符号对 // 开始，可位于行中任何位置。
- 4. 多行注释包含在 /* 和 */ 之间。
- 5. 编译器会跳过注释。
- 6. 保留字不能用作程序中的标识符。
- 7. C++ 中的所有保留字都由小写字母组成（见附录 A）。
- 8. 在 C++ 中，标识符是事物的名称。
- 9. C++ 标识符由字母、数字和下划线组成，并且必须以字母或下划线开头。
- 10. 空白包括空格、制表符和换行符。
- 11. 数据类型是一组值以及一组操作。
- 12. C++ 数据类型分为以下三类：简单类型、结构类型和指针类型。
- 13. 简单数据有三类：整数类型、浮点类型和枚举类型。
- 14. 整数数据类型分为九类：char、short、int、long、bool、unsigned char、unsigned short、unsigned int 和 unsigned long。
- 15. 属于 int 数据类型的值范围为 −2147483648（= −2^31）到 2147483647（= 2^31 − 1）。
- 16. 数据类型 bool 只有两个值：true 和 false。
- 17. 最常见的字符集是 ASCII（有 128 个值）和 EBCDIC（有 256 个值）。
- 18. 字符的排序序列是它在字符数据集中的预设编号。
- 19. C++ 提供三种数据类型来操作十进制数：float、double 和 long double。
- 20. C++ 中数据类型 float 用于表示 −3.4E + 38 到 3.4E + 38 之间的任何实数。为 float 数据类型的值分配的内存是四个字节。
- 21. C++ 中数据类型 double 用于表示 −1.7E + 308 到 1.7E + 308 之间的任何实数。为 double 数据类型的值分配的内存是八个字节。
- 22. C++ 中的算术运算符有加法（+）、减法（−）、乘法（*）、除法（/）和取模（%）。
