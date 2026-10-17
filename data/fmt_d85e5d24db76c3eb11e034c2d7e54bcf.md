
```cpp
1 // 此程序演示了如何使用重载函数来计算
2 // 时薪制或薪制员工的周薪。
3 #include <iostream>
4 #include <iomanip>
5 using namespace std;

6 // 函数原型
7 char getChoice();
8 double calcWeeklyPay(int, double);
9 double calcWeeklyPay(double);

10 int main(){
11 {
12     char selection;      // 菜单选择
13     int worked;         // 周工数
14     double rate;        // 时薪资率
15     double yearly;       // 年薪

17     // 设置数值输出格式
18     cout << fixed << setprecision(2);

20     // 显示菜单并获取选择
21     cout << "Do you want to calculate the weekly pay of\n";
22     cout << "(H) or (S) salaried employee, or ";
```

（程序继续）

## 6.14 函数重载

### 程序 6-29（续）

```cpp
41    // 薪制员工
42    case 'S' :
43        cout << "What is the annual salary? ";
44        cin >> yearly;
45        cout << "The gross weekly pay is $";
46        cout << calcWeeklyPay(yearly) << endl;
47    }
48    return 0;

50
51 /*
52      getChoice()
53      * 接收并返回用户验证过的菜单选择。
54      ****************************************************/
55 char getChoice()
56 {
57     char letter;      // 存储用户的字母选择

59     // 获取用户的选择
60     cin >> letter;

62     // 验证选择
63     while (letter != 'H' && letter != 'h')
64         && (letter != 'S' && letter != 's')
65     {
66         cout << "Enter H or S: ";
67         cin >> letter;
68     }
69     // 返回选择
70     return letter;
71 }
72 
73 /*
74      * 重载函数 calcWeeklyPay
75      * 此函数计算并返回时薪制员工的
76      * 周薪。参数 hours 和 payRate 
77      * 存储了工作小时数和时薪。
78      ****************************************************/
79 double calcWeeklyPay(int hours, double payRate)
80 {
81     return hours * payRate;
82 }
83 
84 /*
85      * 重载函数 calcWeeklyPay
86      * 此函数计算并返回薪制员工的
87      * 周薪。参数 annSalary 存储了
88      * 员工的年薪。
89      ****************************************************/
90 double calcWeeklyPay(double annSalary)
91 {
92     return annSalary / 52.0;
93 }
94 */
```

（程序继续）

### 程序 6-29（续）

带有加粗示例输入的程序输出：

Do you want to calculate the weekly pay of

(H) an hourly-wage employee, or

(S) a salaried employee? H[Enter]

How many hours were worked? 40[Enter]

What is the hourly pay rate? 18.50[Enter]

The gross weekly pay is **740.00**

带有其他加粗示例数据的程序输出：

Do you want to calculate the weekly pay of

(H) an hourly-wage employee, or

(S) a salaried employee? S[Enter]

What is the annual salary? 48000.00[Enter]

The gross weekly pay is **923.08**

## 6.15 exit () 函数

> 概念：`exit()` 函数会导致程序终止，无论正在执行的是哪一个函数或控制机制。

当 C++ 程序遇到 `main` 函数中的 `return` 语句时会停止执行。然而，当其他函数结束时，程序不会停止。程序的控制权会返回到函数调用后的位置。但是，在某些少数情况下，需要在 `main` 以外的函数终止程序。为了实现这一点，使用了 `exit` 函数。

当调用 `exit` 函数时，它会导致程序停止，无论调用位于哪个函数中。程序 6-30 演示了这种效果。

### 程序 6-30

```cpp
1 // 此程序演示了 exit 函数如何导致程序
2 // 停止执行。
3 #include <iostream>
4 #include <cstdlib>    // 使用 exit 函数需要
5 using namespace std;

6 // 函数原型
7 void someFunction();

8 int main()
9 {
10     someFunction();
11     return 0;
12 }
```

（程序继续）

### 程序 6-30（续）

```cpp
16 /*
17 * someFunction
18 * 函数使用了 exit，可以从 main 以外的
19 * 函数结束程序。这不被认为是
20 * 良好的编程习惯，通常
21 * 仅用于信号发生了错误情况。
22 *************************************************/
23 void someFunction()
24 {
25 cout << "This program terminates with the exit function.\n";
26 cout << "Bye!\n";
27 exit(0);
28 cout << "This message will never be displayed!\n";
29 cout << "because the program has already terminated.\n";
30 }
```

### 程序输出

要使用 `exit` 函数，必须包含 `cstdlib` 头文件。注意该函数接受一个整数参数。该参数是您希望程序传回给计算机操作系统的退出码。这有时用于程序外部，以指示程序是成功结束还是带有错误结束。

## 第6章 函数

在屏幕上显示返回值。这让你能够看到程序在与其最终将成为的其他程序隔离运行时的表现。程序 6-31 是用于测试健康俱乐部会员制程序中 `showFees` 函数的驱动程序。

### 程序 6-31

```cpp
1 // 此程序是测试 showFees 函数的驱动程序。
2 #include <iostream>
3 #include <string>
4 using namespace std;
5
6 // 函数原型
7 void showFees(string, double, int);
8
9 int main()
10 {
11 cout << "Calling the showFees function with arguments "
12 << "Adult, 120.0, 3.\n";
13 showFees("Adult", 120.0, 3);
14
15 cout << "Calling the showFees function with arguments "
16 << "Child, 60.0, 2.\n";
17 showFees("Child", 60.0, 2);
18
19 cout << "Calling the showFees function with arguments "
20 << "Senior, 100.0, 4.\n";
21 showFees("Senior", 100.0, 4);
22
23 return 0;
24 }
```

> /** showFees **

* 此函数使用会员类型、每月

* 费率和通过的月数作为参数

* * 来计算并打印会员的总费用。

 */

```cpp
32 void showFees(string memberType, double rate, int months)
33 {
34 cout << "Membership Type : " << memberType << ""
35 << "Monthly rate $" << rate << endl
36 << "Number of months: " << months << endl
37 << "Total charges : $" << (rate * months) << endl;
38 }
```

### 程序输出

Calling the showFees function with arguments Adult, 120.0, 3.

Membership Type : Adult          Monthly rate $120

Number of months: 3

Total charges : $360

(程序输出继续)

### 程序 6-31 (续)

```text
Calling the showFees function with arguments Child, 60.0, 2.
Membership Type : Child    Monthly rate $60
Number of months: 2
Total charges : $120
Calling the showFees function with arguments Senior, 100.0, 4.
Membership Type : Senior    Monthly rate $100
Number of months: 4
Total charges : $400
```

如程序 6-31 所示，驱动程序可以用来彻底测试一个函数。它可以使用不同的测试值反复调用该函数。当函数执行符合预期时，就可以将其放置到所属的实际程序中。

## 小乐透案例研究

### 问题描述

杰斐逊高中的数学系希望开发一个程序，以一种风趣性的方式向学生演示基础概率。特别是，他们想要一个名为“小乐透”（Little Lotto）的程序来模拟抽奖。在程序中，学生可以指定选择集中的数字数量（1–12）以及顾客挑选并与中奖号码匹配的数字数量（1 到选择集的大小之间）。所选数字的顺序并不重要。

### 示例输出

此输出明确说明了该部门想要程序执行的内容。

此程序将告诉你赢得“小乐透”的概率。

- 有多少个数字 (1-12) 可供选择？12

- 你必须选择几个数字来玩？5

你中奖的的几率是 792 次中的 1 次。

该概率为 0.0013

### 程序设计

#### 程序步骤

程序必须执行以下通用步骤：

- 获取并验证可选择的数字数量 (`n`)。

- 获取并验证必须从中选择的数字个数量 (`k`)。

- 计算从 `n` 个物品中选出一组 `k` 个物品的组合数。

- 向玩家报告其中奖几率和中奖概率。

#### 程序模块

程序将设计为一组模块，每个模块都有特定的功能。表 6-1 描述了将使用的模块：

### 表 6-1 小乐透模块

| 函数 | 描述 |
| :--- | :--- |
| `main` | 此函数解释“游戏”，组织对其他函数的调用并报告结果。 |
| `getLotteryInfo` | 此函数获取并验证可选择的数字数量 (`n`) 和必须选择的数量 (`k`)。 |
| `computeWays` | 此函数计算从 `n` 个数字中可以选出的大小为 `k` 的不同集合的数量。 |
| `factorial` | 此函数计算阶乘。被 `computeWays` 调用。 |

### 程序组织

在之前的章节中，使用了层次结构图来说明程序必须执行的动作之间的关系。它们更常用于说明组织成一组函数的程序中模块之间的关系。图 6-15 中的层次结构图说明了小乐透程序的组织结构。注意，它明确了哪些函数调用了其他函数。

### 图 6-15

img1c095ef63c7a34f9802f42.png

### 输入值的变量

```cpp
int pickFrom // 可选择的数字数量
int numPicks // 必须选择的数字数量
```

### 输出值的变量

```cpp
long int ways // 可能的选择数量
1.0 / ways // 概率
```

### 每个模块的详细伪代码

在模块化程序中，应该创建独立的伪代码程序来每个函数的逻辑。这是小乐透程序的每个函数的伪代码。

- 显示程序执行的内容

- 调用 `getLotInfo` // 将输入放入 `pickFrom` 变量

- 调用 `computeWays` // 将返回的结果存入 `ways` 变量

- 显示 `ways` 和 `ways`

- `getLotInfo` // 从用户获取并将其放入引用 `main` 函数变量的引用参数中。

- 输入 `pickFrom` 

- `computeWays` // 接收 `pickFrom` 作为 `n` 和 `numPicks` 作为 `k` 以进行计算

- `factorial` // 接收要计算的阶乘数

### 程序

对伪代码进行逻辑检查后，下一步是将伪代码扩展为最终程序。这在程序 6-32 中所示。

### 程序 6-32

```cpp
1 // 此程序寻找赢得“迷你”彩票的概率
2 // 当用户的数字与抽出的号码完全匹配时。在 main 中，它使用了三个函数。
3 #include <iostream>
4 #include <iomanip>
5 using namespace std;
6
7 // 函数原型
8 void getLotteryInfo(int, int&);
9 int computeWays(int, int);
10 long int factorial(int);
```

### 程序 6-32 (续)

```cpp
int main() { // 可选择的数字数量
    int pickFrom, // 需要选择的数字数量
    numPicks;
    long int ways; // 可能的不同选择数量

    cout << "此程序将告诉你赢得 "
    cout << "Lotto 的概率!\n";
    getLotteryInfo(pickFrom,numPicks);
    ways = computeWays(pickFrom,numPicks);

    cout << fixed << setprecision(4);
    cout << "\n中奖几率是 "
    cout << "1 in " << ways << ".\n";
    cout << "该概率为 " << (1.0 / ways) << ".\n";
    return 0;
}

getLotteryInfo(); // 从用户获取并将其放入引用 main 函数变量的引用参数。
void getLotteryInfo(int &pickFrom, int &numPicks) {
    cout << "有多少个数字 (1-12) 可供选择？ \n";
    cin >> pickFrom;
    while (pickFrom < 1 || pickFrom > 12) {
        cout << "数字必须在 1 到 12 之间。\n";
        cout << "有多少个数字 (1-12) 可供选择？ \n";
        cin >> pickFrom;
    }
    cout << "你必须选择几个数字来玩？ \n";
    cin >> numPicks;
    while (numPicks < 1 || numPicks > pickFrom) {
        if (numPicks < 1) {
            cout << "你至少必须选择一个数字。\n";
        } else { //过多
            cout << "你必须选择 " << pickFrom << " 或更少的数字。\n";
        }
    }
}
```

# 程序 6-32 (续)
