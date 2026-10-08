

# 计费程序

（续）

| 输入 | 处理 | 输出 |
| --- | --- | --- |
| 当前读数 | 处理项目：无 | 使用的电量 |
| 上次读数 | | 总费用 |
| 单位电价 | | |
| 存储变量的变量地址： | | |
| 使用的电量 | | |
| 总费用 | | |

- **算法：**
  1. 通过当前读数减去上次读数来计算用电量
  2. 通过用电量乘以单位电价来计算总费用

| 输入 | 处理 | 输出 |
| --- | --- | --- |
| displayBill 函数 | 处理项目：无 | 使用的电量 |
| 使用的电量 | | 总费用 |

- **算法：**
  1. 显示用电量
  2. 显示总费用

图 10-28 电费程序中函数的 IPO 图。

在完成 IPO 图表后，你将进入问题解决过程的第三步，即对算法进行人工检查（desk-check）。使用 53512 和 51875别为当前和上次读数，检查图 10-28 中的算法。使用这些值，用电量和总费用分别为 1637 和 147.33 美元。图 10-29 显示了完成后的检查表。

| 当前读数 (main) | 上次读数 (main) | 单位电价 (main) |
| --- | --- | --- |
| 当前读数 (main) | 上次读数 (main) | 单位电价 (main) |
| 53512 | 51875 | .09 |
| 用电量 (calcBill) | 总费用 (calcBill) | |
| 用电量 (main) | 总费用 (main) | |
| 1637 | 147.33 | |
| 当前读数 (calcBill) | 上次读数 (calcBill) | unit_charge (calcBill) |
| 53512 | 51775 | .09 |
| 用电量 (displayBill) | 总费用 (displayBill) | |
| 1637 | 147.33 | |

图 10-29 电费算法的人工检查表。

问题解决过程的第四步是将算法编码成程序。电费程序的 IPO 图信息和对应的 C++ 指令如图 10-30 所示。

| main 函数 IPO 图信息 | C++ 指令 |
| --- | --- |
| 输入 | |
| 当前读数 上次读数 单位电价 (.09) | int current = 0; int previous = 0; const double UNIT_CHG = .09; |
| 处理 | |
| 输出 | |
| 用电量 总费用 | int units = 0; double total = 0.0; |
| 算法 | |
| 1. 调用 calcBill 获取当前读数和上次读数，向函数传递用于存储当前读数和上次读数的变量地址 | getInput(current, previous); |
| 2. 调用 calcBill 计算用电量和总费用，向函数传递当前读数、单位电价，以及存储用电量和总费用的变量地址 | calcBill(current, previous, UNIT_CHG, total); |
| 3. 调用 displayBill 显示用电量和总费用，向函数传递用电量和总费用 | displayBill(units, total); |

| getInput IPO 图信息 | C++ 指令 |
| --- | --- |
| 输入 | |
| 存储变量的变量地址：当前读数（形参数） 上次读数（形参数） | int &newReading &oldReading |
| 处理 | |
| 输出 | |
| 当前读数 | 存储在 newReading 参数中 |
| 上次读数 | 存储在 oldReading 参数中 |
- **算法：**
  1. 输入当前读数
  2. 输入上次读数

| calcBill IPO 图信息 | C++ 指令 |
| --- | --- |
| 输入 | |
| 当前读数（形参数） 上次读数（形参数） 单位电价（形参数） | int curRead int prevRead double chPerUnit |
| 处理 | |
| 输出 | |
| 存储变量的变量地址：用电量（形参数） 总费用（形参数） | 存储在 numUnits 参数中存储在 totChg 参数中 |
- **算法：**
  1. 通过当前读数减去上次读数计算用电量
  2. 通过用电量乘以单位电价计算总费用

| displayBill IPO 图信息 | C++ 指令 |
| --- | --- |
| 输入 | |
| 用电量（形参数） 总费用（形参数） | int used double charge |
| 处理 | |
| 输出 | |
| 用电量 总费用 | cout << "Units used: " << used << endl; cout << "Total charge: $" << charge << endl; |
- **算法：**
  1. 显示用电量
  2. 显示总费用

问题解决过程的第五步是对程序进行人工检查。图 10-31 显示了整个电费程序，图 10-32 显示了检查表。

```cpp
//Lab10-2.cpp 显示用电量和总费用
//创建/修改于 <你的名字> <当前日期>

#include <iostream>
#include <iomanip>
using namespace std;

// 函数原型
void getInput(int &newReading, int &oldReading);
void calcBill(int curRead, int prevRead, double chgPerUnit, int &numUnits, double &totChg);

void displayBill(int used, double charge);

int main() {
// 声明常量和变量
const double UNIT_CHG = .09;
int current = 0;
int previous = 0;
int units = 0;
double total = 0.0;

cout << fixed << setprecision(2);

// 调用函数
getInput(current, previous);
calcBill(current, previous, UNIT_CHG, units, total);
displayBill(units, total);

system("pause");
return 0;
}
// main 函数结束

// 函数定义
void getInput(int &newReading, int &oldReading) {
    cout << "Current reading: ";
    cin >> newReading;
    cout << "Previous reading: ";
    cin >> oldReading;
}
// getInput 函数结束

void calcBill(int curRead, int prevRead, double chgPerUnit, int &numUnits, double &totChg) {
    numUnits = curRead - prevRead;
    totChg = numUnits * chgPerUnit;
}
// calcBill 函数结束

void displayBill(int used, double charge) {
    cout << "Units used: " << used << endl;
    cout << "Total charge: $" << charge << endl;
}
// displayBill 函数结束
```

图 10-31 电费程序。

![](img/d64a28a68f49d6113bf2f3170ac40ad_419_0.png)

图 10-32 电费程序人工检查表。

问题解决过程的最后一步是评估并修改（如有必要）程序。记住，评估程序的方法将其指令输入计算机，然后使用计算机运行（执行）。在程序运行时，输入与人工检查程序时相同的示例数据。

# 指示

遵循你正在使用的项目启动说明，你可能需要创建一个新项目；如果是，将其命名为 Lab10-2 并保存到 Cpp6/Chap10 文件夹中。不要输入行号。将文件保存在项目文件夹中。现在，按照运行 Lab10-2.cpp 的相应说明。使用 53512 和 51875 作为当前和上次读数测试程序。用电量和总费用应分别为 1637 和 147.33 美元。也使用自己的示例数据测试程序。如有必要，修正程序中的任何漏洞（错误）。

# 实验 10-3 修改

如有必要，创建一个新项目 Lab10-3。将 Lab10-2.cpp 指令输入名为 Lab10-3.cpp 的新文件中。将第一个注释中的 Lab0-2.cpp 改为 Lab10-3.cpp。目前，电费程序使用一个函数计算用电量和总费用。将 calcBill 函数替换为两个函数：一个计算用电量的 void 类型函数，以及一个计算并返回总费用的返回值函数。将函数命名为 getUnits 和 getTotal。保存并运行程序。相应地测试程序。

# 实验 10-4 人工检查

使用以下四组测试分：78, 85, 93 和 98，以及 54 和 32，检查图 10-33 中的代码。

```cpp
//Lab1-4.cpp 显示平均测试分
//创建/修改于 <你的名字> <当前日期>

#include <iostream>
#include <iomanip>
using namespace std;

// 函数原型
void calcAvg(double num1, double num2, double &avg)

int main() {
// 声明变量
double test1 = 0.0;
double test2 = 0.0;
double average = 0.0;

cout << "first test score: ";
cout << "negative number to end: ";
cin >> test1;
while (test1 >= 0) {

cout << "Second test score: ";
cin >> test2;
}

// 调用函数计算平均值
calcAvg(test1, test2, average);

// 显示平均值
cout << fixed << setprecision(1)
cout << "Average score: " << average
<< endl << endl;
}
```

图 10-33 代码（待续）。

