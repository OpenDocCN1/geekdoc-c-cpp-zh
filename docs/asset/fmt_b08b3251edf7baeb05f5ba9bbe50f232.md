
```cpp
cout << "Enter a negative number to end: ";

cin >> payCode;

while (payCode >= 0)

{

    // 搜索数组中的每一行，在
    // 第一列中查找工资代码
    // 如果数组中还有元素待搜索
    // 且未找到工资代码，继续搜索
    rowSubscript = 0;
    while (rowSubscript <= 3 &&
           codesAndRates[rowSubscript][0]
           != payCode)
    {
        rowSubscript++;
    }
    //end while
    if (rowSubscript <= 3)
    {
        cout << "Pay rate for pay code " <<
             codesAndRates[rowSubscript][0]
              << "$" <<
             codesAndRates[rowSubscript][1] << endl;
    }
    else
    {
        cout << "Invalid pay code" << endl;
    }
    //end if
    // 下一个
    cout << "Pay code (3, 7, 6, or 9)." << endl;
    cout << "Enter a negative number to end: ";
    cin >> payCode;
}
//end while
return 0;
}
```

图 12-17 Wilson 公司程序（续）

## 搜索二维数组（续）

```cpp
30 rowSubscript = 0;
31 while (rowSubscript <= 3 &&
32    codesAndRates[rowSubscript][0]
33    != payCode)
34    rowSubscript++;
35 //end while

37 // 如果找到了工资代码，显示
38 // 同行的
39 // 第二列
40 if (rowSubscript <= 3)
41     cout << "Pay rate for pay code " <<
42      codesAndRates[rowSubscript][0]
43      << "$" <<
44      codesAndRates[rowSubscript][1] << endl;

46 else
47     cout << "Invalid pay code" << endl;
48 //end if

50 // 下一个，获取工资代码
51 cout << "Pay code (3, 7, 6, or 9)." << endl;
52 cout << "Enter a negative number to end: ";
53 cin >> payCode;
54 } //end while
```

图 12-17 Wilson 公司程序

你将检查图 12-18 中的程序以观察如何搜索。第 11 到 16 行的定义了二维数组 `codesAndRates` 以及名为 `payCode` 和 `rowSubscript` 的变量。第 19 和 20 行的 `cout` 语句提示用户输入工资代码，第 21 行的 `cin` 语句存储用户的响应。假设用户输入 6 作为工资代码。

# 第 12 章 二维数组

| codesAndRates[0][0] | codesAndRates[0][1] |
| :--- | :--- |
| 3 | 8 |
| codesAndRates[1][0] | codesAndRates[1][1] |
| 7 | 10 |
| codesAndRates[2][0] | codesAndRates[2][1] |
| 6 | 14 |
| codesAndRates[3][0] | codesAndRates[3][1] |
| 9 | 20 |

图 12-18 执行完第 11 到 21 行语句后的检查表

接下来处理程序外部循环的 `while` 子句。由于 `payCode` 变量的值大于或等于 0，该条件为真。因此，计算机处理外部循环的指令。第 30 到 35 行的外部循环指令在数组的第一列中搜索工资代码。仔细观察这些指令。第 30 行的指令将 0 赋给 `rowSubscript` 变量，以确保从第一行开始搜索。`while` 子句复合条件为真，因为它的两个子句都为真。第一个子句判断 `rowSubscript` 变量的值小于或等于 3（数组的最大行下标）。子句为真是因为 `rowSubscript` 变量包含数字 0。第二个子句将 `codesAndRates[rowSubscript][0]` 元素的值与 `payCode` 变量的值进行比较。该子句为真是因为 `codesAndRates[3][0]` 元素的值不等于 `payCode` 变量的值（6）。结果处理了嵌套循环中第 34 行的 `rowSubscript++` 语句。该语句将 `rowSubscript` 内容加 1，得到 1。递增 `rowSubscript` 变量允许计算机搜索数组的下一行。图 12-19 显示了嵌套循环处理第一次后的检查表。

# 查找二维数组

| codesAndRates[0][0] | codesAndRates[0][1] |
| --- | --- |
| 3 | 8 | |
| codesAndRates[1][0] | codesAndRates[1][1] |
| 7 | 10 |
| codesAndRates[2][0] | codesAndRates[2][1] |
| 6 | 14 |
| codesAndRates[3][0] | codesAndRates[3][1] |
| 9 | 20 |
| payCode | rowSubscript |
| 6 | 6 |
| | 1 |

图 12-19 嵌套循环处理第一次后的手工检查表

计算嵌套循环中 `while` 子句的复合条件。该复合条件的结果为真，因为 `rowSubscript` 的值 (1) 小于或等于 3，且（在该行中）`codesAndRates[1][0]` 元素的值 (7) 不等于 `payCode` 变量的值 (6)。第 34 行的 `rowSubscript += 1` 语句将 `rowSubscript` 变量增加了 1；结果为 2。图 20 嵌套循环处理第二次后的手工检查表。

| codesAndRates[0][0] | codesAndRates[0][1] |
| --- | --- |
| 3 | 8 |
| codesAndRates[1][0] | codesAndRates[1][1] |
| 7 | 10 |
| codesAndRates[2][0] | codesAndRates[2][1] |
| 6 | 14 |
| codesAndRates[3][0] | codesAndRates[3][1] |
| 9 | 20 |
| payCode | rowSubscript |
| 6 | 6 |
| | 2 |

图 12-20 嵌套循环处理第二次后的手工检查表

再次计算嵌套循环中 `while` 子句的复合条件。该复合条件的结果为假，因为 `codesAndRates[2][0]` 元素的值 (6) 等于 `payCode` 变量的值 (6)。此时，嵌套循环结束，继续执行第 40 行的 `if` 语句。`if` 语句的条件

# 第 12 章 二维数组

确定 `rowSubscript` 变量的值是否小于或等于 3（数组中的最大行下标）。该条件的结果为真，因为 `rowSubscript` 变量的值为 2。此时，计算机处理 `cout` 语句，在第 40 行到第 45 行显示一条消息。该语句显示存储在 `codesAndRates[2][0]` 元素中的支付代码以及存储在 `codesAndRates[2][1]` 中的费率，如之前的图 12-15 所示。消息显示后，`if` 语句结束。接下来处理第 51 行和第 52 行的语句。这些语句提示用户输入另一个代码。第 53 行的 `cin` 语句将用户的响应存储在 `payCode` 变量中。假设用户输入数字 5。计算机计算外层循环 `while` 子句中的条件。该条件的结果为真，因为 `payCode` (5) 的值大于或等于数字 2。因此，计算机执行外层循环的指令，将 `rowSubscript` 赋值 0，以确保新的搜索从第一行开始。第 33 行的 `while` 循环告诉计算机，只要 `rowSubscript` 变量的值小于或等于 3（数组中的最大行下标），且数组元素不包含存储在 `payCode` 变量中的支付代码，就处理 `rowSubscript += 1` 语句。数组的嵌套循环没有找到支付代码，或者支付代码存储在数组的第一列中。图 12-21 显示了嵌套循环结束后的手工检查表。在上一次搜索中，嵌套循环在找到支付代码 6 时停止，而这次搜索的嵌套循环在 `rowSubscript` 变量包含数字 4 时停止。

| codesAndRates[0][0] | codesAndRates[0][1] |
|---|---|
| 3 | 8 |
| codesAndRates[1][0] | codesAndRates[1][1] |
| 7 | 10 |
| codesAndRates[2][0] | codesAndRates[2][1] |
| 6 | 14 |
| codesAndRates[3][0] | codesAndRates[3][1] |
| 9 | 20 |
| payCode | rowSubscript |
| 6 | 6 |
| <- | 6 |
| 5 | 6 |
| | 6 |
| | 6 |
| | 4 |

图 12-21 第二次搜索期间嵌套循环结束后的手工检查表

# 将二维数组传递给函数

当嵌套循环结束时，继续处理第 40 行的 `if` 语句。`if` 条件确定 `rowScript` 变量的值是否不等于 3（数组中的最大行下标）。该条件的结果为假，因为 `rowScript` 变量的值为 4。这表明嵌套循环是因为到达第一列末尾且没有找到支付代码而停止的。第 47 行的语句显示“Invalid pay”消息，如之前的图 12-16 所示。消息显示后，`if` 语句结束。接下来，第 51 行和第 52 行的 `cout` 语句提示用户输入另一个支付代码，第 53 行的 `cin` 语句将用户的响应存储在 `payCode` 变量中。假设用户输入 -1。计算机计算外层循环条件。该条件的结果为假，因为 `payCode` 变量的值 (-1) 不大于数字 0。结果是外层循环结束，计算机处理 `return 0;` 语句后程序结束，计算机从内存中移除数组和标量变量。

# 将二维数组传递给函数

图 12-22 显示了之前在图 12-15 中看到的修改版本。在修改版本中，`main` 函数将 `orders` 数组传递给。仔细研究 `displayArray` 函数以及数组的第一组。与一维数组一样，二维数组是通过引用传递的。第一组括号包含行数。第二组括号在函数原型中是可选的。因此，你也可以将形式参数写为 `int [3]`。你在本章末尾学习了值和引用。

# 第 12 章 二维数组

```cpp
//Modified Company.cpp
//Created by <name>
//on <date>
#include <iostream>
using namespace std;

//Displays二维数组
int main() {
    int orders[4][3] = {};
    //向数组输入数据
    for (int region = 0; region < 4; region++) {
        for (int month = 0; month < 3; month++) {
            cout << "Region " << region + 1 << ", " << month + 1 << ": ";
            cin >> orders[region][month];
        }
    } // end for
    //显示数组内容
    displayArray(orders);
    system("pause");
    return 0;
} // end main function
void displayArray(int nums[4][3]) {
    for (int region = 0; region < 4; region++) {
        cout << "Region " << region + 1 << ":" << endl;
        for (int month = 0; month < 3; month++) {
            cout << "Month " << month + 1 << ": " << nums[region][month] << endl;
        }
    } // end for
} // end displayArray
```

你可以在第 17 行和第 37 行使用 `region++`，在第 18 行和第 41 行使用 `month++`。

图 12-2 修改后的订单程序

# 迷你测试 12-2

下列哪一项将 `total` 变量增加了 `purchases` 数组中第二行第一列元素的值？该变量和数组均为 `int` 类型。

- purchases[2][1] += total;
- purchases[1][2] += total;
- total += purchases[2][1];
- total += purchases[1][0];

下列哪一个 `if` 条件确定存储在 `scores` 数组第四列第三行的值是否大于 25？该数组为 `int` 类型。

- if (scores[3, 4] > 25)
- if (scores[4, 3] > 25)
- if (scores[2][3] > 25)
- if (scores[3][4] > 25)

编写一条 C 语句，将 `sales` 数组中第一行第二列元素的内容乘以 .15，并将结果存储在 `bonus` 变量中。`sales` 数组和 `bonus` 变量均为 `double` 类型。

下列哪一个 `if` 条件确定 `int` 类型 `row` 是否包含 `scores` 数组的有效下标？

- if (row >= 0 && row < 10)
- if (row >= 0 && row <= 10)
- if (row >= 0 && row < 9)
- if (row > 0 && row <= 10)

# AB 12-1 停止并分析

研究图 12-23 所示的程序，然后回答问题。`company` 数组包含了公司在到六月期间在国内和国际销售金额。

第一行包含这三个月的国内销售额。第二行包含同一期间的国际销售额。

## 第 12 章 二维数组

```cpp
 //Lab12-1.cpp 计算总销售额
// #由 <你的姓名> 于 <当前日期> 创建/修订
#include <iostream>
using namespace std;
int main() {
    // 声明数组和变量
    int company[2][6] = {{12000, 45000, 32000,
                          67000, 24000, 55000},
                          10000, 56000, 42000,
                          23000, 12000, 34000}};
    int companySales = 0; // 累加器
    // 累加销售额
    for (int location = 0; location < 2; location += 1) {
        for (int month = 0; month < 6; month += 1) {
            companySales += company[location][month];
        }
    }
    // 显示总销售额
    cout << "Company sales: $" << companySales << endl;
    system("pause");
    return 0;
}
```
