
`outFile << "无数据。" << endl;`

```cpp
inputFile.close();
outFile.close();
return 0;
```

运行示例：
输入文件：

Steve Gill 89
Rita Johnson 91.5
Randy Brown 85.5
Seema Arora 76.5
Samir Mann 73
Samantha McCoy 85.5

输出文件：

Steve Gill 89.00 B
Rita Johnson 91.50 A
Randy Brown 85.50 B
Seema Arora 76.50 C
Samir Mann 73.00 C
Samantha McCoy 88.50 B

班级平均分: 84.00

# 268 | 第5章：控制结构II（循环）

上述程序的工作原理如下：第8到13行的语句声明并初始化了程序所需的变量。第14和15行的语句将 `inFile` 为 `ifstream` 变量，将 `outFile` 为 `ofstream` 变量。第16行的语句使用变量 `inFile` 打开输入文件。如果输入文件不存在，第17到21行的语句将输出适当的消息并终止程序。第22行的语句使用变量 `outFile` 打开输出文件。第23行的语句将浮点数的输出设置为固定格式，保留两位小数并补零。

第24和25行的语句以及第26行的循环读取每个学生的名、姓和测试分数，然后用测试分数和等级更新输出文件。第28行的测试分数语句更新 `sum` 的值（在读取所有数据后，`sum` 的值存储了所有分数的总和）。第29行的语句更新 `count` 的值（该变量统计班级学生人数）。第30到55行的 `switch` 语句根据 `testScore` 确定等级并将其存储在变量 `grade` 中。第56行的语句输出学生的名、姓、测试分数和等级。

第61到64行的 `if...else` 语句输出班级平均分，第65和66行的语句关闭文件。

随本书附带的网络编程示例“检查账户余额（Checking Account Balance）”进一步说明了如何在程序中使用由 EOF 控制的 `while` 循环。

# 关于 while 语句中表达式更多

在之前章节的示例中，`while` 语句中的 `while` 非常简单。换句话说，`while` 循环由单个变量控制。然而，在某些情况下，`while` 语句中的表达式可能会更加复杂。

例如，5-6中的程序使用标志控制的 `while` 循环来实现猜数字游戏。它根据用户猜数字所需的次数提供尝试。假设你想给用户最多五次机会猜数字。如果用户在五次内没有猜中数字，程序将输出生成的随机数以及一条你输了游戏的消息。在这种情况下，你可以这样写 `while` 循环，`noOfGuesses` 为：

```cpp
while (noOfGuesses < 5 && !isGuessed) {
    cout << "输入你的猜测：";
    cin >> guess;
    noOfGuesses++;
    if (guess == num) {
        isGuessed = true;
        cout << "你赢了!" << endl;
    } else if (guess < num) {
        cout << "太小了!" << endl;
    } else {
        cout << "太大了!" << endl;
    }
}
```

```cpp
if (!isGuessed) {
    cout << "游戏结束。数字是 " << num << endl;
}
```

本章末的编程练习16要求你编写一个C++ 程序，实现猜数字游戏，用户最多有五次机会猜一个1 到 100 之间的随机数。

## 编程示例：斐波那契数 | 271

```cpp
int current;      //用于存储当前的
//斐波那契数
int counter;     //循环控制变量
int nthFibonacci; //用于存储所需的
//斐波那契数
```

要计算第三个数，将 `previous1` 和 `previous2` 的值相加并将结果存储在 `current` 中。计算第四个斐波那契数，将第二个斐波那契数（即 `previous2`）的值与第三个斐波那契数的值（即 `current`）相加。因此，计算第四个斐波那契数时，不再需要第一个斐波那契数。与其声明额外的变量（可能会过多），在计算出一个斐波那契数以确定下一个之后，`current` 变为 `previous2`，而 `previous2` 变为 `previous1`。因此，你可以使用变量 `current` 来存储下一个斐波那契数。这个过程一直重复直到计算出所需的斐波那契数。初始时 `previous1` 和 `previous2` 是序列的前两个元素，由用户提供。根据前面的讨论，可以你需要五个变量。

- 1. 提示用户输入两个数字——即 `previous1` 和 `previous2`。
- 2. 读取（输入）前两个数字到 `previous1` 和 `previous2`。
- 3. 输出前两个斐波那契数。（回显输入）
- 4. 提示用户所需的斐波那契数的位置。
- 5. 将所需的斐波那契数的位置读入 `nthFibonacci`。
- 6. a. 如果 (`nthFibonacci == 1`)，所需的斐波那契数就是第一个斐波那契数。将 `previous1` 的值复制到 `current`。
   b. 否则如果 (`nthFibonacci == 2`)，所需的斐波那契数是第二个斐波那契数。将 `previous2` 的值复制到 `current`。
   c. 否则计算所需的斐波那契数：因为你已经知道了序列的前两个斐波那契数，通过确定第三个斐波那契数来实现。
   c.1. 将 `counter` 初始化为 3，以跟踪已计算的斐波那契数。
   c.2. 计算下一个斐波那契数，如下：`current = previous2 + previous1;`
   c.3. 将 `previous2` 的值赋给 `previous1`。
   c.4. 将 `current` 的值赋给 `previous2`。
   c.5. `counter` 加1。

主算法

![](img/abc25bb507ebb3eb05460d88ce0e0fde_311_0.png)

## 272 | 第5章：控制结构 II（重复）

重复步骤 c.2 到 c.5，直到计算出你需要的斐波那契数为止。

以下 while 循环执行步骤 c.2 到 c.5 并确定第 n 个斐波那契数。

```cpp
while (counter <= nthFibonacci)
{
  current = previous2 + previous1;
  previous1 = previous2;
  previous2 = current;
  counter++;
}
```

- 7. 输出第 `nthFibonacci` 个数，即 `current`。

## 完整程序列表

```cpp
****************************************************************************************************
// 作者：D.S. Malik
//
// 程序：第 n 个斐波那契数
// 给定斐波那契序列的前两个数，该
// 程序确定并输出所需的斐波那契
// 序列。
****************************************************************************************************

#include <iostream>
using namespace std;
int main()
{
  //声明变量
  int previous1;
  int previous2;
  int current;
  int counter;
  int nthFibonacci;

  cout << "输入前两个斐波那契"
       << "数: "; //步骤 1
  cin >> previous1 >> previous2; //步骤 2
  cout << endl;
  cout << "前两个斐波那契数是"
       << previous1 << " 和 " << previous2; //步骤 3
  cout << endl;
  cout << "输入所需的斐波那契"
       << "数的位置: "; //步骤 4
  cin >> nthFibonacci; //步骤 5
  cout << endl;

  if (nthFibonacci == 1) //步骤 6. a
    current = previous1;
```

```cpp
  else if (nthFibonacci == 2)
    current = previous2;
  else
  {
    counter = 3;
    //步骤 6.c.2 - 6.c.5
    while (counter <= nthFibonacci)
    {
        current = previous2 + previous1;
        previous1 = previous2;
        previous2 = current;
        counter++;
    }
  }

  cout << "位置在 "
    << nthFibonacci << " 的斐波那契数是 " << current
    << endl;

  return 0;
}//结束 main
```

示例运行：在这些示例运行中，用户输入用阴影表示。

示例运行 1：

输入前两个斐波那契数：12 16

前两个斐波那契数是 12 和 16

输入所需的斐波那契数的位置：10

位置在 10 的斐波那契数是 796

示例运行 2：

输入前两个斐波那契数：1 1

前两个斐波那契数是 1 和 1

输入所需的斐波那契数的位置：15

位置在 15 的斐波那契数是 610

## for 循环（重复）结构

上一节讨论的 while 循环足够通用，可以实现大多数形式的重复。这里描述的 C++ for 结构是 for 循环的特殊形式。其目的是简化计数器的编写。

## 第5章：控制结构 II（重复）

上一节讨论的 while 循环足够通用，可以实现大多数形式的重复。这里描述的 C++ for 结构是 for 循环的特殊形式。其目的是简化计数器的编写。

## 第5章：控制结构 II（重复）

（此处为重复内容，保持翻译一致）

...most forms of repetitions. The C++ for structure described here is a specialized form of the for loop...

（重复内容省略）

## 第5章：控制结构 II（重复）

上一节讨论的 while 循环足够通用，可以实现大多数形式的重复。这里描述的 C++ for 结构是 for 循环的特殊形式。其目的是简化计数器的编写。

314

（重复内容省略）

315

（重复内容省略）

16

（重复内容省略）

用于循环（重复）结构 | 277

输出结果为：

10 9 8 7 6 5 4 3 2 1

在这个 for 循环中，变量 `i` 被初始化为 10。在每次循环迭代后，`i` 都会减 1。只要 `i>= 1`，循环就会继续执行。

# 示例 5-13

你可以通过任何固定数值增加（或减少）循环控制变量。在下面的 for 循环中，变量被初始化为 1；在 for 循环结束时，`i` 增加了 2。这个 for 循环输出前 10 个正奇数。

```cpp
for (i = 1; i <= 20; i = i + 2)
cout << " " << i;
cout << endl;
```

# 示例 5-14

假设 `i` 是一个 `int` 类型的变量。

- 考虑以下 for 循环：

```cpp
for (i = 10; i <= 9; i++)
cout << " " << ""
cout << endl;
```

在这个 for 循环中，初始化语句将 `i` 设置为 10。初始时，循环条件 (`i <= 9`) 为假，什么都没有发生。

- 考虑以下 for 循环：

```cpp
for (i = 9; i >= 10; i--)
cout << " " << ""
cout << endl;
```

在这个 for 循环中，初始化语句将 `i` 设置为 9。因为初始时循环条件 (`i >= 10`) 为假，什么都没有发生。

- 考虑以下 for 循环：

```cpp
for (i = 10; i <= 10; i++)
cout << " " << ""
cout << endl;
```

在这个 for 循环中，初始化语句将 `i` 设置为 10。循环条件 (`i <= 10`) 结果为真，因此第 2 行的输出语句执行，输出 10。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_317_0.png)

接下来，更新语句将 `i` 的值加 1，因此 `i` 的值变为 11。现在循环求值为为，for 循环终止。注意，第 2 行之后的输出只执行了一次。

- 4. 考虑以下 for 循环：

```cpp
for (i = 1; i < 10; i++); //第 1 行
cout << i << " "; //第 2 行
cout << endl; //第 3 行
```

这个 for 循环对第 2 行的输出没有影响。for 循环末尾的分号终止了 for 循环；因此 for 循环的作用体。该语句独立存在并执行一次。

- 5. 考虑以下 for 循环：

```cpp
for (i = 1; ; i++)
cout << i << " ";
cout << endl;
```

在这个 for 循环中，因为 for 语句中省略了循环条件，循环条件始终为真。这是一个无限循环。

# 示例 5-15

在这个示例中，for 循环读取五个数字并找到它们的和与平均值。考虑下面的程序代码，其中 `i`, `newNum`, `sum` 和 `average` 都是 `int` 变量。

`sum = 0;`

```cpp
for (i = 1; i <= 5; i++)
{
    cin >> newNum;
    sum = sum + newNum;
}
```

```cpp
average = sum / 5;
cout << "The sum is " << sum << endl;
cout << "The average is " << average << endl;
```

在前面的 for 循环中，在读取一个 `newNum` 后，该值会被加到之前计算的之前读取的所有数字的（部分）和上。变量 `sum` 在 for 循环之前被初始化为 0。因此，程序读取第一个数字并将其加到 `sum` 上，变量 `sum` 存储了第一个数字的正确和。

for 循环的语法如下：

```cpp
for (初始化表达式; 逻辑表达式; 更新表达式)
语句
```

在功能上等同于下面的 while 语句：

```cpp
初始化表达式
while (表达式)
{
    语句
    更新表达式
}
```

例如，下面的 for 循环和 while 循环是等价的：

```cpp
for (int i = 0; i < 10; i++)      int i = 0;
while (i < 10)
cout << i << " ";                 cout << i << " ";
cout << endl;                                 ++;
```

如果循环的迭代次数是已知或可以预定的，程序员通常使用 for 循环。

# 示例 5-16（斐波那契数程序：重温）

上一节中的“给定的斐波那契数”编程示例使用了 while 循环来确定所需的斐波那契数。你可以将 while 循环替换为等价的 for 循环，如下：

```cpp
for (counter = 3; counter < nthFibonacci; counter++)
{
    current = previous2 + previous1;
    previous1 = previous2;
    previous2 = current;
}
```

```cpp
//for 结束
```

使用 for 循环确定所需斐波那契数的程序的完整程序列表位于随书附的网站上。该程序名为 `Ch5_FibonacciNumberUsingAForLoop.cpp`。

在接下来的 C++ 程序中，我们建议你走过每一个步骤。

# 示例 5-17

下面的 C++ 程序计算 n 个整数的和。

```cpp
#include <iostream>
using namespace std;

int main() {
    int counter;
    int sum = 0;
    int n;

    cout << "Enter the number of integers: ";
    cin >> n;

    for (counter = 1; counter <= n; counter++) {
        cout << "Enter an integer: ";
        cin >> counter;
        sum += counter;
    }

    cout << "The sum is " << sum << endl;

    return 0;
}
```

**示例运行：**

Enter the number of integers: 5

Enter an integer: 10

...

Enter an integer: 50

The sum is 150

## 嵌套

# 编程示例：数字分类

记住，将一个控制语句放在另一个语句内部被称为**嵌套**。下面的示例展示了嵌套的简单实例。
