
第四个人来了。他的体重是 180 磅。他的体重并不比你存在变量 `minimum` 中的体重轻，所以你必须忽略他的体重。`minimum` 仍然包含值 160。

`minimum = 160`

当过程结束时，你脑海中的变量 `minimum` 就包含了最轻男人的体重！

以下是流程图以及相应的 C++ 程序，该程序提示用户输入四个人的体重，然后找到并显示最轻的体重。

![](img/6e4b8e11c2f26304087157218fda632f_391_0.png)

## project_23_3

```cpp
#include <iostream>
using namespace std;
int main() {
    int w1, w2, w3, w4, minimum;

    cout << "Enter the weight ";
    cout << "of four men:" << endl;

    cin >> w1 >> w2 >> w3 >> w4;

    // 记住第一个人的体重
    minimum = w1;

    // 如果第二个更轻，忘记
    // 所有的并记住这个体重
    if (w2 < minimum) {
        minimum = w2;
    }

    // 如果第三个更轻，忘记
    // 所有的并记住这个体重
    if (w3 < minimum) {
        minimum = w3;
    }

    // 如果第四个更轻，忘记
    // 所有的并记住这个体重
    if (w4 < minimum) {
        minimum = w4;
    }

    cout << minimum << endl;
    return 0;
}
```

> 你只需通过将所有布尔表达式中的“小于”运算符替换为“大于”运算符，就可以找到最大值而不是最小值。

## 练习 23.3-1 寻找最重者的名字

编写一个 C++ 程序，提示用户输入三个人的体重，然后显示最重者的名字和体重。

## 解答案

在这个练习中，除了 `maximum` 重量，你还需要另一个变量来存储最重者的名字。对应的 C++ 程序所示：

```cpp
#include <iostream>
using namespace std;
int main() {
    int w1, w2, w3, maximum;
    string n1, n2, n3, m_name;

    cout << "Enter the weight of 1st person: ";
    cin >> w1;

    cout << "Enter the name of 1st person: ";
    cin >> n1;

    cout << "Enter the weight of 2nd person: ";
    cin >> w2;

    cout << "Enter the name of 2nd person: ";
    cin >> n2;

    cout << "Enter the weight of 3rd person: ";
    cin >> w3;

    cout << "Enter the name of 3rd person: ";
    cin >> n3;

    maximum = w1;
    m_name = n1;

    if (w2 > maximum) {
        maximum = w2;
        m_name = n2;
    }

    if (w3 > maximum) {
        maximum = w3;
        m_name = n3;
    }

    cout << "The heaviest person is " << m_name << " with weight " << maximum << endl;
    return 0;
}
```

## 23.4 范围练习

正如你所看到的，在许多问题中，你需要测试一个值是否属于某个范围。假设你想显示衣服的类型。

| 温度（度） | 女士可能穿的衣服 |
| --- | --- |
| < 45 | 毛衣、牛仔裤 |
| 45 ≤ 温度 < 65 | 毛衣、牛仔裤、夹克 |
| 65 ≤ 温度 < 75 | 休闲裤、T恤、背心、人字鞋 |
| 75 ≤ 温度 | 短裤、T恤、背心、裙、人字鞋 |

初一看，你可能会倾向于使用单分支决策结构。然而，前者更方便且增加了可读性，如下代码所示：

```cpp
if (temperature < 45)
    cout << "Sweater, jeans" << endl;
else if (temperature >= 45 && temperature < 65)
    cout << "Sweater, jeans, jacket" << endl;
else if (temperature >= 65 && temperature < 75)
    cout << "Casual pants, t-shirt, tank top, flip-flops, athletic shoes" << endl;
else if (temperature >= 75)
    cout << "Shorts, t-shirt, tank top, skort, flip-flops" << endl;
```

仔细检查发现，并不是所有的布尔表达式都是必要的。例如，如果第一个布尔表达式（`temperature < 45`）求值为假，执行流将继续评估第二个布尔表达式。在这一步，由于第一个布尔表达式已经求值为假，`temperature` 一定大于等于 45。因此，布尔表达式 `temperature >= 45` 在评估时始终为真，因此可以省略。同样的逻辑适用于所有情况；你可以省略所有的布尔表达式。最终的代码片段所示，已移除了不必要的评估：

```cpp
if (temperature < 45)
    cout << "Sweater, jeans" << endl;
else if (temperature < 65)
    cout << "Sweater, jeans, jacket" << endl;
else if (temperature < 75)
    cout << "Casual pants, t-shirt, tank top, flip-flops, athletic shoes" << endl;
else
    cout << "Shorts, t-shirt, tank top, skort, flip-flops" << endl;
```

计算并显示以百分比表示的折扣（例如 0%、5% 等）、以美元表示的折扣金额以及折后的最终金额。假设用户输入的金额为非负值。

## 解决方案

下表总结了提供的各种折扣。

| 范围 | 折扣 |
| --- | --- |
| amount < $30 | 0% |
| $30 ≤ amount < $70 | 5% |
| $70 ≤ amount < $150 | 10% |
| $150 ≤ amount | 20% |

该 C++ 程序如下：

```cpp
#include <iostream>
using namespace std;
int main() {
    double amount, discount_amount, final_amount, discount = 0;

    cout << "Enter total amount: ";
    cin >> amount;

    if (amount < 30) {
        discount = 0;
    } else if (amount >= 30 && amount < 70) {
        discount = 5;
    } else if (amount >= 70 && amount < 150) {
        discount = 10;
    } else if (amount >= 150) {
        discount = 20;
    }

    discount_amount = amount * discount / 100;
    final_amount = amount - discount_amount;
    cout << "You got a discount of " << discount << "%" << endl;
    cout << "You saved $" << discount_amount << endl;
    cout << "You must pay $" << final_amount << endl;
    return 0;
}
```

与之前一样，所有下划线的布尔表达式实际上都是需要的。这里显示最终的 C++ 程序，删除了所有不必要的评估。

## project_23_4_1b

```cpp
#include <iostream>
using namespace std;
int main() {
    double amount, discount_amount, final_amount, discount;

    cout << "Enter total amount: ";
    cin >> amount;

    if (amount < 30) {
        discount = 0;
    } else if (amount < 70) {
        discount = 5;
    } else if (amount < 150) {
        discount = 10;
    } else {
        discount = 20;
    }

    discount_amount = amount * discount / 100;
    final_amount = amount - discount_amount;

    cout << "You got a discount of " << discount << "%" << endl;
    cout << "You saved $" << discount_amount << endl;
    cout << "You must pay $" << final_amount << endl;
    return 0;
}
```

## 练习 23.4-2 验证数据输入并计算折扣

重写上一个练习的 C++ 程序以验证数据输入。当用户输入负值时，必须显示错误信息。

## 解决方案

解决此练习题的通用形式 C++ 程序如下：

```cpp
cout << "Enter total amount: ";
cin >> amount;

if (amount < 0) {
    cout << "Entered value is negative" << endl;
}
else {
```

> 代码片段 1：计算并显示给定的折扣、折扣金额和折后的最终金额。

接下来的代码片段 1 取自上一个练习（练习 23.4-1）。它计算并显示以百分比表示的折扣（例如 0%、5% 等）、以美元表示的折扣金额以及折后的最终金额。

```cpp
if (amount < 30) {
    discount = 0;
} else if (amount < 70) {
    discount = 5;
} else if (amount < 150) {
    discount = 10;
} else {
    discount = 20;
}

discount_amount = amount * discount / 100;
final_amount = amount - discount_amount;

cout << "You got a discount of " << discount << "%" << endl;
cout << "You saved $" << discount_amount << endl;
cout << "You must pay $" << final_amount << endl;
```

将代码片段 1 嵌入主 函数中后，最终的 C++ 程序变为：

```cpp
#include <iostream>
using namespace std;
int main() {
    double amount, discount, final_amount, discount;
    cout << "Enter total amount: ";
    cin >> amount;
    if (amount < 0) {
        cout << "Entered value is negative" << endl;
    } else {
        if (amount < 30) {
            discount = 0;
        } else if (amount < 70) {
            discount = 5;
        } else if (amount < 150) {
            discount = 10;
        } else {
            discount = 20;
        }
        discount_amount = amount * discount / 100;
        final_amount = amount - discount_amount;
        cout << "You got a discount of " << discount << "%" << endl;
        cout << "You saved $" << discount_amount << endl;
        cout << "You must pay $" << final_amount << endl;
    }
    return 0;
}
```

## 练习 23.4-3 寄送包裹

在邮局，寄送包裹的费用取决于其重量以及目的地是在国内还是国外。费用根据下表计算：

| 包裹重量 (lb) | 国内费用（每磅美元） | 国内费用（美元） |
| --- | --- | --- |
| weight ≤ 1 | $0.010 | $10 |
| 1 < weight ≤ 2 | $0.013 | $20 |
| 2 < weight ≤ 4 | $0.015 | $50 |
| 4 < weight | $0.020 | $60 |

设计一个流程图和相应的 C++ 程序，提示用户输入包裹重量和目的地（I 代表国内，O 代表国外），然后计算并显示费用。

## 解决方案

以下通用形式流程图解决了此练习题。

(img/6e4b8e11c2f26304087157218fda632f_400_png) 现在你需要一个多分支结构来计算国内包裹的费用，所示：

(img/6e4b8e11c2f26304087157218fda632f_401_png) 你还需要另一个多分支结构来计算国外包裹的费用，所示：

(img/6e4b8e11c2f26304087157218fda632f_401_png) 合并所有流程图后，最终的流程图变为：

(img/6e4b8e11c2f26304087157218fda632f_402_png) 相应的 C++ 程序所示：

```cpp
#include <iostream>
#include <boost/algorithm/string.hpp>
using boost::algorithm;
using namespace std;

int main() {
    double weight, cost;
    string dest;

    cout << "Enter weight & destination: ";
    cin >> weight >> dest;

    if (to_upper_copy(dest) == "I") {
        if (weight <= 1) {
            cost = weight * 0.010;
        } else if (weight <= 2) {
            cost = weight * 0.013;
        } else if (weight <= 4) {
            cost = weight * 0.015;
        } else {
            cost = weight * 0.020;
        }
    } else {
        if (weight <= 1) {
            cost = 10;
        } else if (weight <= 2) {
            cost = 20;
        } else if (weight <= 4) {
            cost = 50;
        } else {
            cost = 60;
        }
    }
    cout << "Shipping cost: " << cost << endl;
    return 0;
}
```

> 用户输入小写或大写的字母 I（目的地）。`to_upper_copy()` 函数确保程序在两种情况下都能正常执行。

## 练习 23.4-4 求 y 的值

设计一个流程图并编写相应的 C++ 程序，根据公式找到并显示 y 的值（如果可能）：

$y = \frac{x}{x-3} + \frac{8+x}{x+1} - \frac{40x}{x-8} - \frac{3x}{|x-9|}$

对于其他 x 值，范围为 $-5 < x \le 0$，$0 < x \le 6$，$6 < x \le 20$。

## 解决方案
