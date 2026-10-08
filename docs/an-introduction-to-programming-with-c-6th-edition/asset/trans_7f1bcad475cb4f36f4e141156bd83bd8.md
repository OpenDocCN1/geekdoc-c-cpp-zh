

# 实验 10-3 修改

```cpp
//Lab10-3.cpp - 显示使用的电量单位数和总电量
//创建/修改人：<your name> 日期：<current date>

#include <iostream>
#include <iomanip>
using namespace std;

// 函数原型
void getInput(int &newReading, int &oldReading);
void getUnits(int curRead, int prevReading, int &numUnits);
double getTotal(int numUnits, double chgPerUnit, double &chgTot);

void displayBill(int used, double charge);

int main() {
    // 声明常量和变量
    const double UNIT_CHG = .09;
    int current = 0;
    int previous = 0;
    int units = 0;
    double total = 0.0;

    cout << fixed <<precision(2);
    // 调用函数
    getInput(current, previous);
    getUnits(current, previous, units);
    total = getTotal(units, UNIT_CHG, total);
    displayBill(units, total);

    system("pause");
    return 0;
} // main 函数结束
******
void getInput(int &newReading, int &oldReading) {
    cout << "当前读数: ";
    cin >> newReading;
    cout << "上一次读数: ";
    cin >> oldReading;
} // getInput 函数结束

void getUnits(int curRead, int prevRead, int &numUnits) {
    numUnits = curRead - prevRead;
    // getUnits 函数结束

double getTotal(int numUnits, double chgPerUnit, double &chgTot) {
    chgTot = numUnits * chgPerUnit;
```

```cpp
    return chgTot;
} // getTotal 函数结束
void displayBill(int used, double charge)
{
    cout << "使用的单位数: " << used << endl;
    cout << "总费用: $" << charge << endl;
}
// displayBill 函数结束
```

# 实验 10-4 纸上检检查 (Desk-Check)

| test1 (main) | test2 (main) | average (main) | num1 (calcAvg) | num2 (calcAvg) |
|--- |--- |--- |--- |--- |
| 6.0 | 6.0 | 6.0 | 75.0 | 65.0 |
| 75.0 | 65.0 | 51.5 | 45.0 | 93.0 |
| 45.0 | 93.0 | 69.0 | 67.0 | 54.0 |
| 67.0 | 54.0 | 43.0 | 54.0 | 32.0 |

# 实验 10-5 调试

要调试该程序，请将函数原型改为 `void assignGrade(int pointsEarned, char &letter);` 并将函数头改为 `void assignGrade(int pointsEarned, char &letter)`。

# 第 11 章微型测验答案

# 微型测验 11-1

- 1. int quantities[20] = {0};
2. quantities[0]
3. quantities[19]
4. quantities[3] = 7;
5. c. total = getTotal(quantities, 20);

# 附录 A 微型测验与实验答案

# 微型测验 11-2

- 1. c. total += orders[2];
2. c. if (orders[3] > 25)
3. bonus = sales[0] * .15;
4. c. if (sub > 0 && sub < 10)
5. a. while (x < 20)

# 微型测验 11-3

- 1. if (prices[x] < lowest)
2. sorting
3. for (int x = 0; x < 10; x ++)
   orders[x] -= 3;
// for 结束

# 第 11 章实验答案

# 实验 11-1 停止与分析

![](img/d64a28a6f49d1137bf2170ac0ad690_0.png)
- 1. 国内数组和国际数组是并行的，因为一个数组的元素与另一个数组的下标对应。例如，两个数组的第一个元素包含一月的销量。第二个元素包含二月的销量，以此类推。
- 2. domestic[1] 元素包含 45000。
- 3. 二月的总销量可以通过将 domestic[1] 元素的内容加上 international[1] 元素的内容计算出来。
- 4. 数组中的最高下标是 5。
- 5. 赋值语句需要改为 `totalSales += domestic[x] + international[x];`。
- 6. 不需要答案。
- 7. //Lab1-1.cpp - 计算国内、国际和总销量
//创建/修改人：<your name> 日期：<current date>

```cpp
#include <iostream>
using namespace std;

int main()
{
    // 声明数组和变量
    int domestic[6] = {12000, 45000, 32000,
        67000, 24000, 55000};
    int international[6] = {10000, 56000, 42000,
        23000, 12000, 34000};

    int totalSales = 0; // 累加器
    int totalDomestic = 0; // 累加器
    int totalInternational = 0; // 累加器

    for (int x = 0; x < 6; x++) {
        totalDomestic += domestic[x];
        totalSales += domestic[x] + international[x];
    }
    
    // 显示国内、国际和总销量
    cout << "国内销量: " <<
        << totalDomestic << endl;
    cout << "国际销量: " <<
        << totalInternational << endl;
    cout << "总销量: " << totalSales << endl;

    system("pause");
    return 0;
} // main 函数结束
```

# 8.

//Lab11-1.cpp - 计算国内、国际、总销量以及每月的总销量
//创建/修改人：<your name> 日期：<current date>

```cpp
#include <iostream>
using namespace std;

int main()
{
    // 声明数组和变量
    int domestic[6] = {12000, 45000, 32000,
        67000, 24000, 55000};
    int international[6] = {10000, 56000, 42000,
        23000, 12000, 34000};
```

# 附录 A 微型测验与实验答案

```cpp
int totalSales = 0; // 累加器
int totalDomestic = 0; // 累加器
int totalInternational = 0; // 累加器
int monthSales[6] = {0};

// 累加销量
for (int x = 0; x < 6; x++) {
    totalDomestic += domestic[x];
    totalInternational += international[x];
    totalSales += domestic[x] + international[x];
}

// 显示国内、国际和总销量以及每月的总销量
cout << "国内销量: " <<
    << totalDomestic << endl;
cout << "国际销量: " <<
    << totalInternational << endl;
cout << "总销量: " << totalSales << endl;

system("pause");
return 0;
} // main 函数结束
```

# 7.

不需要答案。

# 实验 11-2 计划

```cpp
//Lab11-2.cpp - 计算一组学生的平均分
//创建/修改人：<your name> 日期：<current date>

#include <iostream>
using namespace std;

int main() {
    // 声明数组和变量
    int quantities[20] = {0};
    int total = 0;
    double average = 0;
    int choice;

    do {
        cout << "输入学生人数 (1-20): ";
        cin >> choice;
    } while (choice < 1 || choice > 20);

    for (int i = 0; i < choice; i++) {
        cout << "输入学生 " << i + 1 << " 的分数: ";
        cin >> quantities[i];
        total += quantities[i];
    }

    average = (double)total / choice;

    cout << fixed <<precision(2);
    cout << "平均分数为: " << average << endl;

    system("pause");
    return 0;
}
```

# 11-3 修改

```cpp
//Lab11-3.cpp - 在整数数组中寻找最小值和值
//创建/修改人：<your name> 日期：<current date>

#include <iostream>
using namespace std;

// 函数原型
void findMinMax(int scores[], int size, int &low, int &high);

int main() {
    // 声明数组和变量
    int scores[100];
    int size;
    int low, max;

    cout << "输入分数人数 (1-100): ";
    cin >> size;

    for (int i = 0; i < size; i++) {
        cout << "输入分数 " << i + 1 << ": ";
        cin >> scores[i];
    }

    findMinMax(scores, size, low, max);

    cout << "最低分数: " << low << endl;
    cout << "最高分数: " << max << endl;

    system("pause");
    return 0;
}

void findMinMax(int scores[], int size, int &low, int &high) {
    low = scores[0];
    high = scores[0];
    for (int i = 1; i < size; i++) {
        if (scores[i] < low)
            low = scores[i];
        if (scores[i] > high)
            high = scores[i];
    }
}
```

