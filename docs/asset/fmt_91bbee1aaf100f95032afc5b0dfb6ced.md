
`enum Paint = { red, blue, yellow, green, orange, purple };`

`paint = green;`

```
// 编写一个 if/else 语句，如果颜色
// 为红色、蓝色或黄色，则打印 "primary color"，
// 否则打印 "mixed color"。在测试时应使用关系//
// 表达式。
```

## 关注测试与调试：验证输出结果

**概念：** 在测试新创建或修改的程序时，必须仔细检查输出结果以确保其正确性。

一旦正在开发的程序经过了设计、用编程语言编写，并发现编译和链接没有错误，就很容易得出它运行正常的结论。如果程序运行得没有错误并产生了“合理”的输出，情况更是如此。然而，仅仅因为程序运行并产生了输出，并不意味着它是正确的。它可能包含严重的逻辑错误，导致输出错误。要确定一个程序是否实际运行正常，必须使用可以预测输出的数据进行测试，并检查输出以确保其准确性。

程序 4-29 运行并产生的输出最初看起来可能是合理的。然而，它包含一个会导致产生错误输出的错误。

### 程序 4-29

```
1 // 此程序在已知客人人数和人均费用时
2 // 计算客户的自助午餐总费用。
3 // 它包含一个逻辑错误。
4 #include <iostream>
5 #include <iomanip>
6 using namespace std;
7
8 const ADULT_MEAL_COST = 6.25; // 儿童餐点费用 = 此费的 75%
```

（程序继续）

# 第 4 章 决策

### 程序 4-29（续）

### 示例输入对应的程序输出（加粗显示）

此程序计算自助午餐的总费用。

输入成年客人人数（12 岁及以上）：92[回车]

输入儿童客人人数（2-11 岁）：4[回车]

自助午餐总费用为 $570.00

乍一看，程序似乎运行得正确。成人的人均费用是 $6.25，所以如果有 100 名成年客人，费用将是 $625。但只有 96 名客人，其中 4 个是孩子，所以费用应该是 $570。这个数字看起来“大致正确”。

然而，“大致正确”并不是准确性的充分测试。如果程序运行时其数据输出可以更容易地检查，程序员会很快发现存在错误。这里是使用更仔细的样本数据对同一程序进行两次额外运行的输出。

### 不同示例输入对应的程序输出（加粗显示）

此程序计算自助午餐的总费用。

输入成年客人人数（12 岁及以上）：1[回车]

输入儿童客人人数（2-11 岁）：0[回车]

自助午餐总费用为 $62.00

## 4.15 Green Fields 景观案例研究——第 2 部分

### 仍然不同的示例输入对应的程序输出（加粗显示）

此程序计算自助午餐的总费用。

输入成年客人人数（12 岁及以上）：0[回车]

输入儿童客人人数（2-11 岁）：1[回车]

自助午餐总费用为 $4.50

从这个输出中我们可以看到，儿童餐点的费用被正确计算为成年餐点费用的 75%，但成人的费用是错误的。对于一名成年人，结果是 $6.00，而本应该是 $6.25。

为了找到问题，程序员应该确定哪些代码行最可能导致问题。最可能是第 8 行 `ADULT_MEAL_COST` 的初始化或存储有问题，第 14、16、27 和 29 行 `adultTotal` 或 `totalMealCost` 的计算或存储有问题，或者是第 33 行打印 `totalMealCost`。因为一份成年餐的费用错误地显示为整数金额，一个需要检查的项目是所有存储浮点值的变量是否都定义为 `float` 或 `double`。果然，虽然 `adultTotal` 和 `totalMealCost` 都被定义为 `double`，但命名常量 `ADULT_MEAL_COST` 被定义为了 `int`。6.25 在存储时被截断为 6。将该命名常量的定义重写为：

```
const double ADULT_MEAL_COST = 6.25;
```

运行程序后，我们得到了以下结果。

### 修改后程序在示例输入下的输出（加粗显示）

此程序计算自助午餐的总费用。

输入成年客人人数（12 岁及以上）：1[回车]

输入儿童客人人数（2-11 岁）：0[回车]

自助午餐总费用为 $6.25

现在问题已经找到，程序是正确的。然而，应该应该使用精心设计的测试用例进行额外测试以确认这一点。关于如何开发良好的测试用例的主题将在下一章讨论。

## Green Fields 景观案例研究——第 2 部分

### 问题陈述

Green Fields 景观公司提供的服务是常绿树的销售。程序必须执行以下通用步骤：

1. 让用户输入购买的数量和高度。
2. 让用户指示是否需要种植。
3. 如果需要种植，4. 计算总费用。
4. 如果需要送货，5. 计算送货费用。
6. 计算总费用。
7. 打印显示所有购买费用的账单信息。

### 命名常量

```
double PRICE_1 = 39.00
double PRICE_2 = 69.00
double PRICE_3 = 99.00
double PRICE_4 = 199.00
double PER_TREE_DELIVERY = 20.00
double MAX_DELIVERY = 100.00
```

### 输入变量值

```
int numTrees              // 购买的常绿树数量
int height               // 树的高度
char planted             // 是否种植('Y'/'N')
char delivered           // 是否送货?('Y'/'N')
```

### 输出变量值

```
double treeCost          // 每棵树的费用
double totalTreeCost     // 所有树的总价
double deliveryCost      // 运送费用
double plantingCost      // 种植费用
double totalCharges       // 总账单金额
```

### 详细伪代码（包含实际变量名和所需的计算）

```
初始化 deliveryCost 和 plantingCost 为 0
显示屏幕标题
输入 numTrees, height, planted
If planted = 'N'
    输入 delivery
End If
If height < 3
    treeCost = PRICE_1
    Else If height <= 5
        treeCost = PRICE_2
    Else If height <= 8
        treeCost = PRICE_3
    Else
        treeCost = PRICE_4
End If
totalTreeCost = numTrees * treeCost
If planted = 'Y'
    plantingCost = totalTreeCost / 2 // deliveryCost 保持为0
Else If numTrees <= 5
    deliveryCost = PER_TREE_DELIVERY * numTrees
    Else
        deliveryCost = MAX_DELIVERY
End If
totalCharges = totalTreeCost + deliveryCost + plantingCost
显示账单标题
显示 numTrees, treeCost, totalTreeCost,
deliveryCost, plantingCost, totalCharges
```

### 程序

在检查伪代码逻辑错误之后，下一步是将伪代码扩展为最终格式。这在程序 4-30 中所示。

### 程序 4-30

```cpp
// 此程序用于 Green Fields 景观公司
// 创建常绿树销售的客户账单。
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    const double PRICE_1 = 39.00, // 为不同尺寸的树定价
           PRICE_2 = 69.00,
           PRICE_3 = 99.00,
           PRICE_4 = 199.00;

    const double PER_TREE_DELIVERY = 20.00, // 设置送货费
        MAX_DELIVERY = 100.00;
```

# 程序 4-30 (续)

```cpp
int    numTrees;             // 购买的常绿树数量
int height;               // 接近英尺的树高
char   planted;          // 是否要种植？('Y'/'N')
char delivered;           // 是否要送送货？('Y'/'N')
double treeCost;       // 单棵树的费用
double totalTreeCost;        // 所有树的总价
double deliveryCost = 0.0; // 所有树的运费
double plantingCost = 0.0; // 所有树的种植费
double totalCharges;         // 发票总计金额

// 显示购买界面并获取购买信息
cout << "Green Fields Landscaping\n";
cout << "Evergreen Tree Purchase\n";

cout << "Number of trees purchased: ";
cin >> numTrees;
cout << "Tree height to the nearest foot: ";
cin >> height;
cout << "Will Green Fields do the planting?(Y/N): ";
cin >> planted;

if (planted == 'Y' || planted == 'y') {
    cout << "Do you want the trees delivered? (Y/N): ";
    cin >> delivered;
}

// 计算费用
if (height < 3)
    treeCost = PRICE_1;
else if (height <= 5)
    treeCost = PRICE_2;
else if (height <= 8)
    treeCost = PRICE_3;
else
    treeCost = PRICE_4;

totalTreeCost = numTrees * treeCost;
if ((delivered == 'Y') || (delivered == 'y'))
    plantingCost = totalTreeCost / 2;
else if (delivered <= 5)
    deliveryCost = PER_TREE_DELIVERY * numTrees;
else
    deliveryCost = MAX_DELIVERY;

// 种植费和运费均保持为0

totalCharges = totalTreeCost + deliveryCost + plantingCost;
```

## 4.15 Green Fields Landscaping 案例研究——部分 2

# 程序 4-30 (续)

```cpp
65 // 显示发票上的信息
66 cout << fixed << showpoint() << setprecision(2);
67 cout << "\n" << "Green Fields Landscaping" << "\n";
68 cout << "\n" << "Evergreen Tree Purchase" << "\n";
69 cout << setw(2) << numTrees << " trees @ $" << setw(6) << treeCost
70 cout << " each = " << setw(8) << totalTreeCost << endl;
71 cout << setw(8) << deliveryCost << endl;
72 cout << "Delivery charge " << "$";
73 cout << setw(8) << plantingCost << endl;
74 cout << " " << endl;
75 cout << " " << endl;
76 cout << "Total Amount Due " << "$";
77 cout << setw(8) << totalCharges << endl << endl;
78 return 0;
79 }
```

# 显示示例输入的程序输出（加粗部分输入）

Green Fields Landscaping

Evergreen Tree Purchase

Number of trees purchased: 4[Enter]

Tree height to the nearest foot: 7[Enter]

Will Green Fields do the planting?(Y/N): y[Enter]

Green Fields Landscaping

Evergreen Tree Purchase

| 4 trees @ $ 99.00 = | $ 396.00 |

| Delivery charge | $ 0.00 |

| Planting charge | $ 198.00 |

Total Amount Due $ 594.00

# Crazy's My Computer Emporium 案例研究

以下额外的案例研究包含了第 4 章所介绍内容的应用，可以在书籍的配套网站 pearsonhighered.com/gaddis 找到。

Crazy's 是一家家用品零售商，其销售全部采用佣金制。佣金率取决于销售额。该案例研究开发了一个程序，用于计算大量销售佣金，并扣除已付工资，以计算销售员月底还欠多少钱。该案例研究包含了问题定义、通用伪代码设计以及带有示例输出的最终程序。

# 将一切结合在一起：占卜师

利用第 3 章学到的 `rand()` 函数和本章学到的 `if/else` 语句，你现在可以创建一个简单的占卜游戏。程序将首先要求用户输入三个他们想要的职业。程序将使用随机数来预测他们的未来。

### 程序 4-31

```cpp
1 // 此程序使用随机数
2 // 和 if/else 语句预测玩家的未来。
3 #include <iostream>
4 #include <string>          // 用于字符串
5 #include <cstdlib>         // 用于随机数
6 using namespace std;
7 
8 int main(){
9 {
10 // 存储输入的职业
11 string career1,career2,career3;
12 
13 int randomNum;           // 存储随机生成的整数
14 
15 // 设置种子
16 unsigned seed = time(0);
17 srand(seed);
18 
19 // 解释游戏
20 cout << "I am a fortune teller: Look into my crystal screen \n\n";
21 cout << "and enter 3 careers you would like to have. Example: \n";
22 cout << "chef in astronaut \n";
23 cout << "Then will predict what you will be. \n";
24 cout << "Choice 1: ";
25 getline(cin,career1);
26 cout << "Choice 2: ";
27 getline(cin,career2);
28 cout << "Choice 3: ";
29 getline(cin,career3);
30 
31 // 生成一个 1 到 4 之间的整数。
32 randomNum = 1 + rand() % 4;
33 
34 // 使用分支逻辑输出预测
35 if (randomNum == 1)
36 cout << "\nYou will be " << career1 << ". \n";
37 else if (randomNum == 2)
38 cout << "\nYou will be " << career2 << ". \n";
39 else if (randomNum == 3)
40 cout << "\nYou will be " << career3 << ". \n";
41 return 0;
42 }
```

# 程序 431 (续)

显示加粗输入的示例运行

A fortune teller. Look into my crystal screen

and enter 3 careers you would like to have. Example:

chef

astronaut

agent

Then I will predict what you will be.

Choice 1: announcer[Enter]

Choice 2: instructor[Enter]

Choice 3: clown[Enter]

You will be radio announcer.

# 复习题与练习题

填空与简答题

1. 使用大于、小于、大于等于、小于等于、等于或不等于运算符的表达式称为____ 表达式。
2. 如果表达式为____，则关系表达式的值为0；如果表达式为____，则为1。
3. 如果语句代表值为 0 的表达式为____，非零值的表达式为____。
