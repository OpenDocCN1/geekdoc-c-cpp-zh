
为了每次运行程序时获得不同的随机数流，必须为随机数生成器提供一个种子。在 C++ 中，通过调用 `srand` 函数来实现。程序 3-31 说明了这一点。注意 `srand` 函数在第 16 行 `rand` 之前被调用，且整个程序只调用了一次。注意第 9 行持有种子的变量被声明为 `unsigned`。你可能记得，这种数据类型只持有非负整数。这是 `srand` 函数在调用时期望接收的数据类型，因此将变量设为 `unsigned` 可以保证没有负数会被发送到 `srand`。

### 程序 3-31

```cpp
// 此程序演示了当随机数生成器提供了
// “种子”时如何使用随机数。
#include <iostream>
#include <cstdlib> // 使用 srand 和 rand 需要的头文件
using namespace std;

int main() {
    unsigned seed;      // 种子

    // 从用户处获取“种子”值
    cout << "Enter a seed value: ";
    cin >> seed;

    // 在调用 rand() 之前设置生成器种子
    srand(seed);

    // 现在生成并打印三个随机数
    cout << rand() << " ";
    cout << rand() << " ";
    cout << rand() << endl;

    return 0;
}
```

### 粗体显示示例输入的程序输出

| 运行 1: | 运行 2: |
| --- | --- |
| Enter a seed value: **19** | Enter a seed value: **171** |
| 100 15331 209 | 597 10689 28587 |

正如从程序 3-31 的输出所示，每个程序使用不同的种子运行，产生不同的随机数流。然而，如果我们再次使用 19 或 171 作为种子运行程序，我们将得到与第一次完全相同的数字。

> 注意：在你的计算机系统上生成的随机数流可能不同。

## 3.10 随机数 169

## 程序 3-32

```cpp
1 // 此程序演示了如何使用 C++ 时间函数
2 // 为随机数生成器提供一个“种子”。
3 #include <iostream>
4 #include <cstdlib>      // 使用 srand 和 rand 需要的头文件
5 #include <ctime>        // 使用 time 需要的头文件
6 using namespace std;
7 
8 int main()
9 {
10    unsigned seed;      // 随机数生成器种子
11 
12   // 使用时间函数为 srand 获取一个“种子”值
13   seed = time(0);
14   srand(seed);
15 
16   // 现在生成并打印三个随机数
17   cout << rand() << " ";
18   cout << rand() << " ";
19   cout << rand() << endl;
20 
21   return 0;
22 }
```

### 程序输出

2961      2176      181

该输出是由单次运行产生的。每次运行该程序时，结果都会不同。

### 限制随机数的范围

有时程序需要特定范围内的随机数。为了将随机数的范围限制在 1 到某个最大值 `max` 之间，可以使用以下公式。

`number = rand() % max + 1;`

例如，为了生成一个 1 到 6 之间的随机数来代表骰子的点，你会使用：

`dice = rand() % 6 + 1;`

以下是该语句的工作原理。回想一下，模运算给出的是整数除法的余数。当 `rand` 函数返回的正整数除以 6 时，余数将是 0 到 5 之间的一个数字。由于我们需要的是一个 1 到 6 之间的数字，所以我们对其加 1：

这个想法可以扩展到产生任何范围内的随机整数。

`number = (rand() % (maxValue - minValue + 1)) + minValue;`

## 第 3 章 表达式与交互

在公式中，`minValue` 是范围内的最小数字，`maxValue` 是该范围内的最大数字。以下是你可以给变量 `number` 赋值一个 10 到 18 之间的随机整数的方法。

```cpp
const int MIN_VALUE = 10;
const int MAX_VALUE = 18;
number = rand() % (MAX_VALUE - MIN_VALUE + 1) + MIN_VALUE;
```

在此代码中，`MAX_VALUE - MIN_VALUE + 1` 结果为 9。模运算随后返回一个 0 到 8 之间的值。加上 `MIN_VALUE`（即 10），就会产生一个 10 到 18 之间的值。

## 检查点

- 3.27 使用数学库函数结合 `cout` 语句显示双角 `angle1` 英寸四舍五入到最近的整数。
- 3.28 假设变量 `angle1` 和 `angle2` 存储的是弧角。编写一条语句表示 `angle1` 的正弦等于 `angle2` 的余弦，并将结果存储在 `x` 中。
- 3.29 要找到一个数的立方根（三次根），将其提高 1/3 次方。要找到一个数的四次方根，将其提高 1/4 次方。编写一条语句找到变量 `x` 的五次方根并将结果存储在 `y` 中。
- 3.30 编写一条语句产生 1 到 100 之间的随机数，并存储在变量 `luckyNumber` 中。

## 重点调试：程序的手工追踪

手工追踪是一种调试过程，在此过程中你假装自己是执行程序的计算机。你逐行执行程序的每条语句。当你查看一条语句时，记录每个变量在语句执行后将具有的内容。这个过程对于发现数学错误和其他逻辑错误很有帮助。

要追踪程序，你构建一个表格，为每个变量创建一列。表格中的行对应程序中的行。例如，显示了程序 3-33 的手工追踪表。该程序使用了以下变量：`num1`、`num2`、`num3` 和 `avg`。注意手工追踪表为每个变量有一列，并为 `main` 函数中的每行代码有一行。

## 程序 3-33（手工追踪表为空）

```cpp
1 // 此程序计算并显示用户输入的三个数的平均值
2 // 然而，它包含一个错误。你能找到它吗？
3 #include <iostream>
```

（程序继续）

## 3.11 重点调试：程序的手工追踪

## 程序 3-33（手工追踪表为空）（续）

```cpp
4 using namespace std;
5
6 int main()
7 {
8     double num1, num2, num3, avg;
99
10    cout << "Enter the first number: ";
11    cin >> num1;
12    cout << "Enter the second number: ";
13    cin >> num2;
14    cout << "Enter the third number: ";
15    cin >> num3;
16    avg = num1 + num2 + 3;
17    cout << "The average is " << endl;
18    return 0;
19 }
```

| num1 | num2 | num3 | avg |
|---|---|---|---|
| | | | |
| | | | |
| | | | |

## 程序输出示例

第一个数字: 10

第二个数字: 20

第三个数字: 30

平均数是 40

## 程序 3-33（手工追踪为空）

```cpp
1 // 此程序计算并显示用户输入的三个数的平均值
2 // 然而，它包含一个错误。你能找到它吗？
3 #include <iostream>
4 using namespace std;
```

（程序继续）

## 程序 3-33（手工追踪为空）（续）

```cpp
int main()
{
    double num1, num2, num3, avg;

    cout << "Enter the first number: ";
    cin >> num1;
    cout << "Enter the second number: ";
    cin >> num2;
    cout << "Enter the third number: ";
    cin >> num3;
    avg = num1 + num2 + 3;
    cout << "The average is " << avg << endl;
    return 0;
}
```

你看到错误了吗？通过检查第 16 行语句，我们发现了一个错误。除法操作发生在加法之前，因此我们必须将该语句重写为 `avg = (num1 + num2 + num3) / 3;`

## 绿化案例研究 1

## 问题描述

绿化公司提供的服务之一是覆盖物的销售和交付，覆盖物按立方码计量并定价。你被要求创建一个程序确定客户需要多少立方立方覆盖物以及总价。

## 3.12 绿化案例研究–1

## 程序设计

## 程序步骤

程序必须执行以下通用步骤（此列表被称为通用伪代码）：

1. 设置立方的价格（当前为 22.00）。
2. 要求用户输入要覆盖的平方英尺以及在该区域覆盖的深度。
3. 计算所需的立方英尺。
4. 计算所需的立方码。
5. 计算覆盖物的总价。
6. 显示结果。

### 输入变量

| squareFoot // 要覆盖的平方英尺 |
| depth // 覆盖深度（英寸） |

### 输出变量

| double cubicYards // 需要的立方码 |
| double totalPrice // 所有订单立方码的总价 |

## 程序常量

| double PRICE_PER_CUBIC_YD // 每个交付立方的价格 |

## 额外变量

| double cubicFeet // 需要的立方英尺 |

## 详细伪代码（包括实际变量名所需的计算）

```
PRICE_PER_CUBIC_YD = 22.00
Input squareFoot // 带提示输入
Input depth // 带提示输入
cubicFeet = squareFoot * (depth / 12.0)
cubicYards = cubicFeet / 27
totalPrice = cubicYards * PRICE_PER_CUBIC_YD
Display cubicYards, PRICE_PER_CUBIC_YD, and totalPrice
```

### 程序

在检查伪代码逻辑错误后，下一步是将伪代码扩展为最终程序。这在程序 3-34 中所示。

# 第 3 章 表达式与交互

# 程序 3-34

```cpp
1 // 该程序供 Green Fields Landscaping 用于计算客户需要的 
2 // 立方码木覆盖数量及其价格。
3 #include <iostream>
4 #include <iomanip>
5 using namespace std;
6
7 const double PRICE_PER_CUBIC_YD = 22.00;
8
9 int main(){
10 {
11 double squareFeet; // 需要覆盖的面积（平方英尺）
12 int depth; // 铺设深度（英寸）
13 double cubicFeet; // 需要的木覆盖立方英数
14 double cubicYards; // 需要的木覆盖立方码数
15 double totalPrice; // 所有订单立方码的总价
16
17 // 获取输入
18 cout << "Number of square feet to be covered with mulch: ";
19 cin >> squareFeet;
20 cout << "Number of inches deep: ";
21 cin >> depth;
22
23 // 执行计算
24 cubicFeet = squareFeet * (depth / 12.0);
25 cubicYards = cubicFeet / 27;
26 totalPrice = cubicYards * PRICE_PER_CUBIC_YD;
27
28 // 输出结果
29 cout << "\nNumber of cubic yards needed: " << cubicYards << endl;
30 cout << fixed << setprecision(2);
31 cout << "Price per cubic yard: $" << setw(7) << endl;
32 cout << PRICE_PER_CUBIC_YD << endl;
33 cout << "Total price: $" << setw(7) << endl;
34 cout << totalPrice << endl;
35
36 return 0;
37 }
```

### 程序输出（示例输入加粗显示）

Number of square feet to be covered with mulch: 270[Enter]

Number of inches deep: 12[Enter]

Number of cubic yards needed: 10

Price per cubic yard: $ 22.00

Total price: $ 220.00

# 程序输出（不同示例输入加粗显示）

Number of square feet to be covered with mulch: 800[Enter]

Number of inches deep: 3[Enter]

Number of cubic yards needed: 7.40741

Price per cubic yard: $ 22.00

Total price: $ 162.96

# General Crates, Inc., 案例研究

以下额外的案例研究包含了第 3 章介绍的材料的应用，可以在书的配套网站 pearsonpc.com/gaddis 上找到。

该研究开发了一个程序，该程序接受木箱的尺寸，并输出关于其体积、建造成本、销售成本和利润的信息。该案例研究说明了程序开发的步骤：初始问题陈述、使用层次图和伪代码进行程序设计、创建输出所需的算法开发、最终运行程序的源代码，以及通过在多次测试运行程序时生成的输出。

# 综合运用：文字游戏

利用你目前所学的编程知识，你可以开始构建简单的游戏。其中有一个用于玩文字游戏的程序。它将要求玩家输入以下：

- 他们的名字 (`name`)
- 城市名称 (`city`)
- 一项活动 (`activity`)
- 一种动物 (`animal`)
- 你可以买到的食物或产品 (`product`)
- 一个形容词名词 (`petname`)
- 10 到 50 之间的数字 (`age`)
- 0 到 15 之间的数字 (`kids`)

然后它将使用这些单词显示一个故事。

# 程序 3-35

```cpp
1 // 该程序使用字符串来玩文字游戏。
2 #include <iostream>
3 #include <string>
4 using namespace std;
5
6 int main()
7 { // 存储字符串
8 string s1 = "There once a person named ",
9 string s2 = "who lived in ",
10 string s3 = "and loved ";
11 string s4 = "At the age of ",
12 string s5 = "";
13 string s6 = "graduated from high school and went to work in ";
14 string s7 = "factory.\n";
15 string s8 = "got married and had ";
16 string s9 = "children and a pet ";
17 string s10 = "named ";
18 string s11 = "Every weekend the family and ";
19 string s12 = "had fun ";
20 string s13 = "together.";
21 // 用户输入
22 string name, city, activity, product, petName;
23 int age, kids;
```

（程序继续）

# 程序 3-35（续）

# 示例运行（输入加粗）

Enter the following information and I'll tell you a story.

Your name: **Joe**

The name of a city **Honolulu**

A physical activity (e.g. jogging, playing baseball): scuba diving

animal: **bear**

A food or product you can buy: **potato chips**

An adjective noun (e.g. blue car): **dish**

A number between 10 and 50: **20**

A number between 0 and 15: **10**
