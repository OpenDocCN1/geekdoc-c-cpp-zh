
```cpp
cout << "Your grade is C.\n";

else if (testScore >= D_SCORE)

    cout << "Your grade is D.\n";

else if (testScore >= 0)

    cout << "Your grade is F.\n";

else

    cout << "Invalid test score.\n";

return 0;

}
```

## if/else if 语句与嵌套决策结构的比较

你永远不需要使用 `if/else if` 语句，因为它的逻辑可以通过嵌套的 `if/else` 语句来编码。然而，在调试代码时，长系列的嵌套 `if/else` 语句有两个特定的缺点：

- 代码可能会变得复杂且难以理解。
- 因为缩进在嵌套语句中至关重要，长系列的嵌套 `if/else` 语句可能会变得太长，导致无法在计算机屏幕上显示而无需进行水平滚动。此外，长语句在打印到纸上时往往会“换行”，使得代码更难以阅读。

`if/else if` 语句的逻辑通常比长系列的嵌套 `if/else` 语句更容易跟进。而且，由于 `if/else` 语句中的所有子句都是对齐的，语句中的行长度通常较短。

# 检查点

4.16 下面代码将显示什么？

```cpp
int funny = 7, serious = 15;

funny = serious % 2;

if (funny != 1) {

    funny = 0;

    serious = 0;

} else if (funny == 2) {

    funny = 10;

    serious = 10;

} else {

    funny = 1;

    serious = 1;

}

cout << funny << " " << serious << endl;
```

4.17 下列代码用于书店程序，以确定客户获得多少张优惠券。完成程序运行后出现的表格。

```cpp
int numBooks, numCoupons;

cout << "How many books are being purchased? ";

cin >> numBooks;

if (numBooks < 1) {

    numCoupons = 0;

} else if (numBooks < 3) {

    numCoupons = 1;

} else if (numBooks < 5) {

    numCoupons = 2;

else

    numCoupons = 3;

cout << "The number of coupons to give is "

<< numCoupons << endl;
```

如果客户购买这些数量的书，将给予相应数量的优惠券。

| 书的数量 | 给予的优惠券数量 |
|---|---|
| 1 | 1 |
| 3 | 2 |
| 4 | 2 |
| 5 | 3 |
| 10 | 3 |

## 4.7 标志 (Flags)

> **概念：** 标志是一个布尔或整数变量，用于信号某个条件的存在。

标志通常是一个 `bool` 变量，用于信号程序中是否存在某个条件。当标志变量被设置为 `false` 时，表示条件不存在。当标志变量被设置为 `true` 时，意味着条件确实存在。

例如，提议一个计算销售佣金的程序有一个 `bool` 变量，其定义和初始化所示：

```cpp
bool salesQuotaMet = false;
```

在程序中，`salesQuotaMet` 变量用作标志，指示销售人员是否达到了销售额。当我们定义变量时，将其初始化为 `false`，因为我们不知道销售人员是否已经达到了销售额。假设一个名为 `sales` 的变量持有销售额，可以使用类似代码来设置 `salesQuotaMet` 变量的值：

```cpp
if (sales >= QUOTA_AMOUNT)

    salesQuotaMet = true;

else

    salesQuotaMet = false;
```

由于这段代码的结果，`salesQuotaMet` 变量可以作为标志来指示是否已达到销售额。在程序的后续部分，我们可能会以以下方式测试标志：

```cpp
if (salesQuotaMet == true)

    cout << "You have met your sales quota!\n";
```

如果 `bool` 变量 `salesQuotaMet` 为 `true`，这段代码将显示 "You have met your sales quota!"。我们不需要使用 `==` 运算符来显式地比较 `salesQuotaMet` 与 `true` 值。这段代码等同于以下：

```cpp
if (salesQuotaMet)

    cout << "You have met your sales quota!\n";
```

## 整数标志

整数变量也可以用标志。这是因为在 C++ 中，值 `0` 被视为 `false`，而任何非零值都被视为 `true`。在所描述的销售佣金程序中，我们可以使用以下语句定义 `salesQuotaMet` 变量：

```cpp
int salesQuotaMet = 0; // means false.
```

与之前一样，我们用 `0` 初始化变量，因为我们不知道是否已经达到了额。在计算销售额后，我们可以使用类似代码来设置 `salesQuotaMet` 变量的值：

```cpp
if (sales >= QUOTA_AMOUNT)

   salesQuotaMet = 1;

else

   salesQuotaMet = 0;
```

在程序的后续部分，我们可能会以以下方式测试标志：

```cpp
if (salesQuotaMet)

    cout << "You have met your sales quota!\n";
```

> 概念：逻辑运算符将两个或多个关系表达式连接为一个，或者反转表达式的逻辑。

在上一节中，你看到了程序如何使用 `if` 语句测试两个条件。在本节中，你将看到如何使用逻辑运算符将两个或多个关系表达式合并为一个。表 4-6 列出了 C++ 的逻辑运算符。

## && 运算符

`&&` 运算符被称为逻辑与运算符。它接受两个表达式，并创建一个仅当两个子表达式都为真时才为真的表达式。这是一个使用 `&&` 运算符的语句示例：

```cpp
if (temperature < 20 && temperature > 12)

    cout << "You are in the danger";
```

在语句中，两个关系表达式合并为一个表达式。只有当温度小于 20 且大于 12 时，`cout` 语句才会执行。如果任何一个表达式为假，整个表达式即为假。

> 提示：你必须在 `&&` 运算符两侧提供完整的表达式。例如，下面的语句是不正确的，因为右侧不完整：

```cpp
if (temperature < 20 && 100)
```

`&&` 运算符可以简化原本需要嵌套 `if` 语句的程序。

## 表 4-7 && 运算符真表

| 表达式 | 表达式的值 |
|---|---|
| true && true | true (1) |
| true && false | false (0) |
| false && true | false (0) |
| false && false | false (0) |

> 注意：如果 `&&` 运算符左侧的表达式为假，则不会检查右侧。这被称为短路求值。

## 程序

```cpp
// 该程序演示了逻辑运算符。

#include <iostream>

using namespace std;

// 当前就业，Y 或 N

// 最近毕业，Y 或 N

char employed, recentGrad;

// 用户是否已就业且是应届？

int main() {

    // 回答以下问题

    // Y 表示是，N 表示否。

    cout << "Are you employed? ";

    cin >> employed;

    cout << "Have you graduated from college "

         << "in the past two years?";

    cin >> recentGrad;

    // Determine用户的资质。

    if (employed == 'Y' && recentGrad == 'Y')

    {

        cout << "You qualify for the special "

             << "interest rate.\n";

    }

    else

    {

        cout << "You must be employed and have\n"

              << "graduated from college in the\n"

              << "past two years to qualify.\n";

    }

    return 0;

}
```

## 程序 4-15 (继续)

```cpp
// ... (继续)

if (employed == 'Y' && recentGrad == 'Y')

{

    cout << "You qualify for the special "

         << "interest rate.\n";

    }

else

    {

        cout << "You must be employed and have\n"

              << "graduated from college in the\n"

              << "past two years to qualify.\n";

    }

}

// ...
```
*(注：由于原文提供的代码块 4.17 处存在明显的原始语法错误（如 else 缺少大括号和括号不匹配），翻译时保持了逻辑结构。)*

> 注意：尽管它们相似，但程序 4-15 并不是程序 4-11 的逻辑等价程序。例如，程序 4-15 不显示“你必须受雇才能符合资格”这一消息。

## || 运算符

`||` 运算符被称为逻辑或运算符。它接受两个表达式作为操作数，并创建一个当其中任一个子表达式为真时结果为真的表达式。以下是一个使用 `||` 运算符的 `if` 语句示例：

```cpp
if (temperature < 20 || temperature > 100)

cout << "The temperature is in the danger zone.";
```

如果 `temperature` 小于 20 **或者** `temperature` 大于 100，则执行 `cout` 语句。如果任何一个关系测试为真，整个表达式即为真，并执行 `cout` 语句。

> 提示：你必须在 `||` 运算符的双方都提供完整的表达式。例如，以下代码是不正确的，因为 `||` 运算符右侧的条件不是一个完整的表达式：
`temperature < 0 || > 100`

该表达式必须重写为：

```cpp
temperature < 0 || temperature > 100
```

表 4-8 显示了 `||` 运算符的真值表。

## 表 4-8 || 运算符的真值表

| 表达式 | 表达式的值 |
| :--- | :--- |
| true \|\| false | true (1) |
| false \|\| true | true (1) |
| false \|\| false | false (0) |
| true \|\| true | true (1) |

一个或表达式要为真的条件是其中一个子表达式为真。另一个子表达式是真还是假并不重要。

> 注意：`||` 运算符还执行短路求值。如果 `||` 表达式左侧的子表达式为真，则不会检查右侧的表达式。由于只需要一个子表达式为真，检查剩余表达式将浪费 CPU 时间。

程序 4-16 执行了不同的测试以判断某人是否符合贷款条件。此程序判断客户年收入是否至少达到 $35,000，或者工作是否已超过 5 年。

## 程序 4-16

```cpp
 // 此程序演示了逻辑 || 运算符。

#include <iostream>

using namespace std;

int main() {

    // 最小收入和年数的常量

    const double MIN_INCOME = 35000.0;

    const int MIN_YEARS = 5;

    double income; // 年收入

    int years; // 在当前工作的年限

    // 获取年收入

    cout << "What is your annual income? ";

    cin >> income;

    // 获取在当前工作的年限。

    cout << "How many years have you worked at ";

         << "your current job? ";

    cin >> years;

    // 用户的贷款资格。

    if (income >= MIN_INCOME || years > MIN_YEARS)

        cout << "You qualify.\n";

    else {

        cout << "You must earn at least $"

             << MIN_INCOME << " or have been "

             << "employed more than " << MIN_YEARS

             << " years.\n";

    }

    return 0;

}
```

## 程序输出（示例输入已加粗）

What is your annual income? **40000**
How many years have you worked at your current job? **2**
You qualify.

## 程序输出（示例输入已加粗）

What is your annual income? **20000**
How many years have you worked at your current job? **7**
You qualify.

## 程序输出（示例输入已加粗）

What is your annual income? **30000**
How many years have you worked at your current job? **3**
You must earn at least $35000 or have been employed more than 5 years.

# 第 4 章 决策

| 逻辑表达式 | 结果（真或假） |
|---|---|
| true && false | |
| true && true | |
| false && true | |
| false && false | |
| true \|\| false | |
| true \|\| true | |
| false \|\| true | |
| false \|\| false | |
| !true | |
| !false | |

4.19 假设变量 `a = 2, b = 4, 和 c = 6`。确定以下每个条件是否为真（True）或假（False）：

- A) `a == 4 || b > 2`
- B) `6 <= c && a > 3`
- C) `1 != b && c != 3`
- D) `a >= -1 || a <= b`
- E) `(a > 2)`

4.20 编写一个 `if` 语句，如果变量 `speed` 在 0 到 200 的范围内，则打印消息“The number is valid”。

4.21 编写一个 `if` 语句，如果变量 `speed` 在 0 到 200 的范围之外，则打印消息“The number is not valid”。

![](img/191adf3284699566e6a7b1008ce9bdb5_225_0.png)

> 概念：你可以使用嵌套 `if/else` 语句或 `if/else if` 语句来创建菜单驱动程序。菜单驱动程序允许用户通过从操作列表中选择来决定行动方案。

菜单是一个显示一组选项的屏幕，用户从中进行选择。例如，一个管理邮件列表的程序可能会提供以下菜单：

- 向列表中添加姓名。
- 从列表中删除姓名。
- 更改列表中的一个姓名。
- 打印列表。
- 退出程序。

用户通过输入数字来选择其中一种操作。例如，输入 4 会导致打印邮件列表，输入 5 则导致程序结束。可以使用嵌套 `if/else` 语句或 `if/else` 结构来设置此类菜单。在用户输入数字后，程序会将该数字与可用选项进行比较，并执行执行该操作的语句。

程序 4-18 计算健康俱乐部会员的费用。俱乐部有三种会员方案供选择：标准成人会员、俱乐部会员和老年人会员。程序呈现一个菜单，允许用户选择所需的方案，然后计算会员费用。

# 程序 4-18

```cpp
 // 此程序显示一个菜单并要求用户做出

// 选择。使用一个 if/else if 语句来确定用户

// 选了哪一个项目。

#include <iostream>

#include <iomanip>

using namespace std;

int main()

{

    int choice; // 用于存储菜单选择

    int months; // 用于存储月份数

    double charges; // 用于存储月费

    // 会员费率常量

    const double ADULT = 40.0,

           SENIOR = 30.0,
```
