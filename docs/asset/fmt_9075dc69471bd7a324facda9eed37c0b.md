
```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<int> intVector;
    // 将数字 1, 2, 3, 4, 5, ..., 10 存储到 vector
    for (int i = 0; i < 10; i++)
        intVector.push_back(i + 1);

    // 显示 vector 中的数字
    cout << "Numbers in the vector: ";
    for (int i = 0; i < intVector.size(); i++)
        cout << intVector[i] << " ";

    vector<string> stringVector;
    // 将字符串存储到 vector
    stringVector.push_back("Dallas");
    stringVector.push_back("Houston");
    stringVector.push_back("Austin");
    stringVector.push_back("Norman");

    // 显示 vector 中的字符串
    cout << "\nStrings in the vector: ";
    for (int i = 0; i < stringVector.size(); i++)
        cout << stringVector[i] << " ";

    stringVector.pop_back(); // 移除最后一个元素
    vector<string> v2;
    v2.swap(stringVector);
    v2[0] = "Atlanta";

    // 显示 vector v2 中的字符串
    cout << "\nStrings in the vector v2: ";
    for (int i = 0; i < v2.size(); i++)
        cout << v2.at(i) << " ";

    return 0;
}
```

- `vector` 头文件
- `string` 头文件
- 创建一个 `vector`
- 添加 `int` 值
- 添加 `string`
- `vector` `size`
- 创建 `vector`
- `vector` `size`
- `vector` 下标
- 移除元素
- 创建 `vector`
- `swap` `vector`
- 分配 `string`
- `vector` `size`
- `at` 函数

![](img/3b8bc24ba08ad32ac1a370eb095746a9_429_0.png)

程序使用了 `vector` 类，包含了其头文件。由于 `string` 类也被使用，包含了其头文件。在第 8 行创建存储 `int` 值的 `vector`。在第 11 行将 `int` 值添加到 `vector`。`vector` 的 `size` 没有限制。随着更多元素的添加，`size` 会自动增长。在第 15–17 行显示所有 `int` 值。在第 17 行使用下标 `[]` 获取元素。在第 19 行创建 `string`。在第 22–25 行向 `vector` 添加四个字符串。在第 29–30 行显示 `vector` 中的字符串。在第 30 行使用下标 `[]` 获取元素。第 32 行从 `vector` 移除最后一个 `string`。第 34 行创建另一个 `vector`。第 35 行将 `v2` 与 `stringVector` 交换。第 36 行将新的 `string` 分配给 `v2[0]`。

`size()` 函数返回 `unsigned int` 类型的 `size`，而不是 `int`。某些编译器在将 `unsigned` 值与 `signed int` 使用时可能会警告（第 16、29、40 行）。这只是一个警告，不会引起问题，因为在需要时 `unsigned` 值会自动提升为 `signed`。为了消除警告，在第 16 行将 `i` 声明为 `unsigned int`，如下：

```cpp
for (unsigned int i = 0; i < size(); i++)
```

## 12.7 使用 vector 替换数组

`vector` 是可调整数组。使用 `vector` 比数组更灵活。之前所有使用数组的章节都可以使用 `vector`。本节重写了列表 7.2、`DeckOf.cpp` 以及列表 8.1 `PassDimensionalArray`。

回列表 7.2 是一个从52张牌中随机挑选牌的程序。我们使用 `vector` 来存储值为 0 到 51 的 52 张牌，如下：

```cpp
const int NUMBER_OF_CARDS = 52;
vector<int> deck(NUMBER_OF_CARDS);
```

```cpp
// 初始化牌
for (int i = 0; i < NUMBER_OF_CARDS; i++)
    deck[i] = i;
```

`deck[0]` 到 `deck[12]` 是桃梅，`deck[13]` 到 `deck[25]` 是菱形，`deck[26]` 到 `deck[38]` 是红桃，`deck[39]` 到 `deck[51]` 是黑花。列表 12.9 给出了问题的解决方案。

## 12.9 DeckOfCardsUsingVector.cpp

```cpp
#include <iostream>
#include <vector>
#include <ctime>
using namespace std;
const int NUMBER_OF_CARDS = 52;
void displayRank(int rank)
{
    if (rank == 0)
        cout << "Ace of ";
    else if (rank == 10)
        cout << "Jack of ";
    else if (rank == 11)
        cout << "Queen of ";
    else if (rank == 12)
        cout << "King of ";
    else
        cout << rank << " of";
}

void displaySuit(int suit)
{
    if (suit == 0)
        cout << "Clubs" << endl;
    else if (suit == 1)
        cout << "Diamonds" << endl;
    else if (suit == 2)
        cout << "Hearts" << endl;
    else if (suit == 3)
        cout << "Spades" << endl;
}
```

```cpp
int main()
{
    vector<int> deck(NUMBER_OF_CARDS);

    // 初始化牌
    for (int i = 0; i < NUMBER_OF_CARDS; i++)
        deck[i] = i;

    // 洗牌
    srand(time(0));
    for (int i = 0; i < NUMBER_OF_CARDS; i++)
    {
        // 随机生成索引
        int index = rand() % NUMBER_OF_CARDS;
        int temp = deck[i];
        deck[i] = deck[index];
        deck[index] = temp;
    }

    // 显示前四张牌
    for (int i = 0; i < 4; i++)
    {
        displayRank(deck[i] % 13);
        displaySuit(deck[i] / 13);
    }

    return 0;
}
```

- 初始化牌
- 洗牌
- 显示点数
- 显示花色

| 4 of Clubs

Ace of Diamonds

6 of Hearts

Jack of Clubs |

该程序与列表 7.2 完全相同，但第 2 行包含了 `vector`，第 36 行创建的是 `vector` 而不是数组。有趣的是，使用数组和 `vector` 的语法非常相似，因为你可以使用下标索引来访问 `vector` 中的元素，这与访问数组元素的方式一致。

## 12.7 使用 vector 类替换数组 407

回想代码列表 8.1，它创建了一个二维数组并调用一个函数返回数组中所有元素的和。可以使用嵌套的 `vector`（a vector of vectors）来表示二维数组。这里是一个表示四行三列数组的示例：

```cpp
vector<vector<int>> matrix(4); // 四行
```

```cpp
for (int i = 0; i < 4; i++)
    matrix[i] = vector<int>(3);
```

```cpp
matrix[0][0] = 1; matrix[0][1] = 2; matrix[0][2] = 3;
matrix[1][0] = 4; matrix[1][1] = 5; matrix[1][2] = 6;
matrix[2][0] = 7; matrix[2][1] = 8; matrix[2][2] = 9;
matrix[3][0] = 10; matrix[3][1] = 11; matrix[3][2] = 12;
```

> 注意
>
> 在这一行中，`>>` 之间有一个空格
>
> `vector<vector<int>> matrix(4); // Four rows`
>
> 如果没有空格，某些旧的 C++ 编译器可能无法编译。

代码列表 12.10 使用 `vector` 修改了代码列表 8.1 的 `PassTwoDimensionalArray.cpp`。

## 代码列表 12.10 TwoArrayUsingVector.cpp

```cpp
#1 #include <iostream>
#2 #include <vector>
#3 using namespace std;
4
#5 int sum(const vector<vector<int>> &matrix)
6 {
7 int total = 0;
8 for (int row = 0; row < matrix.size(); row++)
9 {
10 for (int column = 0; column < matrix[row].size(); column++)
11 {
12 total += matrix[row][column];
13 {}
14 }
15
16 return total;
17 }
18
19 int main()
20 {
21 vector<vector<int>> matrix(4); // 四行
22 for (int i = 0; i < 4; i++)
23 matrix[i] = vector<int>(3); // 每行有三列
24
25 matrix[0][0] = 1; matrix[0][1] = 2; matrix[0][2] = 3;
26 matrix[1][0] = 4; matrix[1][1] = 5; matrix[1][2] = 6;
27 matrix[2][0] = 7; matrix[2][1] = 8; matrix[2][2] = 9;
28 matrix[3][0] = 10; matrix[3][1] = 11; matrix[3][2] = 12;
29
30 cout << "Sum of all elements is " << sum(matrix) << endl;
31 return 0;
32 }
```

包含 `vector`
带有 `vector` 的函数
用于二维数组的 `vector`
赋值值

# 第 12 章 模板与 vector

所有元素的和为 78

变量 `array` 被声明为一个 `vector`。`vector matrix[i]` 的每个元素都是另一个 `vector`。因此，`matrix[i][j]` 表示二维数组中的第 `i` 行和第 `j` 列。

`sum` 函数返回 `vector` 中所有元素的和。`vector` 的大小可以通过 `vector` 类中的 `size()` 函数获取。因此，在调用 `sum` 函数时，不需要指定 `vector` 的大小。用于二维数组的相同函数需要如下两个参数：

```cpp
int sum(const int a[][COLUMN_SIZE],
```

表示二维数组的 `vector` 简化了编码。

## 12.8 案例研究：表达式求值

栈有很多应用。本节介绍了栈的应用。你可以输入一个算术表达式，并如图 12.3 所示进行求值。

复合表达式

![](img/3b8bc2408ad32ac1a370eb09531_0.png)

图 12.3 你可以计算算术表达式。

程序如何计算表达式？本节介绍了一个处理多个运算符和括号的复合表达式程序（例如 `(5 + 2) * 3`）。为了简单起见，假设操作数是整数，运算符有四种：`+`, `-`, `*`, `/`。这个问题可以使用两个栈来解决，分别命名为 `operandStack`（操作数栈）和 `operatorStack`（运算符栈）。操作数和运算符在处理之前会被压栈。当处理运算符时，它从 `operatorStack` 中弹出并应用于前两个操作数。结果被推回 `operandStack`。

阶段 I：扫描表达式

程序从左到右扫描表达式的操作数、运算符和括号。

- 如果提取的是操作数，将其推入 `operandStack`。
- 如果提取的是 `+` 或 `-` 处理 `operatorStack` 中优先级高于或相同的运算符（即 `*`, `/`），将提取的运算符推入栈。
- 如果提取的是 `*` 或 `/` 处理 `operatorStack` 中优先级高于或相同的运算符（即 `*`, `/`），将提取的运算符推入栈。
- 如果提取的是 `(`，将其推入 `operandStack`。
- 如果提取的是 `)`，重复处理 `operatorStack` 头部运算符，直到遇到 `(`。

阶段 II：清栈

重复处理 `operatorStack` 头部运算符，直到 `operatorStack` 为空。下图显示了该算法如何应用于 `(1 + 2) * 3`。

第 12 章 模板与 vector

![](img/3b8bc2408ad32ac1a370eb0953_0.png) `(1 + 2) * 3` After `*` 被处理

![](img/3b8bc2408ad32ac1a370eb09531_1.png) `(1 + 2) * 3` After `-` 被存储

![](img/3b8bc2408ad32ac1a370eb09531_2.png) `(1 + 2) * 3` After `-` 被处理

![](img/3b8bc2408ad32ac1a370eb09531_3.png) `(1 + 2) * 3` After `-` 被处理

代码列表 12.11 提供了程序。

## 代码列表 12.11 EvaluateExpression.cpp

```cpp
1 #include <iostream>
#2 #include <vector>
#3 #include <string>
#4 #include <cctype>
#5 #include "ImprovedStack.h"
6
7 using namespace std;
8
9 将表达式拆分为数字、运算符和括号
10 vector<string> split(const string &expression);
11
12 计算表达式并返回结果
13 int evaluateExpression(const string &expression);
14
15 执行操作
16 void processAnOperator(
17 Stack<int>& &operatorStack, Stack<char> &operatorStack);
18
19 int main()
20 {
21 string expression;
22 cout << "Enter an expression: ";
23 getline(cin, expression);
24
25 cout << expression << " - " <<n26 << evaluateExpression(expression) << endl;
27
28 return 0;
29 }
30
31 vector<string> split(const string &expression)
32 {
33 vector<string> v; // 用于存储拆分字符串的 vector
34 string numberString; // 数字字符串
35
36 for (int i = 0; i < expression.length(); i++)
```
